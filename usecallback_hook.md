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
# 3 Limitation of React.memo -> it will only work when we send a val like integer string etc but it doesnot work on sending the function in props of childcomponents like 
## let we send a handleclick functionn in childcomponents 
```
<ChildComponents handeclick={handleclick} buttonname="click me"/>
```
## let parse it in child components 
```
<div>
        <button onClick={props.handeclick}>{props.buttonname}</button>
      </div>
```
## Now it will same qa previous problem it re-render on each click button sol here the game come of call back hook 
## 4 we freeze the function that on we working here is -handleclick function we freeze it then their refernce is not change now child component ka React.memo isse naya function nahi samjhega to re-render nahi karega 
so use 
```
  const handleclick=useCallback(()=>{
    setcount(count+1)
  },[])    
```

# but on doing this our increment function is also freeze and always print same value so here we pass count after update in dependency list of function pass (count)
```
 const handleclick=useCallback(()=>{
    setcount(count+1)
  },[])   
```
## Now complete code of App.jsx 
```
import React, { useCallback, useState } from 'react'
import ChildComponents from './components/ChildComponents';

function App() {
  const [count,setcount]=useState(0);
  // function handleclick(){
  //   setcount(count+1)
  // }
   const handleclick=useCallback(()=>{
    setcount(count+1)
  },[count])       
  return (
    <div>
      <div>Count:{count}</div>
      <br />

      <div><button onClick={handleclick}>
        Increment</button></div>
        <br />
        <br />
      <ChildComponents handeclick={handleclick} buttonname="click me"/>
    </div>
  )
}

export default App

```
