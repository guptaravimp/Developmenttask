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
# Add Slice Reducers to the Store
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




