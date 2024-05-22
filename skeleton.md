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
        <Articles />
        <User />
      </div>
    </div>
  );
}

export default App;
```

## Creating Components

Now, let's create the necessary components. In the `src` directory, create a new folder called `components`. Inside this folder, create two files: `User.js` and `Articles.js`.

### User.js

```jsx
import React from 'react';

const User = () => {
  return (
    <div className="user">
      <h2>User Details</h2>
    </div>
  );
}

export default User;
```

### Articles.js

```jsx
import React from 'react';

const Articles = () => {
  return (
    <div className="articles">
      <h2>All Articles</h2>
    </div>
  );
}

export default Articles;
```

With these steps, you've set up a basic React application structure and created components for User and Articles, which will serve as the foundation for implementing skeleton screens. This setup ensures a clean slate, allowing you to focus on building the skeleton loading screens that enhance user experience during data fetching.


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


## Applying Grid Layout

To arrange the Article and User components side by side, we'll use CSS Grid. This powerful layout system allows us to design complex user interfaces with ease. Open the `index.css` file and append the following styles:

```css
h2 {
  padding-bottom: 10px;
  border-bottom: 1px solid #eee;
}

.content {
  width: 100%;
  max-width: 1200px;
  margin: 0 auto;
  padding: 20px;
  display: grid;
  grid-template-columns: 2fr 1fr;
  gap: 100px;
}
```

### Explanation of Styles

- **h2**: Adds a padding to the bottom of the `h2` elements and a subtle border to visually separate the headers from the content.
- **.content**: Defines the layout of the content area. The `display: grid;` property turns the content area into a grid container. The `grid-template-columns: 2fr 1fr;` property creates two columns with a ratio of 2:1, meaning the Articles component will take up twice as much space as the User component. The `gap: 100px;` property adds space between the grid items.

With these styles, the Articles and User components will be displayed side by side, with the Articles component taking up two-thirds of the width and the User component taking up one-third.

Viewing the Layout

To see the changes, make sure your development server is running:

```bash
npm start
```

Then, navigate to `http://localhost:3000
