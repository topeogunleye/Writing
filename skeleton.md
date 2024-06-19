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
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}


header {
  font-size: 1.5rem;
  font-weight: 900;
  display: grid;
  align-items: center;
}


header h1 {
  max-width: 1200px;
  margin: 0 auto;
}


.container {
  background-color: #6b7280;
  color: #ffffff;
  min-height: 100vh;
  transition-property: all;
  transition-duration: 1s;
  transition-timing-function: ease-out;
}


.meals {
  display: grid;
  grid-template-columns: repeat(1, minmax(0, 1fr));
  gap: 1.25rem; /* Equivalent to gap-5 in Tailwind */
  margin-top: 1.25rem; /* Equivalent to mt-5 in Tailwind */
  transition-property: all;
  transition-duration: 1s;
  transition-timing-function: ease-out;
  padding: 10px 50px;
}


@media (min-width: 640px) {
  .meals {
    grid-template-columns: repeat(2, minmax(0, 1fr));
  }
}


@media (min-width: 768px) {
  .meals {
    grid-template-columns: repeat(3, minmax(0, 1fr));
  }
}


@media (min-width: 1280px) {
  .meals {
    grid-template-columns: repeat(4, minmax(0, 1fr));
  }
}


/* .meal class */
.meal {
  /* Equivalent to rounded overflow-hidden shadow-md cursor-pointer relative h-60 w-60 xs:h-56 xs:w-52 sm:h-56 sm:w-52 lg:h-56 lg:w-52 text-left; */
  border-radius: 0.25rem;
  overflow: hidden;
  box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1),
    0 2px 4px -1px rgba(0, 0, 0, 0.06);
  cursor: pointer;
  position: relative;
  height: 15rem; /* Equivalent to h-60 */
  width: 15rem; /* Equivalent to w-60 */
}


.meal-img:hover {
  box-shadow: 0 10px 15px -3px rgba(147, 102, 102, 0.1),
    0 4px 6px -2px rgba(0, 0, 0, 0.05);
  transition-property: all;
  transition-duration: 1s;
  transition-timing-function: ease-out;
}


/* .meal-img class */
.meal-img {
  /* Equivalent to w-full h-full border-solid border-4 border-white; */
  width: 100%;
  height: 100%;
  border-style: solid;
  border-width: 4px;
  border-color: #ffffff; /* Assuming white border */
}
```

### Explanation of Styles

1. The universal selector (`*`) is used to apply the following styles to all elements on the page:
   - `margin: 0;` and `padding: 0;` set the margin and padding of all elements to zero, effectively removing any default spacing.
   - `box-sizing: border-box;` ensures that the total width and height of an element include both its content and padding, but not the margin.

2. The `header` element:
   - `font-size: 1.5rem;` sets the font size to 1.5 times the default font size.
   - `font-weight: 900;` makes the text bold.
   - `display: grid;` uses CSS Grid for layout.
   - `align-items: center;` vertically centers the content within the header.

3. The `.container` class:
   - `background-color: #6b7280;` sets the background color to a shade of gray (#6b7280).
   - `color: #ffffff;` sets the text color to white.
   - `min-height: 100vh;` ensures that the container takes up at least the full viewport height.
   - The `transition` properties control the animation duration and timing function when transitioning styles.

4. The `.meals` class:
   - Uses CSS Grid to create a responsive grid layout with varying column numbers based on screen width.
   - `gap: 1.25rem;` adds spacing between grid items.
   - `margin-top: 1.25rem;` provides top margin.
   - The `transition` properties control the animation when transitioning styles.
   - `padding: 10px 50px;` adds padding to the container.

5. Media queries:
   - Adjust the number of columns in the `.meals` grid based on screen width.

6. The `.meal` class:
   - Creates a card-like styling for meal items.
   - Sets border radius, overflow behavior, box shadow, cursor, and dimensions.

7. The `.meal-img` class:
   - Sets the image dimensions and adds a white border.


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

## Adding React Router

Since you're using `Link` from `react-router-dom`, we need to install `react-router-dom` in your project. Follow these steps:

1. Open your terminal or command prompt.
2. Navigate to your project directory.
3. Run the following command to install `react-router-dom` using npm:

```bash
npm install react-router-dom
```

Alternatively, if you're using Yarn, you can use this command:

```bash
yarn add react-router-dom
```

4. Once the installation is complete, you can import the necessary components from `react-router-dom` and start defining your routes in your `Home.js` file.

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

