# Getting started with redux toolkit 
## use the documentation for reference : https://redux-toolkit.js.org/introduction/getting-started
# Installation
### 1 first setup the react vite project 
```
npm create vite@latest
```
# 2 Create a React Redux App
#### after installation of react vite use these to install redux tolkit 
```
npm install @reduxjs/toolkit
```
```
npm install react-redux
```
# 3 lets create a Store 
##  imppppppp  Go to src file and craete a (Redux) folder and Inside Redux create a file name as (store.js)
![Screenshot 2024-12-01 165716](https://github.com/user-attachments/assets/e170f0ea-12bd-4bf7-b4fd-2d3e77362431)
### Now go to Store.js insert below code and can atke a reference : https://redux-toolkit.js.org/tutorials/quick-start
```
import { configureStore } from '@reduxjs/toolkit'

export const store = configureStore({
  reducer: {},
})
```
# 3 let rapping our app file inside store provider 
### Go to main.jsx  and import provider and store 
```
import { store } from './app/store'
import { Provider } from 'react-redux'
```
###  and wrap the app inside Provider and Store 
####  Why we do this ?
because we want that including app component and every file can access the state defined inside store 

matlab sidhi si baat ye hai ki sabhi state jo bhi hai store ke ander usko sabhi components access kar paye esiliye ham aisa kar rahe hai 

IMPOOOOOOO- Ham kah sakte hai ki ham ye esiliye use kar rahe hai takki store ke ander jo kuch bhi hai usse entire application use kar paye bas esiliye matlab ham sabhi state ko globally define kar rahe hai samjhe 
```
   <Provider store={store}>
    <App />
  </Provider>
```
Complete Code of main folder  Looks Like this 
```
import { StrictMode } from 'react'
import { createRoot } from 'react-dom/client'
import './index.css'
import App from './App.jsx'
import { store } from './app/store'
import { Provider } from 'react-redux'
createRoot(document.getElementById('root')).render(
  <StrictMode>
   <Provider store={store}>
    <App />
  </Provider>
  </StrictMode>,
)

```
##  Impo -> Path ko change karna mat bhulna ki store kaha pada hai jaise ki neeche dekho 
```
import { store } from './Redux/store.js'
```
# 4 Now creating slice 
#### again Bhai documentation bhi dekh lo : https://redux-toolkit.js.org/tutorials/quick-start#create-a-redux-state-slice
##### Now Go to src file and create a Folder name as (features) and uske ander folder create karo let (Counter) fearture and inside folder let createb (CounterSlice.jsx)
####### screenshot
![Screenshot 2024-12-01 165732](https://github.com/user-attachments/assets/611590e2-a7a7-4120-9a79-b0e403838d15)
## Now go inside slice and import createslice 
```
import { createSlice } from '@reduxjs/toolkit'
```
# Slice-> it conatin inistail star  and reducer function  like 
### creatig slice of increment and devrement state look like this 
```
const initialState = {
  value: 0,
}

export const counterSlice = createSlice({
  name: 'counter',
  initialState,
  reducers: {
    increment: (state) => {
      // Redux Toolkit allows us to write "mutating" logic in reducers. It
      // doesn't actually mutate the state because it uses the Immer library,
      // which detects changes to a "draft state" and produces a brand new
      // immutable state based off those changes
      state.value += 1
    },
    decrement: (state) => {
      state.value -= 1
    },
    incrementByAmount: (state, action) => {
      state.value += action.payload
    },
  },
})

```
### imppp- increment,decrement,incrementByAmount all are the action 
## Now export all action from counterSlice and export reducer function from counterSlice.jsx by below code 
```
export const { increment, decrement, incrementByAmount } = counterSlice.actions

export default counterSlice.reducer
```
## Now complete Code of counterSlice.jsx looks like this 
```
import { createSlice } from '@reduxjs/toolkit'

const initialState = {
  value: 0,
}

export const counterSlice = createSlice({
  name: 'counter',
  initialState,
  reducers: {
    increment: (state) => {
      // Redux Toolkit allows us to write "mutating" logic in reducers. It
      // doesn't actually mutate the state because it uses the Immer library,
      // which detects changes to a "draft state" and produces a brand new
      // immutable state based off those changes
      state.value += 1
    },
    decrement: (state) => {
      state.value -= 1
    },
    incrementByAmount: (state, action) => {
      state.value += action.payload
    },
  },
})

// Action creators are generated for each case reducer function
export const { increment, decrement, incrementByAmount } = counterSlice.actions

export default counterSlice.reducer
```
# 5 Add Slice Reducers to the Store
## Now Going to register our slice to store 
### Now go to store.jsx and import below code 
```
import { counterReducer } from '../features/counter/counterSLice'
```
### and add this to register 
```
 reducer: {
    counter:counterReducer
  },
```
Full code of Store.jsx is 
```
import { configureStore } from '@reduxjs/toolkit'
import { counterReducer } from '../features/counter/counterSLice'
export const store = configureStore({
  reducer: {
    counter:counterReducer
  },
})
```
# 6->Now let create a ui and see that how it work 
## Go to App.jsx 
#### agar store me se koi data ko nikalna chahata hu ya kisis  state km access karna chataa hu then we use -> (useSelector) Hook like this 
let we access the initail value of counter 

impppppppp-> that will access the value inside the state name as( counter) and inside this we access the (value )
```
  const count=useSelector((state)=>state.counter.value)

```
### Now if want to do action then use dispatch 
let use dispatch method inside app.jsx
```
const dispatch=useDispatch()
```
##### Now let we want to dispatch the increment reducer then use 
```
dispatch(increment())
```

## Complete code look like this
```
import React from 'react';
import {useSelector,useDispatch} from 'react-redux'
import './App.css'
import { decrement, increment } from './features/counter/counterSlice';
function App() {
  const count=useSelector((state)=>state.
  counter.value)
  const dispatch=useDispatch()
  function handleDecrementClick(){
      dispatch(increment())
  }
  function handleIncrementCLick(){
      dispatch(decrement())
  }
  return (
    <div className='container'>
        <button onClick={handleIncrementCLick}>+</button>
         <p>Count:{count}</p>
        <button onClick={handleDecrementClick}>-</button>
    </div>
  );
}

export default App;

```

# Now check the ui and see the all functiona is working good 

#  7->important-> let we create a action to reset the count 
   so go to first app.jsx create a button of reset and use handler to reset like this 
```
<button onClick={handleresetclick}>reset</button>
```
   #### and let create a action meand dispatch but before dispatch we have to create a reducer function of rest logic so go to (slice) file and add below code inside reducer 
```
resetcount:(state)=>{
      state.value=0;
    },
```
   #### Now add this inside export 
```
export const { increment, decrement,
     incrementByAmount ,resetcount} = counterSlice.actions;
```
   #### Now go to App.jsx and dispatch this action and import this 
```
import { decrement, increment, resetcount } from './features/counter/counterSlice';

```
   ### Now dispatch this inside function
```
function handleresetclick(){
    dispatch(resetcount())
  }
```
#  Now see the complete code of both the file 
   ## App.jsx
```
import React from 'react';
import {useSelector,useDispatch} from 'react-redux'
import './App.css'
import { decrement, increment, resetcount } from './features/counter/counterSlice';
function App() {
  const count=useSelector((state)=>state.
  counter.value)
  const dispatch=useDispatch()
  function handleDecrementClick(){
      dispatch(increment())
  }
  function handleIncrementCLick(){
      dispatch(decrement())
  }
  function handleresetclick(){
    dispatch(resetcount())
  }
  return (
    <div className='container'>
        <button onClick={handleIncrementCLick}>+</button>
        <p>Count:{count}</p>
        <button onClick={handleDecrementClick}>-</button>
        <button onClick={handleresetclick}>reset</button>
    </div>
  );
}

export default App;

```
   ## counterSlice.jsx
```
import { createSlice } from '@reduxjs/toolkit';

const initialState = {
  value: 0,
};

export const counterSlice = createSlice({
  name: 'counter',
  initialState,
  reducers: {
    increment: (state) => {
      // Redux Toolkit allows us to write "mutating" logic in reducers. It
      // doesn't actually mutate the state because it uses the Immer library,
      // which detects changes to a "draft state" and produces a brand new
      // immutable state based off those changes.
      state.value += 1;
    },
    decrement: (state) => {
      state.value -= 1;
    },
    incrementByAmount: (state, action) => {
      state.value += action.payload;
    },
    resetcount:(state)=>{
      state.value=0;
    },
  },
});

// Action creators are generated for each case reducer function.
export const { increment, decrement,
     incrementByAmount ,resetcount} = counterSlice.actions;

export default counterSlice.reducer;

```


Same as we can implement actopn and dispatch this to see the refelect on ui 

 Disclaimer : for enlish  see this reference chat : https://chatgpt.com/c/674c4c29-0d14-800d-b128-0a62e702a749



