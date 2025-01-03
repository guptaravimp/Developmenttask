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
# 3 now first we use below code inside the function where we use this ho0k form to use form 
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
# 4 lets use validation that this input field is required 
### a.required field 
```
    <input {...register("lastName", { required: true })} />
```
### b. min length and max length input 
```
 <input {...register("firstName", { required: true, maxLength: 20 })} />
```

Now for all type check the documentation :   https://www.react-hook-form.com/get-started

# extra validation 
## lets use some code so that any input take input greater than 3 character 
```
<div>
        <label>First Name</label>
        <input {...register("firstName",{
          required:true,
          minLength:{value:3,message:'min length at least 3'},
          maxLength:{value:6,message:'max length at most 10 '}
        })} />
        {errors.firstName && <p>{errors.firstName.message}</p>}
         {/* ///register with this anme firstname */}
      </div>
```
##### it will show message below input that min length at least 3 when input is <3 character 
## 4 Now applying css on error message 
```
<div>
        <label>First Name</label>
        <input 
        className={errors.firstName?'input-error':""}
        {...register("firstName",{
          required:true,
          minLength:{value:3,message:'min length at least 3'},
          maxLength:{value:6,message:'max length at most 10 '}
        })} />
        {errors.firstName && <p className='error-msg'>{errors.firstName.message}</p>}
         {/* ///register with this anme firstname */}
      </div>
```
# vvvvvvvvvimportant login 
### if we want to submit form once and jab tak submit nahi ho jaye button ko disable karna hai to use (issubmitting) in form state and disable button o is submitting 
```
const { register, handleSubmit, formState: { errors,isSubmitting } } = useForm();
```
```
<input 
        type="submit" 
        disabled={isSubmitting} 
        value={isSubmitting ? "Submitting..." : "Submit"} 
      />
```
#  Now our full code 
```
import React from 'react';
import { useForm } from 'react-hook-form';
import './App.css';

function App() {
  const { register, handleSubmit, formState: { errors, isSubmitting } } = useForm();

  async function onSubmit(data) {
    // Simulate an API call
    await new Promise((resolve) => setTimeout(resolve, 5000));
    console.log("Submitting the form: ", data);
  }

  return (
    <form onSubmit={handleSubmit(onSubmit)}>
      <div>
        <label>First Name</label>
        <input 
          className={errors.firstName ? 'input-error' : ""}
          {...register("firstName", {
            required: "First name is required",
            minLength: { value: 3, message: 'Min length at least 3' },
            maxLength: { value: 6, message: 'Max length at most 6' }
          })} 
        />
        {errors.firstName && <p className='error-msg'>{errors.firstName.message}</p>}
      </div>
      <div>
        <label>Middle Name</label>
        <input {...register('middleName')} />
      </div>
      <div>
        <label>Last Name</label>
        <input 
          {...register("lastName", { required: "Last name is required" })} 
        />
        {errors.lastName && <p className='error-msg'>{errors.lastName.message}</p>}
      </div>
      <input 
        type="submit" 
        disabled={isSubmitting} 
        value={isSubmitting ? "Submitting..." : "Submit"} 
      />
    </form>
  );
}

export default App;

```
