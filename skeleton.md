## Introduction

In the evolving landscape of web development, modern browsers have taken on a significant role in data fetching, handling much of this task directly rather than relying solely on the server. This shift enhances the user experience by reducing the wait time for initial page loads, allowing users to interact with the page sooner. However, while the page structure loads quickly, fetching the actual data—whether blog posts, comments, videos, or other content—can still introduce a delay.

To manage user expectations during this data fetching process, developers often employ visual indicators such as loaders or spinners. A particularly effective and popular approach, adopted by major websites like Facebook and LinkedIn, is the use of skeleton loading screens. These screens display placeholder elements that mimic the layout of the actual content, providing a visual cue that data is on its way.

## Prerequisites

- Basic knowledge of React.
- Familiarity with React Hooks.

## Setting Up the Project

First, we'll create a new React application using the following command:

```bash
npx create-react-app react-skeleton-screens
```

Next, navigate into the newly created project directory:

```bash
cd react-skeleton-screens
```

Open the project in Visual Studio Code:

```bash
code .
```

## Removing Boilerplate Code

Let's clean up the default files created by `create-react-app`:

1. Open the `src` folder and delete the following files:
   - `App.css`
   - `App.test.js`
   - `logo.svg`
   - `setupTests.js`

2. In `index.js`, remove the import and invocation of the service worker.

3. In `App.js`, remove the import of `logo.svg` and `App.css`.

Replace the code in `App.js` with the following:

```jsx
import React from 'react';
import User from './components/User';
import Articles from './components/Articles';

function App() {
  return (
    <div className="App">
      <header>
        <h1>React Skeletons</h1>
      </header>

      <div className="content">

      </div>
    </div>
  );
}

export default App;
```

## Creating Components

Now, let's create the necessary components. In the `src` directory, create a new folder called `components`. Inside this folder, create one file: `Home.js`.

```
Home.js

import React from 'react';

const Home = () => {
  return (
    <div className="home">
     
    </div>
  );
}

export default Home;
```

With these steps, you've set up a basic React application structure and created components for our landing page, which will serve as the foundation for implementing skeleton screens. This setup ensures a clean slate, allowing you to focus on building the skeleton loading screens that enhance user experience during data fetching.

Now we’re going to nest the Home component inside the content div in our App.js component. Copy the code below into your app.js to do this:

```.jsx
import Home from './Home';


function App() {
  return (
    <div className="App">
      <header>
        <h1>Meal Recipes</h1>
      </header>

      <div className="content">
        <Home />
      </div>
    </div>
  );
}

export default App;
```

## Adding Styles to the Application

To enhance the appearance of our application, we'll apply some styles to the header in `App.js`. Follow the steps below to update the styles in your `index.css` file.

### Update `index.css`

Open `index.css` and replace its contents with the following styles:

```css
body {
  margin: 0;
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', 'Roboto', 'Oxygen',
    'Ubuntu', 'Cantarell', 'Fira Sans', 'Droid Sans', 'Helvetica Neue',
    sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

code {
  font-family: source-code-pro, Menlo, Monaco, Consolas, 'Courier New',
    monospace;
}

header {
  background: #1e65ff;
  padding: 10px;
}

header h1 {
  color: white;
  max-width: 1200px;
  margin: 0 auto;
}
```

### Explanation of Styles

