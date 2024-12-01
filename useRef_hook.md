# getting started with useref hook 
The useRef hook in React is used to persist values across renders without causing re-renders when the value changes. It is commonly used to access or interact with DOM elements directly or to keep a mutable variable.
# 1 setup react vite project first 
```
npm create vite@latest
```
# 2 let create a ui to increment the value on every onclick increment 
## go to App.jsx and implemet this to show on ui 
```
import React, { useEffect, useState } from 'react'

function App() {
  const [count,setcount]=useState(0);
  function handleincrement(){
    setcount(count+1);
  }
 

  return (
    <div>
      <button onClick={handleincrement}>increment</button>
      <br />
      <div>count: {count}</div>
    </div>
  )
}

export default App

```
### Now let see that on every click ui is alway re-render or not to check this we use useEffet hook
```
  //it run on every render 
  useEffect(()=>{
  console.log("mai fir se render jho gaya hu")
  })
```

### Here we can see in screenshot that it render always on clicking on increment button 
![Screenshot 2024-12-01 223445](https://github.com/user-attachments/assets/20599b18-edd0-45a5-be6d-9132fbdd8716)

in the screenchot we can see that ui is re-render on every time when we click on button 

Now lwt see that on evvery render it persist their value or not use use a variable val to check it see this 
```
 const [count,setcount]=useState(0);
  let val=0;
  function handleincrement(){
    val=val+1;
    console.log("value is ",val)
    setcount(count+1);
  }
  //it run on every render 
  useEffect(()=>{
  console.log("mai fir se render jho gaya hu")
  })
```

### but after doing this see the screenshot 
![Screenshot 2024-12-01 223718](https://github.com/user-attachments/assets/0d266325-f7b0-4130-8d18-cbc8a129a988)
immmmmmpppp--->in the screenshot we can see that val is constant after incrementing it doesnot persist their value on re-render 

seeeeeimmmpppp=->matlab bhai ye hai ki re-render hne pr pura function fir se chalta hai aur value increment ko persist nahi kar raha hai on re-render to esse solve karne ke liye ham useref ka use karte hai 

vvvvvipm->   so here we use a useRef this create a varaible who persist their value on re-render 
##### Complete cole til;l this 
```
import React, { useEffect, useState } from 'react'

function App() {
  const [count,setcount]=useState(0);
  let val=0;
  
  function handleincrement(){
    val=val+1;
    console.log("value is ",val)
    setcount(count+1);
  }
  //it run on every render 
  useEffect(()=>{
  console.log("mai fir se render jho gaya hu")
  })
  return (
    <div>
      <button onClick={handleincrement}>increment</button>
      <br />
      <div>count: {count}</div>
    </div>
  )
}

export default App

```

# 3 let create a  varaible using useRef()

Here current is method to access the value on variable using (val.current)

```
let val=useRef(0);

  function handleincrement(){
    val.current=val.current+1;
    console.log("value is ",val)
    setcount(count+1);
  }
```
#### Now You can seethe screenshot that it persist their value and increment on earch re render 
see this screenshot
![Screenshot 2024-12-01 224718](https://github.com/user-attachments/assets/7c16605b-a2b8-4e77-b957-c3d08f4e0cd2)

# 4 Now see the 2nd usecase of useref ->
## using useRef we cann access any element directly to change the syle access it update it etc 
### Noe see this 
let create a another button in this project and use a useref to access the firstbutton and change is using second button 
like ....->
```
let btnRef=useRef();
```
```
 <button ref={btnRef} onClick={handleincrement}>button 1</button>
      <br />
      <button onClick={handlecolor}>CHnage color of first button</button>
      <div>count: {count}</div>
```
Now let access the seond button and implement the logic f handlecolor function to change the firstbutton color by accessing it 
```
function handlecolor(){
    btnRef.current.style.backgroundColor="red";
  }
```
# complete code looks like this -> 
```
import React, { useEffect, useRef, useState } from 'react'

function App() {
  const [count,setcount]=useState(0);
  let val=useRef(0);
  let btnRef=useRef();
  function handleincrement(){
    val.current=val.current+1;
    console.log("value is ",val.current)
    setcount(count+1);
  }
  function handlecolor(){
    btnRef.current.style.backgroundColor="red";
  }
  //it run on every render 
  useEffect(()=>{
  console.log("mai fir se render jho gaya hu")
  })
  return (
    <div>
      <button ref={btnRef} onClick={handleincrement}>button 1</button>
      <br />
      <button onClick={handlecolor}>CHnage color of first button</button>
      <div>count: {count}</div>
    </div>
  )
}

export default App

```
# see the ecreenshot 
![Screenshot 2024-12-01 230808](https://github.com/user-attachments/assets/58d7062f-92ef-422d-b5f9-7e94cbf49001)



