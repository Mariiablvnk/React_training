# Homework-1

## Introduction

By the end of this course you will create your own completely responsive Weather app using React tools and API.

## Task
### Step 1
Set up React project using the below command in VSCode IDE.

```npx create-react-app <<name_of_your_project>>``

### Step 1
Navigate to the newly created project folder by executing the below command.

### Step 3 
As we are using various packages for the project, we need to install them. Use the below command to install all the packages that will be specified in package.json file. You can install any useful packages for your project which affect the style or API work. You can see the example below.

```npm install axios react-loader-spinner @fortawesome/react-fontawesome @fortawesome/free-solid-svg-icons```

### Step 4
Check created files and folder structure. Pay your attention on App.jsx and App.css. All the logic that is been used in the application is programmatically coded in App.jsx. From this file, all the buttons, cards, and icons are been rendered in the web browser. App.css file consists of all the styling code, whether it is h1 tag styling or background styling. All the look and feel of the application are specified in this styling file.

### Step 5
Remove unnececary code from App.jsx. Import  installed packages and create the main app component  that returns the main layout of your app. You can also include simple function of date / time creation and add it to your component.  Try to style simple layout and render it. Date function can be rendered using curly braces. You can see the example below.

```react
import React, { useState } from 'react'; 
import axios from 'axios'; 
import './App.css'; 
// continue import...
  
function WeatherApp() { 
  
    const date = () => {
        return new Date()
    } 
  
    return ( 
        <div className="App"> 
            <h1> 
                My Weather App 
            </h1> 
            <div className="search-bar"> 
                <input 
                    type="text"
                    className="city-search"
                    placeholder="Enter City Name.."
                /> 
            </div> 
                <div className="date"> 
                    <span>{date()}</span> 
                </div> 
        </div> 
    ); 
} 
  
export default GfGWeatherApp;
```
**Note:** Don't copy the code, be creative! 