Let’s create the style for our skeleton component by creating a file named Skeleton.css and adding the below styles in it:

/* basic styles */
.skeleton {
  background: #ddd;
  margin: 10px 0;
  border-radius: 4px;
}


.skeleton.title {
  width: 50%;
  height: 24px;
  margin-bottom: 15px;
}


.imageBig {
  width: 240px;
  height: 240px;
}


.imageMealInfo {
  width: 92vw;
  height: 48vh;
  padding-top: 0;
  margin-top: 0;
}


.mealInfo {
  width: 176px;
  height: 24px;
}


.textBig {
  width: 240px;
  height: 1152px;
}


.liText {
  width: 100px;
  height: 16px;
  margin: 4px 15px;
}


.imageSmall {
  width: 240px;
  height: 240px;
}


@media screen and (min-width: 1080px) {
  .imageMealInfo {
    max-width: 320px;
    max-height: 320px;
  }
}
@media screen and (min-width: 767px) {
  .imageSmall {
    width: 208px;
    height: 224px;
  }


  .title {
    width: 50%;
    height: 24px;
  }


  .imageBig {
    min-width: 100vw;
    min-height: 320px;
  }


  .imageMealInfo {
    max-width: 200px;
    max-height: 200px;
    margin-bottom: 8rem;
  }


  .mealInfo {
    width: 512px;
    height: 24px;
  }


  .textBig {
    width: 576px;
    height: 456px;
  }


  .liText {
    width: 100px;
    height: 16px;
  }
}


@media screen and (min-width: 475px) {
  .imageSmall {
    width: 208px;
    height: 212px;
  }


  .imageMealInfo {
    width: 92vw;
    height: 62vh;
  }
 
}


@media screen and (min-width: 425px) {
  .imageBig {
    width: 312px;
    height: 312px;
  }


  .textBig {
    width: 318.75px;
    height: 840px;
  }
}


@media screen and (min-width: 375px) {
  .imageBig {
    width: 281.25px;
    height: 281.25px;
  }


  .textBig {
    width: 281.25px;
    height: 960px;
  }


 
}
/* skeleton profile */
.skeleton-wrapper {
  /* margin: 20px auto; */
  padding: 10px 15px;
  border-radius: 4px;
  position: relative;
}


.wrapper {
  border-radius: 4px;
  position: relative;
}


/* Category */
.catImg {
  width: 177px;
  height: 110px;
}


.catName {
  width: 75px;
  height: 28px;
}


/* themes */
.light {
  background: #f2f2f2;
}


.dark {
  background: #444;
}


.dark .skeleton {
  background: #777;
}


/* animation effects */
.shimmer-wrapper {
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  position: absolute;
  animation: loading 2.5s infinite;
}


.shimmer {
  width: 50%;
  height: 100%;
  background: rgba(255, 255, 255, 0.2);
  transform: skewX(-20deg);
  box-shadow: 0 0 30px 30px rgba(255, 255, 255, 0.05);
}


.dark .shimmer {
  background: rgba(255, 255, 255, 0.05);
}


@keyframes loading {
  0% {
    transform: translateX(-150%);
  }
  50% {
    transform: translateX(-60%);
  }
  100% {
    transform: translateX(150%);
  }
}


/* skeleton profile */
.skeleton-profile {
  display: grid;
  grid-template-columns: 1fr 2fr;
  grid-gap: 30px;
  align-items: center;
}


/* themes */
.skeleton-wrapper.light {
  background: #f2f2f2;
}
.skeleton-wrapper.dark {
  background: #444;
}
.skeleton-wrapper.dark .skeleton {
  background: #777;
}

Explanation of Styles for Skeleton Loading

1. Skeleton Element Styles: The `SkeletonElement.js` file defines a reusable skeleton component that can be configured with different shapes. These shapes are defined in the accompanying `Skeleton.css` file. By applying different CSS classes, we can customize the appearance of skeleton elements, such as their size, color, and animation effects.

2. Wrapper Styles: The `SkeletonHome.js` file wraps the skeleton elements in a `div` with the class `wrapper`. This wrapper provides a container for the skeleton elements and allows for additional styling or layout adjustments if needed.

3. Shimmer Effect: The `Shimmer` component adds a subtle shimmer effect to the skeleton elements. This effect is achieved through CSS animations and helps indicate to the user that content is loading.


Creating our Skeleton Home page
Let’s create a SkeletonHome.js file and add this code below to it:


