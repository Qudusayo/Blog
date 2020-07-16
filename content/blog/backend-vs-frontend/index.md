---
title: "Backend versus Frontend"
date: 2020-06-08
description: Simple explanation on backend and frontend development # Add post description (optional)
img: ./img1.png # Add image post (optional)
tags: [Backend, Frontend, Fullstack, Web Development] # add tag
---
Is Backend really dependent on frontend or frontend really dependent on backend? This is a question most newbie to backend find confusing. I will be explaining both concepts based on my knowledge of both using simple explanation with a login form

## What is Frontend ?

Frontend is the visible part of a website which users see upon visting a site. As a developer, for example, when you inspect a page or view the source code of a page, only the code of the frontend will & can be shown, but the backend is hidden.

## What is Backend ?

Backend is the invisible part of a website which a user cannot see upon visting a site, it cannot be inspected in the browser when a website is in production ( I mean working website). The backend handles the database too.

## Example with a Login Page

**The Frontend**: When a user visits a site to login, the frontend part is shown to the user just to enter their username and password. When the user clicks login button in order to get access to the site, the information entered is sent to the backend.  

**The Backend**: The Backend receives the information and checks if the username sent is in the database, if found, it then checks if the password sent by the user also matches the password of the same user stored in their database. If true, the backend send some messages to the frontend which also inclusive a message telling the frontend the user information is genuine.  

**The Frontend**: After receiving  yes from the  backend, the user's permission is now granted and taken to the homepage.  

This is how the communication works for pages  like Registration page, Profile page, Cart page and even some sites uses this in all their web pages.

## Why Backend ?

Backend major work is to manage and control database. A major reason for backend is to be able to control site access ,  storing client information and helping (Helping by providing APIs for others on need of some information provided by our backend which is shareable)

## Why Frontend ?

Without Frontend , what will a client see ? Nothing really!!! That's why frontend. But there are types of frontend without backend:  

+ Static: a site which is built to be the same unless the code in it is changed or update like my [100DailyUI](https://100_Daily_UI.netlify.app) challenge preview site.
+ Dynamic: A site which is static, but it's content is dynamic which always change without updating the code. This type of website mostly rely on APIs to work. An example is like my [Covid19-statistic App](https://covid19-statistic.netlify.app) site which only the figure of the covid19 values change.

## Is Frontend required for Backend?

A frontend must be active in order to see the actions of the backend in action, because a non-developer do not know how to code, to handle or send request to the backend and others who can code does not know how the backend is shaped for query. Its best for a backend to have a frontend **except if it's rendering an API**  

## How much Frontend must I know for Backend

The answer to this is dependent on the backend scheme you want to use. **SCHEME ? YES**. I meant by example if you're going to send and receive all your request to the backend through API, then all you need to know is how to use API in frontend. This is common in ReactJS, Angular , even it can be used anyhow.

**<p align="center">FRONTEND + BACKEND = FULLSTACK</p>**