- **body**: Sets the base margin to 0 and specifies a list of fallback fonts for the body text. Also, enables font smoothing for better text rendering.
- **code**: Specifies a set of monospaced fonts for displaying code snippets.
- **header**: Applies a background color (#1e65ff) and padding to the header.
- **header h1**: Sets the text color to white, defines a maximum width for the content, and centers the header text by setting the margin to auto.

These styles will ensure that your application's header looks clean and visually appealing. The header will have a consistent blue background with white text, providing a professional look.

### Final Steps

After adding the styles, your header in the application should now have a distinct appearance, with a blue background and centered white text.

### Running the Application

To see your changes in action, make sure to start your development server if it's not already running:

```bash
npm start
```

Navigate to `http://localhost:3000` in your browser to view the updated header with the new styles applied.

With these styling updates, your React application now has a polished header, setting a solid foundation for building out the rest of the skeleton loading screens and other features.


Fetching Data

We're going to use the MealDB API for our data fetching: https://www.themealdb.com/api.php.

In our `App.js`, let's create a state to store our data when we fetch it.

```jsx
const [meals, setMeals] = useState(null);
```

Initially, our `meals` state will be `null` because we don't have any meal data yet. However, when this component is rendered to the DOM, we need to fetch the data. To do this, we'll use the `useEffect` hook, which runs automatically after the component has been rendered.

Let's create a `useEffect` and use a `setTimeout` so that we can see the effect of the skeleton loader for a bit longer. Note that we wouldn't typically use a delay like this in a production application. Copy and paste the code below into the `App.js` file:

```jsx
import React, { useState, useEffect } from 'react';
import Home from './components/Home';

function App() {

  const [meals, setMeals] = useState(null);

  // runs automatically after initial render
  useEffect(() => {
    setTimeout( async () => {
      const res = await fetch('https://www.themealdb.com/api/json/v1/1/search.php?s=chicken');
      const data = await res.json();
      setMeals(data);
    }, 5000)
  }, [])


  return (
    <div className="App">
      <header>
        <h1>Meal Recipes</h1>
      </header>

      <div className="content">
        <Home />
      </div>
    </div>
  );
}

export default App;
```

Now we need to check if we have our meal results. Let's use conditional rendering in React to display our meal recipe results. Copy and paste the code below into the `Home.js` file:

```.jsx
import { useEffect, useState } from 'react';
import { Link } from 'react-router-dom'


const Home = ( ) => {
    const [meals, setMeals] = useState(null);


  useEffect(() => {
    setTimeout(async () => {
      const res = await fetch(
        "https://www.themealdb.com/api/json/v1/1/search.php?s=chicken"
      );
      const meals = await res.json();
      setMeals(meals);
      console.log(meals.meals[0])
    }, 5000);
  }, []);


  return (
    <>
      <div className="bg-gray-900 text-white min-h-screen">
        <div className="m-auto max-w-3xl flex flex-col items-center justify-center text-center">


          <div id="meals" className="meals">
            {meals &&
              meals.meals.map((meal) => (
                <div className="meal" key={meal.idMeal}>
                  <Link to={`/MealInfo/${meal.idMeal}`}>
                    <img
                      className="meal-img"
                      src={meal.strMealThumb}
                      alt={meal.strMeal}
                    />
                    <div className="meal-info" data-mealid={meal.idMeal}>
                      <h3>{meal.strMeal}</h3>
                    </div>
                  </Link>
                </div>
              ))}
          </div>
          ){"}"}
        </div>
      </div>
    </>
  );
};


export default Home;
```

### Wrapping the App with BrowserRouter
Let’s wrap our App in main.js with BrowserRouter from react-router-dom. This is because we're using Link from react-router-dom in our Home component, which is calling useContext. The context it is looking for is provided by BrowserRouter, but our app is not wrapped by a BrowserRouter. Your main.js should be like this:

```.jsx
import React from 'react'
import ReactDOM from 'react-dom/client'
import App from './App.jsx'
import './index.css'
import { BrowserRouter } from 'react-router-dom'


ReactDOM.createRoot(document.getElementById("root")).render(
  <React.StrictMode>
    <BrowserRouter>
      <App />
    </BrowserRouter>
  </React.StrictMode>
);
```

### Creating a Reusable Skeleton Component

We aim to create a base skeleton element component that is reusable and can be configured into different shapes. To achieve this, let's start by creating a new folder named `skeletons` within our `src` directory. Inside this folder, we'll create a file named `skeletonElement.js`. This file will house our base skeleton component, which is designed to be both reusable and customizable. 

Here's the code to include in the `skeletonElement.js` file:

```.jsx
import React from 'react';
import './Skeleton.css';

const SkeletonElement = ({ type }) => {
  const classes = `skeleton ${type}`;

  return (
    <div className={classes}></div>
  )
}

export default SkeletonElement
```

In this code, we define a `SkeletonElement` component that accepts a `type` prop. This `type` prop allows us to customize the shape of the skeleton element by applying different CSS classes. The component then returns a `div` with the CSS classes applied.

Using this writing style (Introduction),  modify this:

