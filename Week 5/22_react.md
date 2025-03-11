# Node.js and React

## Basic Installation

```bash
sudo apt install nodejs npm
```

This command installs Node.js and npm (Node Package Manager) from the default repositories. However, these may not be the latest versions.

## Installing the Latest Node.js Version

```bash
curl -fsSL https://deb.nodesource.com/setup_20.x | sudo -E bash -
sudo apt install nodejs
```

These commands:
1. Download and run the NodeSource setup script for Node.js 20.x
2. Install the Node.js 20.x version from the NodeSource repository

## Installing Build Tools

```bash
sudo apt install build-essential
```

This installs essential build tools that are required for compiling and installing some npm packages that contain native code.

## Creating a React Application

```bash
npx create-react-app hello-world
```

This command:
1. Uses npx to run the create-react-app tool without installing it globally
2. Creates a new React application in a folder called "hello-world"
3. Sets up all necessary files, dependencies, and configuration

## Complete Reinstallation Process

If you need to completely remove an existing Node.js installation and install a fresh version:

```bash
# Remove existing Node.js completely
sudo apt remove nodejs npm -y
sudo apt autoremove -y

# Clean up any remaining Node.js files
sudo rm -rf /usr/local/bin/npm /usr/local/share/man/man1/node* /usr/local/lib/dtrace/node.d ~/.npm ~/.node-gyp /opt/local/bin/node /opt/local/include/node /opt/local/lib/node_modules

# Get the NodeSource setup script for Node.js 20.x
curl -fsSL https://deb.nodesource.com/setup_20.x | sudo -E bash -

# Install Node.js and npm from NodeSource repository
sudo apt install -y nodejs

# Verify installation
node -v  # Should show v20.x.x
npm -v   # Should show a compatible npm version

# Install build essentials (needed for some npm packages)
sudo apt install -y build-essential
```

This process:
1. Removes the existing Node.js and npm packages
2. Removes automatically installed dependencies that are no longer needed
3. Cleans up any remaining Node.js files from various locations
4. Sets up the NodeSource repository for Node.js 20.x
5. Installs Node.js from the NodeSource repository
6. Verifies the installation by checking versions
7. Installs build tools needed for some npm packages

## Getting Started

After creating your React application, you can:

1. Navigate to the project directory:
   ```bash
   cd hello-world
   ```

2. Start the development server:
   ```bash
   npm start
   ```

3. Open your browser and visit `http://localhost:3000` to see your application running

## Additional Information

- The React application comes with a development server, testing environment, and build scripts.
- You can modify the files in the `src` directory to customize your application.
- The `package.json` file contains information about your project and its dependencies.

## App.js 

### Code

```jsx
import logo from './logo.svg';
import './App.css';
import Counter from './Counter';
import Todo from './Todo';
import ThemeSwitcher from './themechanger';
import DatatoTable from './data';

function App() {
  return (
    <div className="App">
      <header className="App-header">
        <img src={logo} className="App-logo" alt="logo" />
        <h>
          HI Banwar
        </h>
        <p>
          Edit <code>src/App.js</code> and save to reload.
          <Counter />
          <Todo />
          <DatatoTable />
        </p>
        <ThemeSwitcher />
        <a
          className="App-link"
          href="https://reactjs.org"
          target="_blank"
          rel="noopener noreferrer"
        >
          Learn React
        </a>
      </header>
    </div>
  );
}

export default App;
```

### Imports

```jsx
import logo from './logo.svg';
import './App.css';
import Counter from './Counter';
import Todo from './Todo';
import ThemeSwitcher from './themechanger';
import DatatoTable from './data';
```

These lines import various resources needed by the component:

1. `logo from './logo.svg'` - Imports an SVG image file that will be used as the application logo
2. `'./App.css'` - Imports CSS styles specific to this component
3. `Counter from './Counter'` - Imports a custom Counter component
4. `Todo from './Todo'` - Imports a custom Todo component
5. `ThemeSwitcher from './themechanger'` - Imports a ThemeSwitcher component
6. `DatatoTable from './data'` - Imports a DatatoTable component

### Main Component Function

```jsx
function App() {
  return (
    // JSX content here
  );
}
```

This defines a functional component called `App`. In React, components are functions that return JSX (JavaScript XML) to define what should be rendered.

### Component Structure

The component returns a JSX structure:

