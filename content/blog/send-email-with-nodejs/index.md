---
title:  "Send Email with NodeJS"
date: "2020-06-17"
description: Sending email in Nodejs using nodemailer
img: ./img1.jpeg 
tags: [NodeJS, Email]
---
Sending email in Nodejs requires a module named **Nodemailer**.  
**Nodemailer** is a module for Node.js applications to allow easy as cake email sending  

## Requirements  

Node.js v6.0.0 or newer. That’s it. If you are able to run Node.js version 6 or newer, then you can use Nodemailer. There are no platform or resource specific requirements

## Installation  

The Nodemailer module can be downloaded and installed using npm
> ```npm install nodemailer```  


After you have downloaded the Nodemailer module, you can include the module in any application:  
```js
var nodemailer = require('nodemailer');
```  

## Sending an Email  

Now you are ready to send emails from your server.  

1. Create a Nodemailer transporter using either [SMTP](https://nodemailer.com/smtp/) or [some other](https://nodemailer.com/transports/) transport mechanism
    ```js
    var transporter = nodemailer.createTransport({
    service: 'gmail',
    auth: {
            user: 'youremail@gmail.com',
            pass: 'yourpassword'
        }
    });
    ```
    If **service: _gmail_**, you need to allow [Less Secure App](https://myaccount.google.com/lesssecureapps) in your gmail account and add 
    ```js
         tls:{
            rejectUnauthorized: false
        }
    ```
    to the transporter options 

2. Set up [message options](https://nodemailer.com/message/) (who sends what to whom)
    ```js
    var mailOptions = {
        from: 'youremail@gmail.com',
        to: 'myfriend@yahoo.com',
        subject: 'Sending Email using Node.js',
        text: 'That was easy!'
    };
    ```

    ### Multiple Receivers
    To send an email to more than one receiver, add them to the "to" property of the mailOptions object, separated by commas:
    ```js
    var mailOptions = {
        from: 'youremail@gmail.com',
        to: 'myfriend@yahoo.com, myotherfriend@yahoo.com',
        subject: 'Sending Email using Node.js',
        text: 'That was easy!'
    }
    ```

    ### Send HTML
    To send HTML formatted text in your email, use the "html" property instead of the "text" property:
    ```js
    var mailOptions = {
        from: 'youremail@gmail.com',
        to: 'myfriend@yahoo.com',
        subject: 'Sending Email using Node.js',
        html: '<h1>Welcome</h1><p>That was easy!</p>'
    }
    ```

3. Deliver the message object using the **sendMail()** method of your previously created transporter
    ```js
    transporter.sendMail(mailOptions, function(error, info){
        if (error) {
            console.log(error);
        } else {
            console.log('Email sent: ' + info.response);
        }
    });
    ```
In Conclusion, 

```js
var nodemailer = require('nodemailer');

var transporter = nodemailer.createTransport({
  service: 'gmail',
  auth: {
    user: 'youremail@gmail.com',
    pass: 'yourpassword'
  },
    tls:{
        rejectUnauthorized: false
    }
});

var mailOptions = {
  from: 'youremail@gmail.com',
  to: 'myfriend@yahoo.com',
  subject: 'Sending Email using Node.js',
  text: 'That was easy!',
  html: '<h1>Welcome</h1><p>That was easy!</p>'
};

transporter.sendMail(mailOptions, function(error, info){
  if (error) {
    console.log(error);
  } else {
    console.log('Email sent: ' + info.response);
  }
});
```

[Here is an In my github with a complete project](https://github.com/Qudusayo/mailqudusayo/blob/463f7dd1d6327ade7953a61c35281afd5d35e1d4/app.js#L30);
