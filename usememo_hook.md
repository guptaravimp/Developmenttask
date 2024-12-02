# Getting started with usememo hook 
The useMemo hook in React is used to optimize the performance of functional components by memoizing the result of expensive calculations. It ensures that the computation is only performed when one of its dependencies changes, reducing unnecessary re-renders.
# 1 SetUp React Vite Project 
```
npm create vite@latest
```
# 2 See the complete code of usememo Hook
```
import React, { useState, useMemo } from 'react';

function App() {
  const [count, setCount] = useState(0);
const [input,setinput]=useState(0);
  function handleClick() {
    setCount(count + 1);
  }

  function expensiveTask(num) {
    console.log("Inside Expensive Task");
    for (let i = 0; i <= 10000000; i++) {}
    return num * 2;
  }

  // let doubleValue=expensiveTask(input)
  // let usememo hook for momorizxation 
  // imppppppppp->agar aai hui input ki value pahle se ha tousememo return kar deta nhi to function ko call karke calculate karega 
let doubleValue=useMemo(()=>expensiveTask(input),[input]);
  return (
    <div>
      <button onClick={handleClick}>Increment</button>
      <p>Count: {count}</p>
      <input type="number" placeholder='Enter Number'
       value={input} onChange={(e)=>setinput(e.target.value)}/>
      <div>Double: {doubleValue}</div>
    </div>
  );
}

export default App;


```
