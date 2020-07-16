---
title:  "Node Email Code Confirmation"
date: "2020-05-06"
description: Making email confirmation with NodeJS # Add post description (optional)
img: ./img1.png # Add image post (optional)
tags: [NodeJS, Email Confirmation] # add tag
---
This method is commonly used by some websites like **Twitter**, **Github**, **Colors** and others.This method is used for verifying email addresses for authentication.  

## Steps and Setup

1. Create a new folder _node-email-code-verification_
2. Open the folder in terminal  
3. Create a _server.js_ file
4. Create a _mail.js_ file for sending email
5. Create a _user.js_file for storing some values like **email password**, etc  
6. Create an _index.html_ file which holds the main content where user inputs their email for confirmation  
7. Create a _confirm.html_ file where user input their confirmation code gotten from the  email message  
8. Create a _success.html_ file which will be rendered if the confirmation is  successfull  
9. Initialize a new project  by running  ```npm init  -y```
10. Install the  required dependencies by running  ```npm i --save express nodemailer```

### Setting Up the mailer  (_mail.js_)  

create a  new  const that holds a variable to your  mail function which will be exported  

```javascript
const nodemailer = require('nodemailer');

const user = require('./user')

const mail = (email, message) => {
    console.log('Mailing...............');
    var transporter = nodemailer.createTransport({
        service: 'gmail',
        auth: {
            user: user.mail,
            pass: user.auth
        }
    });

    var mailOptions = {
        from: user.mail,
        to: email,
        subject: 'EMAIL CONFIRMATION',
        text: `Confirmation Pins is ${message}`
    };

    transporter.sendMail(mailOptions, function (error, info) {
        if (error) {
            console.log(error);
        } else {
            console.log('Email sent: ' + info.response);
        }
    });
}

module.exports = mail;
```

After the mail.js  setup successfully, you can close it and set up the configuration file (___user.js___)

```javascript
const user = {
    mail: '',       //gmail account
    auth: ''      //account password
}

module.exports = user;
```

## Server.js setup  

Lets setup our _server.js_ file for the installed dependencies.  
We have to require some dependencies in order for our backend to run because our application is fully backend dependent;

```javascript
const express = require('express');
const path = require('path');

const mail = require('./mail');

const server = express();

server.use(express.static('./public'))
server.use(express.json());
server.use(express.urlencoded({ extended: false }));
```  

We required  some packages  

+ Express: For our backend application  
+ path: To use our static files which are _index.html, confirm.html, and success.html_
+ mail: To use our exported function in _mail.js_  

+ Line 5 allow us to use static files which may comtains all _css_  files and **images**
+ Line 6 and 7 allows us to read  request from the url provided

We now have to render the _index.html_ file for the client in order for him/her to enter their email  address. This is also from the _server.js_

```javascript
server.get('/', (req, res) => {
    res.sendFile(path.join(__dirname, 'index.html'));
})
```

After the _mail.js and user.js_ file is set up successfully, add a form  to your  _index.html_ file  which takes an **input of email**  and makes  a **POST** request to the home route *'/'*
We can now  handle the post request in our backeend  in _server.js_ file

```javascript
let code;
server.post('/', (req, res) => {
    code = Math.floor(Math.random() * 903192)
    res.sendFile(path.join(__dirname, 'confirm.html'));
    mail(req.body.email, code)
})
```  

A  code variable was initialized. When the user makes a post request to the home route, a new code is generated which is now sent to the client's mail with the mail function we imported above;.  

**Thats the End of the Sending Part**  
Now we add  a  form with an input of tel which makes a post request to the **'/confirmEmail'** route to verify the code sent

```javascript
server.post('/confirmEmail', (req, res) => {
    if (req.body.code == code) {
        res.sendFile(path.join(__dirname, 'success.html'))
    } else {
        res.sendFile(path.join(__dirname, 'index.html'))
    }
});
```  

This checks if  the code tested by the user is equal to the code sent, if the  response is true, the _success.html_ page is rendered, if error, the index page is rendered  for the user to start  allover.
**If success, you can add  the user to your registered members in your database and render the success page**  

### Remember  

We've been writing code since but we didn't run it, so we have to  create a port to start our server in our _server.js_ file

```javascript
const port = process.env.PORT || 5500
server.listen(port, () => console.log(`Server started on port ${port}`))
```

#### Start Your  Server  
We can now test our application by runing ```node server.js``` in the terminal we opened


The Whole Code can  be found in my Github Repo [Here](https://github.com/qudusayo/node-email-confirmation)
