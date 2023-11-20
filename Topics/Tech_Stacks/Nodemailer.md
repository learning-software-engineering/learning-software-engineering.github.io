# Nodemailer

## Table of contents
### [Introduction](#introduction-1)
### [Create a Transporter object](#create-a-transporter-object-1)
### [Create a MailOptions Object](#create-a-mailoptions-object-1)
### [Use the Transporter.sendMail method](#use-the-transportersendmail-method-1)

## Introduction

Nodemailer is a Node.js module that allows you to send emails from your server easily. You can use Nodemailer. For example, you can communicate with others or notify yourself via email. As the name suggests, Nodemailer is used in Node.js, so when you want to use Nodemailer to send mail, make sure to use Node.js and have Node.js ready with you.

Before I start explaning how Nodemailer can be used, we have to install and import so we can use it. You can install nodemailer by the below command:

```
npm install nodemailer
```
After you installed Nodemailer, make sure you import nodemailer so you can use it

``` JavaScript
const nodemailer = require('nodemailer');
```

[This link](https://www.freecodecamp.org/news/use-nodemailer-to-send-emails-from-your-node-js-server/) provides a more practical and detailed method of installing the necessary packages, as well as nodemailer examples.

## Create a Transporter object

Now you are ready to use nodemailer! Using nodemailer involves three steps. Here, we explain first step which is creating a transporter object. This step is basically creating an object and setting information about basic information about a mail you are sending, such as the service you are using to send a mail, information about senders, and so on. The example codes are shown below:

``` JavaScript
let transporter = nodemailer.createTransport({
      service: 'gmail',
      auth: {
        user: YOUR_MAIL_ADDRESS,
        pass: YOUR_PASSWORD
      }
    });
```
Here, it uses gmail to send email. Information about the mail address that you want the email to be sent from goes to auth as the code suggested. Note that you usually want to define your mail address and password in different file such as .env so that it is not visible by others.

[This website](https://www.freecodecamp.org/news/use-nodemailer-to-send-emails-from-your-node-js-server/) gives further explanation about credentials. It might be helpful when you are actually implementing and encounter any errors.


## Create a MailOptions Object: 

MailOptions object contains information about the contents of the mail that you want to send. The example code is shown below:

``` JavaScript
let mailOptions = {
      from: YOUR_EMAIL,
      to: WHERE_EMAIL_IS_SENT_TO,
      subject: 'Nodemailer Testing',
      text: 'contents of your mail goes here'
    };
```
 
As the example code above shows, you can define the contents and subject in this object. There are some options for the text such as using HTML to format the text by adding html in mailOption like below:

``` JavaScript
let mailOptions = {
      from: YOUR_EMAIL,
      to: WHERE_EMAIL_IS_SENT_TO,
      subject: 'Nodemailer Testing',
      text: 'contents of your mail goes here'
      html: '<a href="https://google.com" title="Lets go to Google!">'
    };
```

## Use the Transporter.sendMail method

The last step is to use the Transporter.sendMail method. This is simpler than earlier steps. However, there are some things we should aware of which is error handling. It is common that the nodemailer causes errors since there might be a typo in the mail address and so on. Therefore, make sure to check for the error. If there are errors, make sure to hadle them separately. This code below gives you an idea how the error should be handled and how the method is used.

``` JavaScript
transporter.sendMail(mailOptions, function(err, data) {
      if (err) {
        console.log("Error " + err);
      } else {
        console.log("Email sent successfully");
      }
    });
```
This is very common way to handle errors. If specific operations are needed when there is an error, you can edit the code as needed. This data attribute for errors can be used to notify what the error or problem is.

In conclusion, nodemailer is a very simple way to send emails to a user. 

## Useful Links
https://mailtrap.io/blog/sending-emails-with-nodemailer/


https://www.knowledgehut.com/blog/web-development/nodemailer-module-nodejs


These websites have full tutorials from setting up to implementing which can be useful!
