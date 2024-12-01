# Getting started with redux toolkit 
## use the documentation for reference : https://redux-toolkit.js.org/introduction/getting-started
# Installation
### 1 first setup the react vite project 
```
npm create vite@latest
```
## 2 Create a React Redux App
#### after installation of react vite use these to install redux tolkit 
```
npm install @reduxjs/toolkit
```
```
npm install react-redux
```
## 3 lets create a Store 
###imppppppp  Go to src file and craete a (Redux) folder and Inside Redux create a file name as (store.js)
## Now go to Store.js insert below code and can atke a reference : https://redux-toolkit.js.org/tutorials/quick-start
```
import { configureStore } from '@reduxjs/toolkit'

export const store = configureStore({
  reducer: {},
})
```


