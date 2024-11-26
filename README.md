
# React Router for navigation between different pages.

This project is a basic React web application that demonstrates the use of React Router for navigation between different pages. It includes multiple components, routing, dynamic parameters, and state handling through navigation. This documentation will guide you through the installation and setup process, the functionality of each component, and how the entire application works.

# 1. Project Setup and Installation
Before starting the development, ensure that you have the following tools installed:

Node.js (https://nodejs.org) – JavaScript runtime for building and running your React app.
npm (Node Package Manager) – To manage dependencies and packages.


## Run in terminal 

To start this project run

```bash
npm create vite@latest

```
# Step 2: Install Required Dependencies

```bash
npm install react-router-dom
```
# 2. Project Structure  
images here 

## Explanation of Key Files and Directories:
public/: Contains the static HTML file (index.html) where the React app is mounted.

1 : "src/: This is where all the JavaScript and JSX files reside. It contains the React components and the main application logic.

2 components/: Contains the individual components like Home, About, Navbar, etc.

3 App.jsx: Main component that renders the application and handles routing.

4 index.css: The global styles for the app.

5 main.jsx: The entry point for the React application where the root element is rendered.
#  3. Application Components Explanation
## Main Files:
### 1 main.jsx – Entry point of the React application  jsx
```bash
import { StrictMode } from 'react';
import { createRoot } from 'react-dom/client';
import './index.css';
import App from './App.jsx';

createRoot(document.getElementById('root')).render(
  <StrictMode>
    <App />
  </StrictMode>
);


```
Purpose: This file initializes the React app, connects the App component to the DOM, and ensures the app runs in strict mode for better development practices.
### 2 App.jsx – Main component with routes
```
import React from 'react';
import { BrowserRouter, RouterProvider, createBrowserRouter } from 'react-router-dom';
import About from './components/About';
import Home from './components/Home';
import Dashboard from './components/Dashboard';
import Navbar from './components/Navbar';
import ParamComp from './components/ParamComp';
import Courses from './components/Courses';
import Mocktest from './components/Mocktest';
import Reports from './components/Reports';

// Setting up the routing configuration using createBrowserRouter
const router = createBrowserRouter([
  {
    path: '/',
    element: <div><Navbar/><Home/></div>  // Home page route
  },
  {
    path: '/about',
    element: <div><Navbar/><About/></div> // About page route
  },
  {
    path: '/dashboard',
    element: <div><Navbar/><Dashboard/></div>, // Dashboard route with nested routes
    children: [
      { path: 'courses', element: <Courses /> }, // Nested route for courses
      { path: 'mock-test', element: <Mocktest /> }, // Nested route for mock tests
      { path: 'reports', element: <Reports /> } // Nested route for reports
    ]
  },
  {
    path: '/student/:id',
    element: <div><Navbar/><ParamComp /></div> // Dynamic route for student with parameter `id`
  }
]);

// Main App component that renders the RouterProvider which provides the router to the application
function App() {
  return (
    <div>
      <RouterProvider router={router} /> {/* Rendering the RouterProvider with defined routes */}
    </div>
  );
}

export default App;

```
Why Use: This file sets up routing using createBrowserRouter from react-router-dom. The RouterProvider is used to provide the routing configuration to the app. Each route points to different components, and the dashboard contains nested routes for additional content like courses, mock tests, and reports. The :id in the student/:id route is a dynamic parameter that changes based on the URL.
### 3 Navbar.jsx – Navigation Bar Component jsx
```
import React from 'react';
import { NavLink } from 'react-router-dom';
import './Navbar.css';

function Navbar() {
  return (
    <div>
      <ul>
        <li><NavLink to="/" activeClassName="active-link">Home</NavLink></li>
        <li><NavLink to="/about">About</NavLink></li>
        <li><NavLink to="/dashboard">Dashboard</NavLink></li>
      </ul>
    </div>
  );
}

export default Navbar;

```
Purpose: The Navbar component contains navigation links (NavLink) that allow users to navigate to different routes of the app. The NavLink helps to style the active link dynamically
### 4 Home.jsx – Home Page Component jsx
```
import React from 'react';
import { useNavigate } from 'react-router-dom';

function Home() {
  const navigate = useNavigate();

  function handleclick() {
    navigate('/about');
  }

  return (
    <div>
      <button onClick={handleclick}>Move to about Pages</button>
      Home Page
    </div>
  );
}

export default Home;

```
Purpose: The Home component contains a button that uses useNavigate to navigate to the /about route.
### 5 About.jsx – About Page Component
```
import React from 'react';
import { useNavigate } from 'react-router-dom';

function About() {
  const navigate = useNavigate();

  function handleclick() {
    navigate('/dashboard');
  }

  return (
    <div>
      <button onClick={handleclick}>Move to Dashboard</button>
      About Page
    </div>
  );
}

export default About;
```

Purpose: The About component contains a button to navigate to the /dashboard route when clicked.
### 6 Dashboard.jsx – Dashboard Page with Nested Routes
```
import React from 'react';
import { Outlet } from 'react-router-dom';

function Dashboard() {
  return (
    <div>
      Dashboard Page
      <Outlet />
    </div>
  );
}

export default Dashboard;

```
Purpose: The Dashboard component serves as a container for nested routes. The Outlet component renders the nested route content, such as Courses, Mocktest, and Reports.
Other Components (Courses.jsx, Mocktest.jsx, Reports.jsx, ParamComp.jsx) – Each component represents a page that will be displayed when its corresponding route is accessed.
### 9. Conclusion
This React app demonstrates the use of react-router-dom for handling routing and navigation between different pages. 
The following key points were used:

BrowserRouter: Used to enable client-side routing.

NavLink: Used for navigation with automatic styling of the active link.

useNavigate: Used for programmatic navigation, enabling dynamic transitions between pages.

Outlet: Renders nested routes inside a parent component, useful for layouts like dashboards.

##  Packages Used
a. react

React is the core library that powers the UI.

b. react-dom

Provides DOM-specific methods for rendering React components.

Why?
 React is a library for building UIs, but react-dom connects it to the DOM (web browser).
c. react-router-dom

Used for routing and navigation in React applications.

Features Used:

BrowserRouter: Wraps the application and enables navigation between components without page reloads.

createBrowserRouter: Defines the routing configuration for the application.

RouterProvider: Connects the router to the application.


NavLink: Used for navigation links with active styling support.

useNavigate: Enables programmatic navigation.

useParams: Accesses URL parameters.

Outlet: Renders nested routes.

## 4. Components Explanation

### a. main.jsx

Purpose: The entry point of the app.
What it Does:

Wraps the app in StrictMode, which highlights potential issues.
Uses createRoot to render the application into the DOM.
Why Use: Ensures the app starts correctly and optimally renders React components.

### b. App.jsx

Purpose: Centralized routing configuration.
What it Does:

Defines all application routes using createBrowserRouter.
Sets up parent-child routes (e.g., Dashboard and its nested routes).
Passes the router configuration to the app via RouterProvider.
Why Use: It organizes the app's navigation logic in a single place for easy scalability.

#### c. Navbar.jsx

Purpose: Provides navigation links to different pages.
What it Does:

Uses NavLink to highlight the active route.
Adds styling to active links with the active-link class.
Why Use: A reusable navigation bar makes navigating between pages intuitive for users.

### d. Home.jsx and About.jsx

Purpose: Render specific content for the "Home" and "About" pages.
What it Does:

Each component has a button that navigates to a different page using useNavigate.
Why Use: useNavigate provides an easy way to trigger navigation programmatically.

### e. Dashboard.jsx

Purpose: A parent component for nested routes like Courses, Mocktest, and Reports.

What it Does:

Uses Outlet to render child routes.
Why Use: This setup supports nested routing, enabling complex layouts like dashboards.

### f. Courses.jsx, Mocktest.jsx, Reports.jsx

Purpose: Render content for specific sections of the dashboard.
What it Does:

Each component renders a simple UI for its section.
Why Use: Modularizes the app for better code organization and reusability.
#### g.ParamComp.jsx
 

Purpose: Handles dynamic routing for the /student/:id route.
What it Does:

Uses useParams to extract the id parameter from the URL.
Displays the dynamic parameter on the page.
Why Use: Dynamic routing is essential for pages like profiles, where the content depends on the URL.

## 5. Key Concepts Used

#### a. Routing

Allows navigation between components without reloading the page.
Nested routes (Outlet) make it possible to load sub-content within a parent route.

#### b. useNavigate

Enables navigation based on user actions, like button clicks.
Example: Navigating from Home to About with navigate('/about').

#### c. useParams

Extracts parameters from the URL for dynamic content.
Example: Displaying a student's details based on their ID in /student/:id.
#### d. NavLink

Creates navigation links with active styling for the current route.

#### e. Outlet

Placeholder for rendering child routes in nested layouts like dashboards.

#### 6. Styling
Navbar.css: Styles the NavLink components, especially for the active link state (active-link class).

## 7. Benefits of this Setup
### Scalability:


Easily add more pages or nested routes without restructuring the app.

#### Modularity:


Each component is self-contained, making it reusable and maintainable.
Dynamic Routing:


Supports pages with content dependent on URL parameters (e.g., student/:id).

### User Experience:


No page reloads; fast navigation between pages.