- `<div className="App">` - The root container for the entire application
  - `<header className="App-header">` - A header section styled with the "App-header" class
    - `<img src={logo} className="App-logo" alt="logo" />` - Displays the React logo with CSS animations
    - `<h>HI Banwar</h>` - A greeting message (note: should be `<h1>`, `<h2>`, etc. for proper HTML)
    - `<p>` - A paragraph element that contains:
      - Text: "Edit `src/App.js` and save to reload."
      - `<Counter />` - Renders the Counter component
      - `<Todo />` - Renders the Todo component
      - `<DatatoTable />` - Renders the DatatoTable component
    - `<ThemeSwitcher />` - Renders the ThemeSwitcher component
    - `<a>` - A link to the React website with:
      - `className="App-link"` - Styling for the link
      - `href="https://reactjs.org"` - The destination URL
      - `target="_blank"` - Opens in a new tab
      - `rel="noopener noreferrer"` - Security attributes for external links

### Export Statement

```jsx
export default App;
```

This exports the App component as the default export of this module, allowing it to be imported in other files (typically in `index.js`).

### Counter.js

#### Code

```jsx
import React, {useState} from "react";

function Counter() {
    const [count, setCount] = useState(0);

    return (
        <div>
            <p>You clicked {count} times</p>
            <button onClick={() => setCount(count + 1)}>
                Click me
            </button>
        </div>
    )
}

export default Counter;
```

#### Imports

```jsx
import React, {useState} from "react";
```

This line imports:
1. `React` - The core React library
2. `useState` - A React Hook specifically destructured from the React library that enables state management in functional components

#### Component Function

```jsx
function Counter() {
    // Component code here
}
```

This defines a functional component named `Counter`. In React, functional components are JavaScript functions that return JSX to define the UI.

#### State Management

```jsx
const [count, setCount] = useState(0);
```

This line uses the `useState` Hook to:
1. Initialize a state variable called `count` with a value of `0`
2. Create a function called `setCount` that will be used to update the `count` value
3. React will preserve this state between re-renders of the component

The `useState` Hook takes an initial value as an argument (in this case, `0`) and returns an array with two elements:
- The current state value (`count`)
- A function to update that value (`setCount`)

#### Component Structure

The component returns a JSX structure:

```jsx
return (
    <div>
        <p>You clicked {count} times</p>
        <button onClick={() => setCount(count + 1)}>
            Click me
        </button>
    </div>
)
```

This structure consists of:
- A `<div>` container element
  - A paragraph `<p>` that displays the current count value: "You clicked {count} times"
  - A `<button>` element with:
    - Text content: "Click me"
    - An `onClick` event handler that calls `setCount()` to increment the count by 1 each time the button is clicked

The `{count}` syntax is JSX's way of embedding JavaScript expressions within markup.

#### Event Handling

```jsx
onClick={() => setCount(count + 1)}
```

This defines an inline arrow function that:
1. Is triggered when the button is clicked
2. Calls `setCount()` with the new value (`count + 1`)
3. When `setCount()` is called, React will:
   - Update the `count` state value
   - Re-render the component with the new state

#### Export Statement

```jsx
export default Counter;
```

This exports the Counter component as the default export of this module, allowing it to be imported in other files (like `App.js`).

#### Component Behavior

When this component is rendered:
1. It displays a paragraph showing how many times the button has been clicked (initially 0)
2. When the user clicks the button, the count increases by 1
3. The component re-renders with the updated count value
4. The cycle continues for each click


### Todo.js

#### Code 

```jsx
import React , { useState } from 'react';

function Todo() {
    const [todos, setTodos] = useState([]);
    const [input, setInput] = useState('');
    const [removeInput , setRemoveInput] = useState('');
    
    const addTodo = () => {
        if (input.trim() !== '') {
            setTodos([...todos, input]);
            setInput('');
        }
    };
    const removeTodo = () => {
        const index = todos.indexOf(removeInput);
        if(index === -1) {
            alert('Todo not found');
        }
        else{
            setTodos(todos.filter((_, i) => i !== index));
        }
        setRemoveInput('');
    };
    return (
        <div>
            <h1>Todo List</h1>
            <div>
            <input
                type="text"
                value={input}
                onChange={(e) => setInput(e.target.value)}
                placeholder="Add a todo"
            />
            <button onClick={addTodo}>Add</button>
            </div>
            <div>
            <input
                type="text"
                value={removeInput}
                onChange={(e) => setRemoveInput(e.target.value)}
                placeholder="Remove a todo"
            />            
            <button onClick={removeTodo}>Remove</button>
            </div>
            <ul>
                {todos.map((todo, index) => (
                    <li key={index}>{todo}
                    </li>
                ))}
            </ul>
        </div>
    )
}

export default Todo;
```

#### Imports

```jsx
import React , { useState } from 'react';
```

This line imports:
1. `React` - The core React library
2. `useState` - A React Hook destructured from the React library that enables state management in functional components

