# A Beginner's Guide to Using React Hook Form

React Hook Form (RHF) is a popular library for handling forms in React. It provides a simple, performant, and flexible solution for managing forms, making it a favorite among developers. In this guide, we'll walk through setting up a React project, installing React Hook Form, and using its features.
# 1. Getting Started: Project Setup
Before diving into React Hook Form, you need a React project set up. Follow these steps:
```
npm create vite@latest
```
# 2 Install react hook form 
```
npm install react-hook-form
```
# Lets use this 
### 3 now first we use below code inside the function where we use this ho0k form to use form 
```
const { register, handleSubmit, formState: { errors } } = useForm();
```
### Now Import this inside this file 
```
import { useForm } from 'react-hook-form';
```
### now your file looks like this 
like this 
```
import React from 'react';
import { useForm } from 'react-hook-form';

function App() {
  const { register, handleSubmit, formState: { errors } } = useForm();

  
  return (
    
      <div>
       
      </div>
  
  );
}

export default App;
```
### Now register our all input area with form 
```
<div>
      <label>First Name</label>
        <input {...register("firstName")} />
      </div>
      <div>
        <label>Middle Name</label>
        <input {...register("middleName")} />
      </div>
      <div>
        <label>Last Name</label>
        <input {...register("lastName")} />
      </div>
      <input type="submit" />
```
### now use handleSubmit to to send pr print our data
```
<form onSubmit={handleSubmit(onSubmit)}>
      <div>
        <label>First Name</label>
        <input {...register("firstName")} />
      </div>
      <div>
        <label>Middle Name</label>
        <input {...register("middleName")} />
      </div>
      <div>
        <label>Last Name</label>
        <input {...register("lastName")} />
      </div>
      <input type="submit" />
    </form>
```
### Now overall code lokks like this
```
import React from 'react';
import { useForm } from 'react-hook-form';

function App() {
  const { register, handleSubmit, formState: { errors } } = useForm();

  // The `onSubmit` function receives the form data as a parameter
  function onSubmit(data) {
    console.log("Submitting the form: ", data);
  }

  return (
    <form onSubmit={handleSubmit(onSubmit)}>
      <div>
        <label>First Name</label>
        <input {...register("firstName")} />
      </div>
      <div>
        <label>Middle Name</label>
        <input {...register("middleName")} />
      </div>
      <div>
        <label>Last Name</label>
        <input {...register("lastName")} />
      </div>
      <input type="submit" />
    </form>
  );
}

export default App;

```
#### Now when you see you console you will find your  entered data that you enter in form input
