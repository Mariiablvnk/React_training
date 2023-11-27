## Lesson-3
### API Calls In React 

**What Is a React API Call?**

An API call in React refers to making a request to a web API from a React application. React uses API calls to connect with external services to receive or send data. They allow your React application to interact with other systems and exchange information with them.

*3 Ways to Make React API Calls*
In React, we can make the API call in the following ways:

* XMLHttpRequest
*Fetch API
*Axios

1. **XMLHTTPREQUEST**
In JavaScript, the XMLHttpRequest object is an API for sending HTTP requests from a web page to a server. It’s a low-level API because it only provides a basic mechanism for making HTTP requests and leaves it up to the developer to parse the response, handle errors and manage the request’s state. Here’s an example of how it can make an API call:
```react
import React, { useState } from 'react';

function Example() {
  const [data, setData] = useState(null);

  function handleClick() {
    const xhr = new XMLHttpRequest();
    xhr.open('GET', 'https://api.example.com/data');
    xhr.onload = function() {
      if (xhr.status === 200) {
        setData(JSON.parse(xhr.responseText));
      }
    };
    xhr.send();
  }

  return (
    <div>
      <button onClick={handleClick}>Get Data</button>
      {data ? <div>{JSON.stringify(data)}</div> : <div>Loading...</div>}
    </div>
  );
}
``` 

2. **FETCH API**
Fetch API is a modern, promise-based API for making HTTP requests in JavaScript. It provides a simple and flexible interface for making GET, POST, PUT and DELETE requests and handling the response from the server.

Here’s an example of how you can use fetch to make a GET request to retrieve data from a server in a React component:

```react
import React, { useState, useEffect } from 'react';

function App() {
  const [data, setData] = useState(null);

  useEffect(() => {
    fetch('https://api.example.com/data')
      .then(response => response.json())
      .then(json => setData(json))
      .catch(error => console.error(error));
  }, []);

  return (
    <div>
      {data ? <pre>{JSON.stringify(data, null, 2)}</pre> : 'Loading...'}
    </div>
  );
}

export default App;
```

*XMLHttpRequest vs. Fetch API*

The main difference between XMLHttpRequest and the Fetch API is that XMLHttpRequest is an older, more established API that’s been around since the early days of the web. Fetch API is a more modern API that was introduced in modern browsers to provide a simpler and more flexible way to make HTTP requests.

Here are some of the key differences between XMLHttpRequest and the Fetch API:

* Simpler syntax: Fetch API uses a more concise and intuitive syntax that is easier to read and write. With Fetch API, you can make a request and handle the response using a single function call, while with XMLHttpRequest, you need to create an instance of the XMLHttpRequest object, set properties and register event listeners.
* Better error handling: Fetch API provides a more straightforward and automatic error handling mechanism using promises, which makes it easier to write robust and maintainable code. With XMLHttpRequest, error handling requires the use of callbacks and manual error checking, which can make the code more complex and harder to maintain.
*Automatic type conversion: Fetch API provides automatic type conversion for request and response data, making it easier to work with things like JSON data, for example. With XMLHttpRequest, we must parse the response data manually, which can be error-prone and time-consuming.

Fetch API offers several advantages over XMLHttpRequest. Despite XMLHttpRequest’s reliability and wide usage, Fetch API has a more modern and user-friendly interface for making HTTP requests and handling the responses.

3. **AXIOS**
Axios is a popular JavaScript library for making HTTP requests, and it works great with React. Axios makes it easy to send asynchronous HTTP requests to REST endpoints and perform CRUD operations (create, read, update and delete), as well as handle the responses.

To use Axios in your React application you first need to install it. You can install Axios by running the following command in your terminal:

```npm install axios```

Then, you’ll need to import Axios into your React component to use it, like this:

```react
import React, { useState, useEffect } from 'react';
import axios from 'axios';

function App() {
  const [posts, setPosts] = useState([]);

  useEffect(() => {
    axios.get('https://jsonplaceholder.typicode.com/posts')
      .then(response => {
        setPosts(response.data);
      })
      .catch(error => {
        console.error(error);
      });
  }, []);

  return (
    <ul>
      {posts.map(post => (
        <li key={post.id}>{post.title}</li>
      ))}
    </ul>
  );
}

export default App;
``` 

*Fetch API vs. Axios*

While both Fetch API and Axios are viable options for making HTTP requests in a React application, Axios offers a more feature-rich and user-friendly API that makes it easier to work with.

There are several advantages of Axios over the native fetch API:

* Automatic transformation of data: Axios automatically transforms the response data into a JSON object, which makes it easier to work with. With fetch, you need to parse the response data using the json() method.
* Handling errors: Axios provides a simple way to handle errors, by using the catch method on the returned promise. With fetch, you need to check the status of the response to determine if there was an error or not.
* Support for older browsers: Axios has better support for older browsers compared to fetch, as it includes a polyfill for older browsers that don’t support fetch.
* Abort requests: Axios allows you to cancel a request by using the CancelToken feature. With fetch, you can’t cancel a request once it has started.
* Better testing: Axios provides a simple and intuitive interface that makes it easier to write tests for your code that makes HTTP requests. With fetch, it can be more difficult to mock the fetch function and test your code.
* Improved functionality: Axios has additional functionality not available in fetch, such as the ability to make GET and POST requests with a single line of code, as well as the ability to make requests with a specified timeout.

## Useful Links

* [API Request in ReactJS With Axios and Fetch](https://www.youtube.com/watch?v=rpg1jOvGCtQ&ab_channel=PedroTech)
### [Next part. Handling data from server. Tips ](/Lesson-4/Data-Handling/)