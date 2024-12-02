# Getting started with usecallback Hook 
# 1  Setup react Vite project run in terminal 
```
npm create vite@latest

```
# Noe let see the usecase -1 of usecallback functiomn 
### Let see the first problem - Unnessary re-render of child components like -App.jsx create a chilComponent name as ChildComponent.jsx see complete code 
```
import React, { useState } from 'react'
import ChildComponents from './components/ChildComponents';

function App() {
  const [count,setcount]=useState(0);
  function handleclick(){
   setcount(count+1)
  }
  return (
    <div>
      <div>Count:{count}</div>
      <br />

      <div><button onClick={handleclick}>
        Increment</button></div>
        <br />
        <br />
      <ChildComponents buttonname="click me"/>
    </div>
  )
}

export default App

```
## ChildComponent.jsx
```
import React from 'react'

function ChildComponents() {
    console.log("Child component got re-render again ")
  return (
    <div>
      <button>Click me</button>
    </div>
  )
}

export default ChildComponents

```

## Now Ypu can in image that after each click on incremnet child component render again and again that is unneccessary re-render of chil components 
## Screenshot
![Screenshot 2024-12-02 180412](https://github.com/user-attachments/assets/aef0ab7c-8774-4df4-b56a-cfae7b7889cb)
#  Now to prevent this ans solve this wrap the child components inside React.memo like this 
## Updates ChilcComponent.jsx file 
```
import React from 'react'

const ChildComponents=React.memo(() =>{
    console.log("Child component got re-render again ")
    return (
      <div>
        <button>Click me</button>
      </div>
    )
}
  
  
)


export default ChildComponents

```
## means on warping chilc components inside React.memo our child component will not re-render on same props if the props will change it will re-render again just like meorization algorithms 