#### State Management

The component uses three state variables:

```jsx
const [todos, setTodos] = useState([]);
const [input, setInput] = useState('');
const [removeInput , setRemoveInput] = useState('');
```

1. `todos` - An array that stores all the todo items, initialized as an empty array
2. `input` - A string that stores the current value of the input field for adding todos
3. `removeInput` - A string that stores the current value of the input field for removing todos

Each state variable has its corresponding setter function (`setTodos`, `setInput`, `setRemoveInput`) that will be used to update the state.

#### Helper Functions

##### Add Todo Function

```jsx
const addTodo = () => {
    if (input.trim() !== '') {
        setTodos([...todos, input]);
        setInput('');
    }
};
```

This function:
1. Checks if the input is not empty or just whitespace
2. If valid, adds the new todo to the existing todos array using the spread operator (`...todos`)
3. Clears the input field by setting it to an empty string

##### Remove Todo Function

```jsx
const removeTodo = () => {
    const index = todos.indexOf(removeInput);
    if(index === -1) {
        alert('Todo not found');
    }
    else{
        setTodos(todos.filter((_, i) => i !== index));
    }
    setRemoveInput('');
};
```

This function:
1. Finds the index of the todo that matches the `removeInput` value
2. If the todo is not found (index is -1), shows an alert
3. If found, creates a new array without the todo at the matching index using the `filter` method
4. Clears the remove input field by setting it to an empty string

#### Component Structure

This structure consists of:
- A main `<div>` container
  - An `<h1>` heading "Todo List"
  - A `<div>` containing:
    - An `<input>` field for adding todos, bound to the `input` state
    - An "Add" `<button>` that calls the `addTodo` function when clicked
  - A `<div>` containing:
    - An `<input>` field for removing todos, bound to the `removeInput` state
    - A "Remove" `<button>` that calls the `removeTodo` function when clicked
  - A `<ul>` (unordered list) that:
    - Maps through the `todos` array
    - Creates an `<li>` (list item) for each todo
    - Assigns a unique `key` prop to each item (using the array index)

#### Event Handling

##### Input Field Events

```jsx
onChange={(e) => setInput(e.target.value)}
```

```jsx
onChange={(e) => setRemoveInput(e.target.value)}
```

These event handlers:
1. Capture the input event
2. Update the corresponding state variable with the current value of the input field

##### Button Click Events

```jsx
onClick={addTodo}
```

```jsx
onClick={removeTodo}
```

These event handlers call their respective functions when the buttons are clicked.

#### List Rendering

```jsx
{todos.map((todo, index) => (
    <li key={index}>{todo}</li>
))}
```

This code:
1. Uses the JavaScript `map` function to iterate over each item in the `todos` array
2. Creates an `<li>` element for each todo item
3. Sets a unique `key` prop for React's virtual DOM reconciliation (using the array index)
4. Displays the todo text inside each list item

### ThemeSwitcher.js

#### Code

```jsx
import React, { useState } from 'react';

function ThemeSwitcher() {
    const [theme, setTheme] = useState('light');

    const toggleTheme = () => {
        setTheme(theme === 'light' ? 'dark' : 'light');
    };

    return (
        <button onClick={toggleTheme}>
            {theme === 'light' ? 'Dark Mode' : 'Light Mode'}
            <style jsx>{`
                .App-header{
                    background-color:${theme === 'light' ? 'white' : '#282c34'} ;
                    color: ${theme === 'light' ? 'black' : 'white'};
                }
                button {
                    background-color: ${theme === 'light' ? 'white' : 'black'};
                    color: ${theme === 'light' ? 'black' : 'white'};
                }
            `}</style>
        </button>
    );
}

export default ThemeSwitcher;
```

#### State Management

```jsx
const [theme, setTheme] = useState('light');
```

This line uses the `useState` Hook to:
1. Initialize a state variable called `theme` with a value of `'light'`
2. Create a function called `setTheme` that will be used to update the `theme` value
3. React will preserve this state between re-renders of the component

#### Helper Function

```jsx
const toggleTheme = () => {
    setTheme(theme === 'light' ? 'dark' : 'light');
};
```

This function uses a ternary operator to:
1. Check if the current theme is `'light'`
2. If it is, set the theme to `'dark'`
3. If it's not, set the theme to `'light'`

This effectively toggles between the two theme options.

#### Component Structure



This structure consists of:
- A `<button>` element with:
  - An `onClick` event handler that calls the `toggleTheme` function
  - Dynamic text content that shows either "Dark Mode" or "Light Mode" based on the current theme
  - A `<style jsx>` element containing CSS rules (this uses CSS-in-JS approach)

