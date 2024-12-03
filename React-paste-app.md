# Getting started our Project 
## 1 -> setup react vite + Tailwind 
### Open terminal ans paste
## (i)-> Install react Vite (let Project name- React_paste-app)
```
npm create vite@latest
```
###  Now go inside the folder 
```
 cd React_paste-app
 npm install
```
## (ii)-> Install Tailwind Css
```
npm install -D tailwindcss postcss autoprefixer
npx tailwindcss init -p
```
### Configure your template paths
 Add the paths to all of your template files in your (tailwind.config.js) file.
```
/** @type {import('tailwindcss').Config} */
export default {
  content: [
    "./index.html",
    "./src/**/*.{js,ts,jsx,tsx}",
  ],
  theme: {
    extend: {},
  },
  plugins: [],
}
```
### Add the Tailwind directives to your CSS
 Add the @tailwind directives for each of Tailwind’s layers to your ./src/index.css file.
 ```
@tailwind base;
@tailwind components;
@tailwind utilities;
```
## 3->Installing react routing because we will also use this in our project 
```
npm install react-router-dom
```
## 4-> Installing Redux Toolkit because we will also use this to create feature like copy, paste ,delete etc 
```
npm install @reduxjs/toolkit
npm install react-redux
```
## 5- Now run this project 
```
npm run dev
```
## 5- Now See all the dependencies here 
![Screenshot 2024-12-03 181136](https://github.com/user-attachments/assets/dbb58649-c14c-44c7-8212-5f89b11e7095)

