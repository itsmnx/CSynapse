## ReactNotes 
React is a front-end JavaScript library.

React was developed by the Facebook Software Engineer Jordan Walke.

React is also known as React.js or ReactJS.

React is a tool for building UI components.

## How does React Work?
React creates a VIRTUAL DOM in memory.
- Instead of manipulating the browser's DOM directly, React creates a virtual DOM in memory, where it does all the necessary manipulating, before making the changes in the browser DOM.

React only changes what needs to be changed!
- React finds out what changes have been made, and changes only what needs to be changed.

---

## Difference between the JS and JSX
.js file is a normal js file in react :
- it contains plain js
- it can contain react code without JSX
- browsers understand .js directly

```js
import React from "react";

function App() {
  return React.createElement(
    "h1",
    null,
    "Hello World"
  );
}

export default App;

This is valid in react
but it is sometime hard to read and write 
```
a .jsx file is js+HTML like syntax(JSX)
```html
JSX=javascript XML
```
It allows you to wrute UI like HTML inside js.


## 🧩 What is Fragment in React?

A Fragment lets you group multiple elements without adding an extra DOM node.

👉 It solves the “one parent element” problem in JSX.
```jsx
return (
  <h1>Hello</h1>
  <p>Welcome</p>
);
Invalid JSX 
Adjacent JSX elements must be wrapped in an enclosing tag
```

Perfect solution to use fragment like -
```jsx
import React from "react";

return (
  <React.Fragment>
    <h1>Hello</h1>
    <p>Welcome</p>
  </React.Fragment>
);

NO extra DOM node
clean HTML
```
or you can use short syntax like <></>
```jsx
return (
  <>
    <h1>Hello</h1>
    <p>Welcome</p>
  </>
);
```
What Fragment Does Internally

Fragment:
- Exists only in Virtual DOM
- Does NOT appear in real DOM


## What is Map method in JSX?
- it is a converter in react
- map() is a JavaScript array method used in React to       render lists of elements dynamically.

1. map() in Plain JavaScript (Foundation)
  ```js
    const nums = [1, 2, 3];

    const doubled = nums.map(n => n * 2);

    console.log(doubled); // [2, 4, 6]
  ```
  📌 Rule-

    - map() loops over array

    - Returns a NEW array

    - Does NOT modify original array

2. Bsically map method kya karta ek chiz ko dusre me convert karta hai kyuki UI is based on the data and data often comes as arrays
for example-
```js
const users = ["Manas", "Aman", "Rohit"];
```
now you want like -
```html
<li>Manas</li>
<li>Aman</li>
<li>Rohit</li>
```
but aap yha manully kar rhe ho so we use a map() method here.

map() Inside JSX (Core Usage)
```jsx
function App() {
  const users = ["Manas", "Aman", "Rohit"];

  return (
    <ul>
      {users.map(user => (  
        <li>{user}</li>
      ))}
    </ul>
  );
}


//yha per aapne map() method call kiya and moslty jo bhi data dynamically show krna hai woh hamesha hi curly braces me hi hoga
```
Important:

- {} → JavaScript inside JSX

- map() returns JSX elements

- React renders them


# Aur ache samje toh
map() = Loop ka hi modern form
```js
const arr = [1, 2, 3];

arr.map(x => x * 2);
```
yeh internally aise hi kaam karta hai:
```js
for (let i = 0; i < arr.length; i++) {
  // har element par kaam
}
```

Difference:
- for → manual loop
- map → automatic loop + return new array

## Note
jab bhi hum jsx use krte hai toh className hi use krte hai sirf class use krenge toh woh galat hoga woh sirf js me hi use kr skate hai
- JSX HTML nahi hai, yeh JavaScript ke andar likha gaya syntax hai.
- JavaScript me class-> reserved keyword hai
- isliye react me HTML ka class = JSX me className

## what is conditional rendering in JSX?
Condition ke base par JSX ka UI show ya hide karna hi conditional rendering hota hai.

Matlab:
- Agar condition true → UI dikhao
- Agar condition false → UI mat dikhao

**Kyun zaroori hota hai?**

Real apps me:
- User logged in / logged out
- Data load hua / nahi hua
- Button enable / disable
- Error aaya / nahi aaya

👉 Sab condition par depend karta hai.


## Conditional Rendering in React

### ✅ Correct Ways of Conditional Rendering

#### 🔹 1. Ternary Operator (MOST USED ⭐)

```jsx
{isLoggedIn ? <Dashboard /> : <Login />}
```

**📌 Use Case:** When you have two options

---

#### 🔹 2. Logical AND (&&) (Very common)

```jsx
{isAdmin && <AdminPanel />}
```

**📌 Use Case:** If condition is false → nothing will be rendered

**⚠️ Warning:**

```jsx
{0 && <p>Hello</p>} // 0 will be rendered
```

---

#### 🔹 3. if Statement (Outside JSX)

```jsx
let content;

if (isLoggedIn) {
  content = <Dashboard />;
} else {
  content = <Login />;
}

return <div>{content}</div>;
```

**Benefits:**
- ✔️ Clean code
- ✔️ Best for complex logic

---

#### 🔹 4. Function Approach

```jsx
function renderPage() {
  if (isLoggedIn) return <Dashboard />;
  return <Login />;
}

return <div>{renderPage()}</div>;
```

**Benefits:**
- ✔️ Reusable
- ✔️ Testable

---

#### 🔹 5. Switch Case (Advanced)

```jsx
function renderStatus(status) {
  switch (status) {
    case "loading":
      return <Loading />;
    case "error":
      return <Error />;
    default:
      return <Data />;
  }
}
```

---

### 4️⃣ Real-Life Example

```jsx
{isLoading ? (
  <p>Loading...</p>
) : (
  <p>Data Loaded</p>
)}
```

## What are Props in React?
Props (properties) are used to pass data from a parent component to a child component in React.
- Think of props like function parameters, but for components.

1. Props ≈ Function Arguments (BEST ANALOGY)

Normal JS function
```js
function greet(name) {
  return "Hello " + name;
}

greet("Manas");
```

2. React component
```jsx
function Greeting(props) {
  return <h1>Hello {props.name}</h1>;
}

<Greeting name="Manas" />
```

👉 Same idea, different syntax.

- How Props Work (Behind the Scenes)
  ```jsx
  <Greeting name="Manas" age={21} />
  ```

- React internally does:
  ```js
  Greeting({ name: "Manas", age: 21 });
  ```


👉 Props are just a JavaScript object.

- Small Example to understand props

Folder Structure
```css
src/
  - App.jsx
  - Student.jsx
```
1️⃣ Student.jsx (Child Component)
```jsx
function Student(props) {
  return (
    <div>
      <h2>Name: {props.name}</h2>
      <p>Age: {props.age}</p>
      <p>Course: {props.course}</p>
    </div>
  );
}

export default Student;

yahaan:
- props ek object hai
- props.name, props.age etc use ho raha hai
```
2️⃣ App.jsx (Parent Component)
```jsx
import Student from "./Student";

function App() {
  return (
    <div>
      <h1>Student Details</h1>

      <Student 
        name="Manas" 
        age={21} 
        course="Computer Science" 
      />
    </div>
  );
}

export default App;

Yahan:
- Student component import hua
- Data props ke form me pass hua
```
Behind the Scenes (MOST IMPORTANT)
```js
Student({
  name: "Manas",
  age: 21,
  course: "Computer Science"
});
```
# React: State & Hooks – Short Notes

## 1️⃣ State in React

### Definition
**State** is a special data in React components that can change over time and updates the UI automatically.

**Key point:** Normal JS variables do not trigger re-render, but state does.

### Syntax (useState Hook)

```javascript
import { useState } from "react";

const [stateVariable, setStateFunction] = useState(initialValue);
```

- **stateVariable** → Current state value
- **setStateFunction** → Function to update state
- **initialValue** → Starting value of state

---

### Example 1: Counter

```javascript
import { useState } from "react";

function Counter() {
  const [count, setCount] = useState(0);

  return (
    <>
      <h1>Count: {count}</h1>
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </>
  );
}
```

✅ Clicking button updates state and UI automatically.

---

### Example 2: Object State

```javascript
const [user, setUser] = useState({ name: "Manas", age: 20 });

// Update age
setUser({ ...user, age: 21 });
```

---

### Example 3: Array State

```javascript
const [list, setList] = useState([]);

setList([...list, "New Item"]); // Add item
```

---

## 2️⃣ Hooks in React

### Definition
**Hooks** are special functions that let you use React features (state, lifecycle, context) inside functional components.

- **Introduced:** React 16.8
- **Rules:** Only use hooks at the top level of functional components, not inside loops or conditions.

