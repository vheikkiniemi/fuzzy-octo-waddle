# Introduction to React

## What is React?

[`React`](https://react.dev/) is an open-source JavaScript library developed by Facebook (now Meta), specifically designed for building reusable components in web applications. React allows developers to create efficient, reactive, and reusable user interfaces (UI) for web applications.

## History

React was released in 2013 when Facebook developed it for internal use to solve complex UI management challenges. Its popularity grew quickly, and today, React is widely used in both startups and large tech companies.

## Connections to Other Technologies

React is not a full-stack solution on its own but focuses solely on UI development. It is often used in combination with the following technologies:
- **Node.js and Express**: Backend logic and APIs
- **Redux or Zustand**: State management for large applications
- **Next.js**: Server-side rendering (SSR) and static site generation (SSG) for React applications
- **TypeScript**: Better type safety and development experience

## Example Use Cases
React is widely used in various applications, such as:
- **Facebook**: Originally developed for Facebook's needs.
- **Instagram**: A UI built using React components.
- **Netflix**: Improved performance and development tools.
- **Airbnb**: Modular and reusable components.

## Pros and Cons

### Pros
- ✅ Fast and efficient: Virtual DOM optimizes updates and makes React fast.
- ✅ Component-based architecture: Easy to reuse and maintain code.
- ✅ Strong community and ecosystem: Extensive support, documentation, and third-party libraries.
- ✅ Good development experience: Hot-reloading and powerful development tools.

### Cons
- ❌ Steep learning curve: JSX, hooks, and state management can be challenging at first.
- ❌ SEO challenges: Server-side rendering may be required for SEO optimization.
- ❌ Rapid evolution: Changes and new features may require constant learning.

# React Basics

## First React Component
A React application is built with components. Below is an example of a simple React component:
```javascript
function Greeting() {
  return <h1>Hello, welcome to the React world!</h1>;
}
```

Components can be used within other components as follows:
```javascript
function App() {
  return (
    <div>
      <Greeting />
    </div>
  );
}
```

## JSX – JavaScript XML
[`React's JSX`](https://react.dev/learn/writing-markup-with-jsx) is a special syntax that resembles HTML but works inside JavaScript:
```javascript
const element = <h1>Hello, world!</h1>;
```

JSX is converted into JavaScript using the Babel compiler:
```javascript
const element = React.createElement("h1", null, "Hello, world!");
```

## State Management
React's state management allows dynamic changes to a component's state.
```javascript
import { useState } from 'react';

function ClickCounter() {
  const [counter, setCounter] = useState(0);

  return (
    <div>
      <p>Clicked {counter} times</p>
      <button onClick={() => setCounter(counter + 1)}>Click me</button>
    </div>
  );
}
```

# Setting up Visual Studio Code for React Development

Before starting your first React application, follow these steps to set up Visual Studio Code:

1. Install Node.js: Download and install [Node.js](https://nodejs.org/), which includes npm (Node Package Manager).
2. Install VS Code and essential extensions:
    - `ES7+ React/Redux/React-Native snippets`
    - `Prettier - Code formatter`
    - `Live Server`
3. Create a new project using Vite by running the following command in the terminal:
    ```sh
    npm create vite@latest my-app -- --template react
    ```
    This command creates a new React project called `my-app` using Vite, which is a faster alternative to Create React App.

4. Navigate to the project folder and install dependencies:
    ```sh
    cd my-app
    npm install
    ```
5. Start the development server:
    ```sh
    npm run dev
    ```
    This opens the React application in a browser at http://localhost:5173.

## Example Project: A Simple Web Page with CSS

Here is a simple example of a React web page that also includes CSS.

1. Create **`src/App.jsx`** file:
    ```javascript
    import './App.css';

    function App() {
      return (
        <div className="container">
          <h1>Welcome to the React Page!</h1>
          <p>This is a simple React page styled with CSS.</p>
        </div>
      );
    }

    export default App;
    ```

2. Create **`src/App.css`** file:
    ```css
    .container {
      text-align: center;
      margin-top: 50px;
    }

    h1 {
      color: blue;
    }

    p {
      font-size: 18px;
    }
    ```

3. Start the application → Restart the development server with the command:
    ```sh
    npm run dev
    ```
    Your page will be visible at http://localhost:5173, displaying a styled greeting text.

# Additional Resources
- [Full Stack open](https://fullstackopen.com/en/)
- [Full Stack open → React Basics](https://fullstackopen.com/en/part1/introduction_to_react)