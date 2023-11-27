### React Forms

**What is React Hook Form?**

React Hook Form takes a slightly different approach than other form libraries in the React ecosystem by adopting the use of uncontrolled inputs using ref instead of depending on the state to control the inputs. This approach makes the forms more performant and reduces the number of re-renders.

The package size is tiny (just 8.6 kB minified and gzipped) and it has zero dependencies. The API is very intuitive, which provides a seamless experience to developers. React Hook Form follows HTML standards for validating the forms using a constraint-based validation API.

Another great feature offered by React Hook Form is its painless integration with UI libraries because most libraries support the ref attribute.

To install React Hook Form, run the following command:

```npm install react-hook-form```

*How to use React Hooks in a form*

In this section, you will learn about the fundamentals of the useForm Hook by creating a very basic registration form.

First, import the useForm Hook from the react-hook-form package:

```react import { useForm } from "react-hook-form"; ```

Then, inside your component, use the Hook as follows:

```react const { register, handleSubmit } = useForm(); ```

The useForm Hook returns an object containing a few properties. For now, you only require register and handleSubmit.

The register method helps you register an input field into React Hook Form so that it is available for the validation, and its value can be tracked for changes.

To register the input, we’ll pass the register method into the input field as such:

```react
 <input type="text" name="firstName" {...register('firstName')} /> 
 ```

This spread operator syntax is a new implementation to the library that enables strict type checking in forms with TypeScript. You can learn more about strict type checking in React Hook Form here.

Versions older than v7 had the register method attached to the ref attribute as such:

```react 
<input type="text" name="firstName" ref={register} /> 
```
Note that the input component must have a name prop, and its value should be unique.

The handleSubmit method, as the name suggests, manages form submission. It needs to be passed as the value to the onSubmit prop of the form component.

The handleSubmit method can handle two functions as arguments. The first function passed as an argument will be invoked along with the registered field values when the form validation is successful. The second function is called with errors when the validation fails.

```react 
const onFormSubmit  = data => console.log(data);
const onErrors = errors => console.error(errors);
<form onSubmit={handleSubmit(onFormSubmit, onErrors)}>
 {/* ... */}
</form> ```

Now that you have a fair idea about the basic usage of the useForm Hook, let’s take a look at a more realistic example:

```react
import React from "react";
import { useForm } from "react-hook-form";

const RegisterForm = () => {
  const { register, handleSubmit } = useForm();
  const handleRegistration = (data) => console.log(data);

  return (
    <form onSubmit={handleSubmit(handleRegistration)}>
      <div>
        <label>Name</label>
        <input name="name" {...register('name')} />
      </div>
      <div>
        <label>Email</label>
        <input type="email" name="email" {...register('email')} />
      </div>
      <div>
        <label>Password</label>
        <input type="password" name="password" {...register('password')} />
      </div>
      <button>Submit</button>
    </form>
  );
};
export default RegisterForm;
```

As you can see, no other components were imported to track the input values. The useForm Hook makes the component code cleaner and easier to maintain, and because the form is uncontrolled, you do not have to pass props like onChange and value to each input.

You can use any other UI library of your choice for creating the form. But first make sure to check the docs, and find the prop used for accessing reference attribute of the native input component.

In the next section, you will learn how to handle form validation in the form we just built.

*How to validate forms with React Hook Form?*
To apply validations to a field, you can pass validation parameters to the register method. Validation parameters are similar to the existing HTML form validation standard.

These validation parameters include the following properties:

```required``` indicates if the field is required or not. If this property is set to true, then the field cannot be empty
minlength and maxlength set the minimum and maximum length for a string input value
min and max set the minimum and maximum values for a numerical value
type indicates the type of the input field; it can be email, number, text, or any other standard HTML input types
pattern defines a pattern for the input value using a regular expression
If you want to mark a field as required, you code should turn out like this:

```react
<input name="name" type="text" {...register('name', { required: true } )} />
``` 
Now try submitting the form with this field empty. This will result in the following error object:

```react
{
name: {
  type: "required",
  message: "",
  ref: <input name="name" type="text" />
  }
}
```

Here, the type property refers to the type of validation that failed, and the ref property contains the native DOM input element.

You can also include a custom error message for the field by passing a string instead of a boolean to the validation property:

```
// ...
<form onSubmit={handleSubmit(handleRegistration, handleError)}>
  <div>
      <label>Name</label>
      <input name="name" {...register('name', { required: "Name is required" } )} />
  </div>
</form>
```

Then, access the errors object by using the useForm Hook:
```react
const { register, handleSubmit, formState: { errors } } = useForm();
```
You can display errors to your users like so:
```
const RegisterForm = () => {
  const { register, handleSubmit, formState: { errors } } = useForm();
  const handleRegistration = (data) => console.log(data);

  return (
    <form onSubmit={handleSubmit(handleRegistration)}>
      <div>
        <label>Name</label>
        <input type="text" name="name" {...register('name')} />
        {errors?.name && errors.name.message}
      </div>
      {/* more input fields... */}
      <button>Submit</button>
    </form>
  );
};
```
Below you can find the complete example:
```
import React from "react";
import { useForm } from "react-hook-form";

const RegisterForm = () => {
  const { register, handleSubmit, formState: { errors } } = useForm();
  const handleRegistration = (data) => console.log(data);
  const handleError = (errors) => {};

  const registerOptions = {
    name: { required: "Name is required" },
    email: { required: "Email is required" },
    password: {
      required: "Password is required",
      minLength: {
        value: 8,
        message: "Password must have at least 8 characters"
      }
    }
  };

  return (
    <form onSubmit={handleSubmit(handleRegistration, handleError)}>
      <div>
        <label>Name</label>
        <input name="name" type="text" {...register('name', registerOptions.name) }/>
        <small className="text-danger">
          {errors?.name && errors.name.message}
        </small>
      </div>
      <div>
        <label>Email</label>
        <input
          type="email"
          name="email"
          {...register('email', registerOptions.email)}
        />
        <small className="text-danger">
          {errors?.email && errors.email.message}
        </small>
      </div>
      <div>
        <label>Password</label>
        <input
          type="password"
          name="password"
          {...register('password', registerOptions.password)}
        />
        <small className="text-danger">
          {errors?.password && errors.password.message}
        </small>
      </div>
      <button>Submit</button>
    </form>
  );
};
export default RegisterForm;
```
If you want to validate the field when there is an onChange or onBlur event, you can pass a mode property to the useForm Hook:

```react
const { register, handleSubmit, errors } = useForm({
  mode: "onBlur"
});
```
Find more details on the useForm Hook in the [API reference](https://react-hook-form.com/docs#useForm).

## Useful Links

* [React Hooks Form Playlist](https://www.youtube.com/watch?v=KejZXxFCe2k&list=PLC3y8-rFHvwjmgBr1327BA5bVXoQH-w5s&ab_channel=Codevolution)

### [Lesson 3. Homework](/Lesson-3/HW-Lesson-3)