import Shimmer from "./Shimmer";
import SkeletonElement from "./SkeletonElement";


const SkeletonHome = ({ theme }) => {
  const themeClass = theme || "light";


  return (
    <div className={`wrapper ${themeClass}`}>
      <div className="meals grid grid-cols-1  gap-5 mt-5 xs:grid-cols-2 sm:grid-cols-3 xl:grid-cols-4">
        <SkeletonElement type="imageSmall" />
        <SkeletonElement type="imageSmall" />
        <SkeletonElement type="imageSmall" />
        <SkeletonElement type="imageSmall" />
        <SkeletonElement type="imageSmall" />
        <SkeletonElement type="imageSmall" />
        <SkeletonElement type="imageSmall" />
        <SkeletonElement type="imageSmall" />
        <SkeletonElement type="imageSmall" />
        <SkeletonElement type="imageSmall" />
        <SkeletonElement type="imageSmall" />
        <SkeletonElement type="imageSmall" />
      </div>
      <Shimmer />
    </div>
  );
};


SkeletonHome.propTypes = {
  theme: PropTypes.string
};


export default SkeletonHome;



Now let’s make use of our SkeletonHome.js component in our Home.js component so that we have a skeleton loader on our home component. Copy the code below and paste it into our Home.js component:

```.jsx
import { useEffect, useState } from "react";
import SkeletonHome from "../skeletons/SkeletonHome";


const Home = () => {
  const [meals, setMeals] = useState(null);


  useEffect(() => {
    setTimeout(async () => {
      const res = await fetch(
        "https://www.themealdb.com/api/json/v1/1/search.php?s=chicken"
      );
      const meals = await res.json();
      setMeals(meals);
      console.log(meals.meals[0]);
    }, 5000);
  }, []);


  return (
    <>
      <div className="container">
        <div className="m-auto max-w-3xl flex flex-col items-center justify-center text-center">
          <div id="meals" className="meals">
            {meals &&
              meals.meals.map((meal) => (
                <div className="meal" key={meal.idMeal}>
                  <img
                    className="meal-img"
                    src={meal.strMealThumb}
                    alt={meal.strMeal}
                  />
                  <div className="meal-info" data-mealid={meal.idMeal}>
                    <h3>{meal.strMeal}</h3>
                  </div>
                </div>
              ))}
              {!meals && [1,2,3,4,5].map((n) => <SkeletonHome key={n} theme="dark" />)}
          </div>
          {}
        </div>
      </div>
    </>
  );
};


export default Home;
```




Explanation of Theme Customization in SkeletonHome.js Component:

The SkeletonHome.js component offers theme customization through the `theme` prop. This prop allows users to specify the color scheme for the skeleton elements, providing flexibility in integrating the skeleton loading experience with different application designs.

1. **Theme Prop Handling**: Within the SkeletonHome.js component, the `theme` prop is utilized to determine the color scheme. By default, if no theme is provided, the component falls back to the "light" theme. This ensures that the component remains functional even if the theme prop is not explicitly set.

```jsx
const SkeletonHome = ({ theme }) => {
  const themeClass = theme || "light"; // Default to "light" theme if no theme is provided
  // Rest of the component code...
};
```

2. **Applying Theme Classes**: The determined theme, either "light" or the provided value, is used to dynamically generate CSS classes. These classes are then applied to the wrapper `div` of the skeleton elements, enabling the styling of the skeleton components based on the selected theme.

```jsx
<div className={`wrapper ${themeClass}`}>
  {/* Skeleton elements go here */}
</div>
```

3. **Theme Flexibility**: By allowing users to specify the theme, developers can seamlessly integrate the skeleton loading experience with their application's design language. For example, setting the theme to "dark" can complement dark mode interfaces, ensuring consistency in visual presentation across different application states.

```jsx
<SkeletonHome key={n} theme="dark" />
```

In summary, the SkeletonHome.js component facilitates theme customization through the `theme` prop, providing users with the ability to tailor the skeleton loading experience to match their application's design requirements. This flexibility enhances the overall user experience by ensuring a cohesive and visually appealing transition between content loading and display.

Conclusion:

In wrapping up, adding skeleton loading screens to your React app can make it feel faster and more user-friendly. With components like `SkeletonHome`, you can easily create these loading screens for different parts of your app. By using CSS and React, you can customize how these loading screens look and behave to match your app's style. Ultimately, using skeleton loading screens improves how users perceive your app's speed and makes it more enjoyable to use.


Using this writing style (Introduction),  modify this:

