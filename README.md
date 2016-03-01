# React Native StyleGuide + Best Practices() {
*A proposed style + best practices for creating React-Native mobile apps used internally at [GuavaPass.com](https://guavapass.com)*

---
This guideline is an extension to the AirBnB style guide for [javascript](https://github.com/airbnb/javascript) and [react](https://github.com/airbnb/javascript/tree/master/react)

![](http://www.blissout.com.sg/wp-content/uploads/2015/10/guava-pass-big-logo.gif) ![](https://goodbits-production.s3.amazonaws.com/uploads/link/thumbnail/2391724/logo_og.png)


## Table of Contents

  1. [Libraries](#libraries)
  1. [Folder Structure](#folders)

## Libraries

 - Use react native libraries where possible, rather than writing custom Java/Objective C/Swift bindings, and if you have to please open source them!
 
- [1.1](#1.1) <a name='1.1'>**Npm Modules**</a> : 

    + `react-redux`   [ View on GitHub](https://github.com/reactjs/react-redux)
    + `relm` [View on GitHub](https://github.com/realm/realm-js)

## Folder Structure

  - To encourage reuse of style between a react app and a react native app I propose keeping the same folder structure as is common with other react-redux apps.
  
This folder structure should reflect something similar to:
```
.
├── index.android.js 
├── index.ios.js
├── package.json
├── android
├── ios
├── node_modules
├── src
   ├── actions
   │   ├── exampleActionsCreators.js
   ├── components
   │   └── ExampleComponent
   │       │   └── ExampleComponent.android.jsx
   │       │   └── ExampleComponent.ios.jsx
   ├── constants
   │   ├── exampleConstants.js
   ├── containers
   │   └── ExampleContainer
   │           └── ExampleContainer.android.jsx
   │           └── ExampleContainer.ios.jsx
   ├── layout
   │   └── layout.android.jsx
   │   └── layout.ios.jsx
   ├── reducers
   │   ├── index.js
   ├── routes
   │   └── routes.jsx
   └── store
       └── store.js
```

This structure should look fairly familiar to anyone with experience developing an app using redux, but lets quickly cover the conventions behind the folder structure and the conventions used above.

## ./actions
 ActionCreators are responsible for converting your application’s data to a format of some remote API and/or updating the state of the store. It is responsible for both making the requests and handling responses.

Actions are simply stored in this folder usually related to some subset of the store, the convention it to name them <noun>-<verb>, eg Lesson-Create, Booking-Confirm. The idea behind this is that you want to categorize then by  object type, rather than the action type.

## ./containers
First step read [Dan Abramov's post about the different type of components](https://medium.com/@dan_abramov/smart-and-dumb-components-7ca2f9a7c7d0#.n7jx61gix)

Containers are simply `Smart Components`. Smart components are components that are concerned with managing the flow of data to other `dumb` child components. They are responsible for connecting with the store to pass the information to children, provide actions and callbacks for children to use.

These containers should be the only components that we reference in our routes

Inside of these containers we should:
- Generate action creators for children
    -  This allows the dumb child components to not be responsible for any logic, and it should simply reference an action passed down from the container
    -  The container is also responsible for handling the suitable manipulation of data and forwarding that on to the appopriate action creator.
-  Should **NOT** contain any rendering of markup, except dump components. This is to seperate the concerns of containers vs components and we should avoid even wrapping our components in `<div></div>` tags
 