---

### Common Hooks

| Hook | Purpose | Syntax |
|------|---------|--------|
| `useState` | Manage state | `const [state, setState] = useState(initialValue)` |
| `useEffect` | Lifecycle / side effects | `useEffect(() => { ... }, [dependencies])` |
| `useContext` | Access context | `const value = useContext(MyContext)` |
| `useRef` | DOM reference / mutable value | `const ref = useRef(initialValue)` |

---

### Example: useEffect

```javascript
import { useState, useEffect } from "react";

function Timer() {
  const [seconds, setSeconds] = useState(0);

  useEffect(() => {
    const interval = setInterval(() => setSeconds(s => s + 1), 1000);
    return () => clearInterval(interval); // cleanup
  }, []);

  return <h1>Seconds: {seconds}</h1>;
}
```

- Runs once on mount because dependency array `[]` is empty
- Updates UI every second automatically

---

## 3️⃣ Key Points

- **State** = data that changes and updates UI
- **Hooks** = functions to use React features in functional components
- **useState** → state management
- **useEffect** → side effects / lifecycle

# React: useRef() Hook – Short Notes

## 1️⃣ useRef() kya hai?

### Definition
**useRef()** ek Hook hai jo mutable reference create karta hai jo component ke re-render ke baad bhi persist karta hai.

### Important points

- **useState** ke opposite, ref update karne se component re-render **nahi** hota.

### Use cases

1. DOM element access karna directly
2. Value store karna jo render ke baad bhi rahe (without re-render)

---

### Syntax

```javascript
import { useRef } from "react";

const myRef = useRef(initialValue);
```

- **myRef.current** → actual value
- **initialValue** → starting value

---

## 2️⃣ useRef() kaise value persist karta hai

### Example: Render count track karna

```javascript
function Counter() {
  const renderCount = useRef(0); // useRef value
  renderCount.current += 1;

  console.log("Rendered:", renderCount.current);
  
  return <h1>Check console</h1>;
}
```

✅ **Result:**

- Har render ke baad `renderCount.current` apni value yaad rakhta hai
- Unlike normal `let` variable jo har render pe reset ho jaata hai

---

### Vs normal let variable

```javascript
function Counter() {
  let renderCount = 0;
  renderCount += 1;

  console.log("Rendered:", renderCount);

  return <h1>Check console</h1>;
}
```

❌ **Problem:**

- `let renderCount = 0` har render pe 0 se start hota hai
- Persist nahi hota

---

## 3️⃣ let vs useRef() ka table

| Feature | let | useRef() |
|---------|-----|----------|
| Value persist across renders | ❌ No | ✅ Yes |
| Re-render trigger karta hai? | ❌ No | ❌ No |
| DOM element store kar sakta hai? | ❌ No | ✅ Yes |

---

## 4️⃣ Example: Counter with render tracking

```javascript
import { useState, useRef } from "react";

function Counter() {
  const [count, setCount] = useState(0);
  const renderCount = useRef(0);

  renderCount.current += 1;

  return (
    <>
      <h1>Count: {count}</h1>
      <h2>Render Count: {renderCount.current}</h2>
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </>
  );
}
```

**Flow:**

- Button click → count change → component re-render
- `renderCount.current` increment hota hai aur value persist karti hai
- Agar `let` use karte → hamesha 1 dikhega har render pe

---

## 5️⃣ Key points yaad rakhne ke liye

- **useRef()** → persistent value store karta hai across renders
- **let** → har render pe reset ho jaata hai
- **useRef** → re-render nahi karta, unlike useState

### Best for:

- DOM reference
- Timer / interval
- Previous value store karna (`prevValue.current`)


**Example**
```jsx
import { useEffect, useRef, useState } from 'react'
import reactLogo from './assets/react.svg'
import viteLogo from '/vite.svg'
import './App.css'
import Navbar from './componets/navbar.jsx'

function App() {
  const [count, setCount] = useState(1)
  const a=useRef(0)
  useEffect(()=>{
    a.current=a.current+1;
    console.log(`rerendering and the value of a is : ${a.current}..`);
  });


  return (
    <>
    <Navbar color="cyan"/>
      <div>
        <h1>The count is : {count}</h1>
        <button onClick={()=>{setCount(count*2)}}>
          Increment Count
        </button>
      </div>
        
    </>
  )
}

export default App
```
So the output will print like -

![alt text](image.png)