#### Inline Styling with CSS-in-JS

```jsx
<style jsx>{`
    .App-header{
        background-color:${theme === 'light' ? 'white' : '#282c34'} ;
        color: ${theme === 'light' ? 'black' : 'white'};
    }
    button {
        background-color: ${theme === 'light' ? 'white' : 'black'};
        color: ${theme === 'light' ? 'black' : 'white'};
    }
`}</style>
```

This section uses a CSS-in-JS approach with the `style jsx` tag to:
1. Define CSS rules that change based on the current theme state
2. Target the `.App-header` class to change:
   - Background color (white for light mode, dark gray #282c34 for dark mode)
   - Text color (black for light mode, white for dark mode)
3. Target all `button` elements to change:
   - Background color (white for light mode, black for dark mode)
   - Text color (black for light mode, white for dark mode)

#### Component Behavior

When this component is rendered:
1. It displays a button that says "Dark Mode" (initially, since the theme starts as 'light')
2. When clicked, it toggles the theme state between 'light' and 'dark'
3. The button text changes to reflect the mode the user can switch to
4. The CSS styles for `.App-header` and `button` update dynamically based on the theme

### DatatoTable.js

#### Code

```jsx
import React, { useState } from 'react';

function DatatoTable() {
    const [data, setData] = useState([]);
    const [name, setName] = useState('');
    const [email, setEmail] = useState('');

    const DataAsTable = () => {
        setData([...data, { name, email }]);
        setName('');
        setEmail('');
    };

    return (
    <>
        <style>
        {`
            .table {
                width: 100%;
                border-collapse: collapse;
                margin-top: 10px;
            }
            .table th, .table td {
                border: 1px solid black;
                padding: 10px;
                text-align: left;
            }
            .table th {
                background-color: #f2f2f2;
                color : black;
            }
        `}
        </style>
        <div>
            <input
                type="text"
                value={name}
                onChange={(e) => setName(e.target.value)}
                placeholder="Name"
            />
            <input
                type="email"
                value={email}
                onChange={(e) => setEmail(e.target.value)}
                placeholder="Email"
            />
            <button onClick={DataAsTable}>Add Data</button>
            <table className='table'>
                <thead>
                    <tr>
                        <th>Name</th>
                        <th>Email</th>
                    </tr>
                </thead>
                <tbody>
                    {data.map((item, index) => (
                        <tr key={index}>
                            <td>{item.name}</td>
                            <td>{item.email}</td>
                        </tr>
                    ))}
                </tbody>
            </table>
        </div>
    </>
    )
}

export default DatatoTable;
```

#### State Management

```jsx
const [data, setData] = useState([]);
const [name, setName] = useState('');
const [email, setEmail] = useState('');
```

The component uses three state variables:
1. `data` - An array that stores all the entries (objects with name and email properties), initialized as an empty array
2. `name` - A string that stores the current value of the name input field
3. `email` - A string that stores the current value of the email input field

#### Helper Function

```jsx
const DataAsTable = () => {
    setData([...data, { name, email }]);
    setName('');
    setEmail('');
};
```

This function:
1. Adds a new object containing the current name and email values to the data array using the spread operator (`...data`)
2. Clears both input fields by setting their values to empty strings

#### Component Structure

The component returns a JSX structure wrapped in a React Fragment (`<>`):

```jsx
return (
<>
    <style>
    {/* CSS styling */}
    </style>
    <div>
        {/* Input fields, button, and table */}
    </div>
</>
)
```

The structure consists of:
- A React Fragment (`<>...</>`) as the root container
- A `<style>` element containing CSS rules for the table
- A `<div>` container that holds:
  - Input fields for name and email
  - An "Add Data" button
  - A table displaying all entries

#### CSS Styling

```jsx
<style>
{`
    .table {
        width: 100%;
        border-collapse: collapse;
        margin-top: 10px;
    }
    .table th, .table td {
        border: 1px solid black;
        padding: 10px;
        text-align: left;
    }
    .table th {
        background-color: #f2f2f2;
        color : black;
    }
`}
</style>
```

This section defines CSS styles for the table:
1. Sets the table to occupy 100% width
2. Collapses borders between cells
3. Adds margin above the table
4. Applies borders, padding, and left alignment to table cells and headers
5. Gives table headers a light gray background and black text

#### Form Inputs

```jsx
<input
    type="text"
    value={name}
    onChange={(e) => setName(e.target.value)}
    placeholder="Name"
/>
<input
    type="email"
    value={email}
    onChange={(e) => setEmail(e.target.value)}
    placeholder="Email"
/>
<button onClick={DataAsTable}>Add Data</button>
```

These elements:
1. Create a text input field for the name that:
   - Is bound to the `name` state
   - Updates the `name` state on every change
   - Displays "Name" as placeholder text
2. Create an email input field for the email that:
   - Is bound to the `email` state
   - Updates the `email` state on every change
   - Displays "Email" as placeholder text
3. Create a button that calls the `DataAsTable` function when clicked

#### Table Structure

```jsx
<table className='table'>
    <thead>
        <tr>
            <th>Name</th>
            <th>Email</th>
        </tr>
    </thead>
    <tbody>
        {data.map((item, index) => (
            <tr key={index}>
                <td>{item.name}</td>
                <td>{item.email}</td>
            </tr>
        ))}
    </tbody>
</table>
```

This creates a table with:
1. A `thead` section containing a single row with "Name" and "Email" headers
2. A `tbody` section that:
   - Maps through each item in the `data` array
   - Creates a table row for each item
   - Assigns a unique `key` prop to each row (using the array index)
   - Displays the item's name and email in separate table cells

#### Event Handling

```jsx
onChange={(e) => setName(e.target.value)}
```

```jsx
onChange={(e) => setEmail(e.target.value)}
```

These event handlers:
1. Capture the input event
2. Update the corresponding state variable with the current value of the input field

```jsx
onClick={DataAsTable}
```

This event handler calls the `DataAsTable` function when the button is clicked.

## Component Behavior

When this component is rendered:
1. It displays two input fields for name and email, and an "Add Data" button
2. When the user enters data and clicks the button, the data is added to the table
3. The input fields are cleared after adding data
4. Each new entry appears as a row in the table
5. The table is styled according to the CSS rules defined within the component

## Rouitng


### Installation
Before using React Router, make sure you install the necessary package:
```sh
npm install react-router-dom
```

### Routing Structure
**React Router** to navigate between different components: `App.js`, `Home.js`, and `About.js`.

#### **Base_App Page(`App.js`)**
In `App.js`, we import necessary components from `react-router-dom` and define the routes inside **`<Routes>`**:

```jsx
import { BrowserRouter as Router, Routes, Route, Link } from 'react-router-dom';
import Home from './Home';
import About from './About';

function App() {
  return (
    <Router>
      <div className="App">
        <header className="App-header">
          <h1>HI Banwar</h1>
          <Link to="/home">
            <button>HOME</button>
          </Link>
          <Link to="/about">
            <button>ABOUT</button>
          </Link>
        </header>

        <Routes>
          <Route path="/home" element={<Home />} />
          <Route path="/about" element={<About />} />
        </Routes>
      </div>
    </Router>
  );
}

export default App;
```

#### **Home Page(`Home.js`)**
Inside `Home.js`, we use the `useNavigate` hook to navigate to the **About**, **Base** page when the buttons are clicked:

```jsx
import { useNavigate } from 'react-router-dom';

function Home() {
  const navigate = useNavigate();
  return (
    <div>
      <h1>Home Page</h1>
      <button onClick={() => navigate('/about')}>About</button>
      <button onClick={() => navigate('/')}>Base_App</button>
    </div>
  );
}

export default Home;
```

#### **About Page (`About.js`)**
The `About.js` component is a simple page displayed when navigating to `/about`:

```jsx
import { useNavigate } from 'react-router-dom';

function About() {
  const navigate = useNavigate();
  return (
    <div>
      <h1>About Page</h1>
      <button onClick={() => navigate('/home')}>Home</button>
      <button onClick={() => navigate('/')}>Base_App</button>
    </div>
  );
}

export default About;
```

#### How Navigation Works
1. Clicking the **HOME** button in `App.js` navigates to `/home` and displays the `Home.js` component.
2. Clicking the **ABOUT** button in `App.js` navigates to `/about` and displays the `App.js` component.
3. Inside `Home.js`, clicking the **About** button navigates to `/about`, displaying `About.js`.
3. Inside `Home.js`, clicking the **Base_App** button navigates to `/`, displaying `App.js`.
4. Inside About.js, clicking the **Base_App** button navigates to `/`, displaying `App.js`.
4. Inside About.js, clicking the **HOME** button navigates to `/home`, displaying `Home.js`.
3. Routing is handled using `<Routes>` and `<Route>` from `react-router-dom`.

#### Overview
- `BrowserRouter` is used to wrap the application for routing.
- `<Routes>` and `<Route>` define the available paths.
- `<Link>` is used for navigation within `App.js`.
- `useNavigate` is used for programmatic navigation within `Home.js`.