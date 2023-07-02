# JS Template File
### Table of Contents
<details open>
<summary><b>(click to expand/hide)</b></summary>
<!-- MarkdownTOC -->
    
1. [NodeJS Template](#node_section)
2. [JQuery Template](#jquery_section)
3. [ReactJS Template](#react_section)

<!-- /MarkdownTOC -->
</details>

<a id="node_section"></a>
## NodeJS Template File

### included libraries : express, body-parser, ejs, lodash, mongoose, dotenv
### include request methods: get, post, listen
---
### Initial project creation
1. create a folder, and switch to the folder directory
    ```bash
      mkdir <folder name>
    ```
    ```bash
      cd <folder name>
    ```
2. create required files (in the folder)
    ```bash
      touch app.js
    ```
    ```bash
      mkdir views
    ```
    ```bash
      cd views
    ```
    ```bash
      touch home.ejs header.ejs footer.ejs
    ```
3. initialize npm and install required npm libraries (in the folder)
    ```bash
      npm init
    ```
    ```bash
      npm i express body-parser ejs lodash mongoose dotenv
    ```
### other useful functions
#### render specific ejs files in nodejs request function
```javascript
res.render("filename");
```
```javascript
res.render("filename", {<var1 in ejs>: <var1 in js>, <var2 in ejs>: <var2 in js>});
```
  - calling variable in ejs
    ```html
    <%= variablename %>
    ```
#### writing function in ejs file (**must use <% and %> to cover every js code**)
```html
<% for(let i=0; i<newListItems.length ; i++){ %>
            <div class="item">
                <input type="checkbox">
                <p>
                    <%= newListItems[i] %>
                </p>
            </div>
        <% } %>
```
#### calling other ejs file to render in current ejs file
- in this case the header.ejs will render before the div element and footer.ejs will render after the div element
```html
<%- include("header") -%>
<div class="box" id="heading">
   <h1>It's <%= listTitle %>!</h1>
</div>
<%- include("footer") -%>
```
#### module.exports
 - import Strings/Objects/Functions
   ```javascript
   let example = require('path/filename.js');
   ```
 - export functions
   ```javascript
   module.exports.<function name> = function() {
    ... code ...
    return variable/object;
   };
   ```
 - export functions in bulk
   ```javascript
   function example1(){
   }
   function example2(){
   }
   module.exports = {
    example1,
    example2
   }
   ```
#### get the value in url
```javascript
app.get("/posts/:postName", function(req, res){
console.log(req.params.postName);
});
```
#### find one of the key-value in a object array
1. some()
    - return type : boolean value
    ```javascript
    if(array.some(item => item.title === req.params.ItemName)){
        console.log("Match Found");
    }
    ```
2. find()
    - return type : object
    ```javascript
    let foundItem = array.find(item => item.title === req.params.ItemName);
    if(foundItem){
        console.log(foundItem.title);
    }
    ```
#### use .env to hide private information(ex. API key)
1. install dotenv package if have bot install already, and create a .env file
   ```bash
      npm i dotenv
   ``` 
   ```bash
      touch .env
   ```
2. Store private information in .env
   ```javascript
     API_KEY = 00000000000
   ```
3. Calling private information in javascript file
   ```javascript
     require("dotenv").config();
   ```
   ```javascript
     let example = process.env.API_KEY;
   ```
#### using https get request
```javascript
    const https = require("https"); //make sure to include library, it is a built-in nodejs library so we don't have to npm install it.
    const exampleAPI_URL = "https://api.exampleapi.com/key?=value";
    https.get(exampleAPI_URL, function(res){
        console.log(res.statusCode); //get the status code
        res.on("data", function(data){
            const weatherData = JSON.parse(data); // JSON.parse will convert the response data from hex format to json format
            console.log(weatherData);
            //JSON.stringify(weatherData); //this will turn weatherData from object to string
        });
    });
```
#### connect to mongo server and call mongo find function
```javascript
async function getInfoDB() {
  let result;
  try {
    await mongoose.connect("mongodb+srv://" + process.env.MONGO_USERNAME + ":" + process.env.MONGO_PS + "@cluster0.6gezmfg.mongodb.net/<db name>", { useNewURLParser: true });
    result = await <collection name>.find({});
    mongoose.connection.close();
  } catch (err) {
    console.error(err);
    mongoose.connection.close();
  }
  return result;
}
```
---

<a id="jquery_section"></a>
## JQuery Template File
### Import jquery libraries in html
- Include jquery cdn libraris
```html
<script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
```
- Include jquery custom js script file
```html
<script src="./<path>/<script file name>.js"></script>
```
### jquery ajax get method
```javascript
function functionName() {
  // Fetch and process data
  $.ajax({
    url: "/<pathname>",
    method: "GET",
    async:false, //disallow concurrent running
    success: function (data) {
      function2Name(data);
    },
    error: function () {
      console.log("An error occurred accessing stock info data");
        function3Name();
    },
    complete: function () {
      function4Name();
    }
  });

  // Fetch and process data
  $.ajax({
    url: "/<pathname2>",
    method: "GET",
    async:false, //disallow concurrent running
    success: function (data) {
      function5Name(data);
    },
    error: function () {
      console.log("An error occurred accessing stock info data");
        function6Name();
    },
    complete: function () {
      function7Name();
    }
  });
}

$(document).ready(function () {
  setTimeout(functionName, 1000); // 1000 means delay for 1 second then call function "function"
});
```
---

<a id="react_section"></a>
## React Template File
### Creating React App
- In bash
    ```bash
      npx create-react-app <app name>
    ```
### Start development server
- In bash located into the react app directory
    ```bash
      cd <app name>
    ```
    ```bash
      npm start
    ```
### Upgrade React App version
- In bash located into the react app directory
    ```bash
      cd <app name>
    ```
    ```bash
      npm install react-scripts@latest
    ```
### React in JS file
#### Import react js file in html
```html
<script src="./src/index.js" type="text/jsx"></script>
```
#### Import libraries in js file
```javascript
import React from 'react';
import ReactDOM from 'react-dom/client';
```
#### Inject code to an element (ex. div/h1/p)
```javascript
import React from 'react';
import ReactDOM from 'react-dom/client';

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(
  <h1>
    Hello World
  </h1>
);

```
#### Calling js variable in an element (ex. div/h1/p)
```javascript
import React from "react";

function Footer() {
  const currentYear = new Date().getFullYear();
  return (
    <footer>
      <p>Copyright ⓒ {currentYear}</p>
    </footer>
  );
}

export default Footer;
```
#### React function with parameter (React props)
```javascript
import React from "react";
import ReactDOM from "react-dom";

function Card(props) {
  return (
    <div>
      <h2>{props.name}</h2>
      <img src={props.img} alt="avatar_img" />
      <p>{props.tel}</p>
      <p>{props.email}</p>
    </div>
  );
}

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(
  <div>
    <h1>My Contacts</h1>
    <Card
      name="Beyonce"
      img="https://blackhistorywall.files.wordpress.com/2010/02/picture-device-independent-bitmap-119.jpg"
      tel="+123 456 789"
      email="b@beyonce.com"
    />
    <Card
      name="Jack Bauer"
      img="https://pbs.twimg.com/profile_images/625247595825246208/X3XLea04_400x400.jpg"
      tel="+7387384587"
      email="jack@nowhere.com"
    />
  </div>,
  document.getElementById("root")
);

```
