# Frontend Daily Drill Bible

**Your 60-Minute Daily Ritual to Ace U.S. Frontend Interviews**

📅 *Last Updated: April 25, 2025*

---

✨ **PRs are welcome!**
If this guide helped you, drop a ⭐ on the repo — it means a lot.
Wanna say thanks? Ping me or share it with a fellow frontend warrior.

---

This guide is your ultimate resource for mastering frontend development and excelling in interviews. It includes practical code examples and interview insights to help you grasp core concepts, write better code, and articulate answers confidently. Study daily to prepare for JavaScript, React, CSS, system design, Next.js, and more.

##  📚 Table of Contents

- [PART 1: JavaScript Core — The Foundation of Frontend](#part-1-javascript-core--the-foundation-of-frontend)
- [PART 2: DOM & Browser APIs](#part-2-dom--browser-apis)
- [PART 3: CSS & Layout](#part-3-css--layout)
- [PART 4: React Fundamentals](#part-4-react-fundamentals)
- [PART 5: State Management](#part-5-state-management)
- [PART 6: Next.js Rendering Strategies](#part-6-nextjs-rendering-strategies)
- [PART 7: Web Performance Optimization](#part-7-web-performance-optimization)
- [PART 8: Security Fundamentals](#part-8-security-fundamentals)
- [PART 9: Software Design Principles](#part-9-software-design-principles)
- [PART 10: Accessibility & Semantic HTML](#part-10-accessibility--semantic-html)
- [PART 11: Common Pitfalls & Best Practices](#part-11-common-pitfalls--best-practices)
- [PART 12: Modern Frontend Architecture](#part-12-modern-frontend-architecture)
- [PART 13: Modern State Management](#part-13-modern-state-management)
- [PART 14: Modern Performance Optimization](#part-14-modern-performance-optimization)
- [PART 15: Modern Testing Approaches](#part-15-modern-testing-approaches)
- [PART 16: Modern CSS Features](#part-16-modern-css-features)
- [PART 17: Modern Build Tools](#part-17-modern-build-tools)
- [PART 18: Modern React Patterns](#part-18-modern-react-patterns)
- [PART 19: Modern API Patterns](#part-19-modern-api-patterns)
- [PART 20: Modern Development Practices](#part-20-modern-development-practices)
- [PART 21: Modern Tooling & TypeScript](#part-21-modern-tooling--typescript)
- [PART 22: AI Integration in Frontend](#part-22-ai-integration-in-frontend)
- [PART 23: Modern Security Practices](#part-23-modern-security-practices)

---

## PART 1: JavaScript Core — The Foundation of Frontend

JavaScript is the language of the web. Understanding its types, scope, and async behavior is essential for interviews and real-world work.

### JavaScript Data Types

JavaScript has two main categories of data types: primitives and objects.

#### Primitives

Primitives are the most basic data types. They include:

| Type      | Description                          | Example                            |
| --------- | ------------------------------------ | ---------------------------------- |
| Number    | Integers, floats, Infinity, NaN      | `let num = 42;`                    |
| String    | Sequence of characters               | `let str = "Hello";`               |
| Boolean   | true or false                        | `let isTrue = true;`               |
| BigInt    | Large integers beyond Number's limit | `let big = 12345678901234567890n;` |
| Null      | Explicit "no value"                  | `let nothing = null;`              |
| Undefined | Variable not assigned                | `let undeclared;`                  |
| Symbol    | Unique, immutable keys               | `let sym = Symbol("id");`          |

**Key Points:**

- Primitives are immutable: you can't change them in place. Any "change" creates a new value.
- When you assign a primitive to another variable, it copies the value (not a reference).
- `typeof null` returns "object" (historical bug); `NaN` is a Number, check with `Number.isNaN()`.

**Example:**

```js
let a = 10;
let b = a;
b = 20;
console.log(a); // 10 (a is unchanged)
```

#### Objects and Arrays

Objects and arrays are reference types. When you assign them to another variable, both variables point to the same object in memory.

**Example:**

```js
let arr = [1, 2, 3];
let arr2 = arr;
arr2[0] = 100;
console.log(arr); // [100, 2, 3] (arr is changed)
```

**Interview Tip:**
Be ready to explain the difference between `null` and `undefined`, and why `typeof null` returns `"object"` (it's a historical bug).

### Truthy & Falsy Values

Some values in JavaScript are considered "falsy" (they behave like false in a boolean context), while everything else is "truthy".

**Falsy values:** `0`, `""`, `undefined`, `null`, `NaN`, `false`
**Truthy values:** Everything else (e.g., `"0"`, `[]`, `{}`)

**Example:**

```js
if (0) {
  console.log('Nope');
} // Falsy, won't run
if ('0') {
  console.log('Yup');
} // Truthy, runs
```

**Interview Tip:**
Use explicit checks (e.g., `if (x === 0)`) to avoid bugs with truthy/falsy values.

### == vs === (Equality)

- `==` checks for value equality with type coercion (not recommended)
- `===` checks for value and type equality (always use this)

**Example:**

```js
console.log(0 == '0'); // true
console.log(0 === '0'); // false
```

### typeof and Type Checking

- `typeof` returns a string describing the type (e.g., "number", "string")
- `typeof null` returns "object" (historical bug)
- Use `instanceof` or `Array.isArray()` for objects/arrays

**Example:**

```js
console.log(typeof 42); // "number"
console.log(typeof null); // "object"
console.log(Array.isArray([])); // true

// Using instanceof
class Animal {}
class Dog extends Animal {}

const myDog = new Dog();
console.log(myDog instanceof Dog); // true
console.log(myDog instanceof Animal); // true
console.log(myDog instanceof Array); // false
```

### Variable Scope

JavaScript has function, block, and global scope. `let` and `const` are block-scoped, `var` is function-scoped.

**Example:**

```js
let globalVar = "I'm global";
function outer() {
  let localVar = "I'm local";
  if (true) {
    let blockVar = "I'm block-scoped";
    console.log(localVar); // ✅ Accessible (inside the same function)
  }
  console.log(blockVar); // ❌ ReferenceError
}
```

### Hoisting

- `var` and function declarations are hoisted (moved to the top of their scope)
- `let` and `const` are hoisted but not initialized (temporal dead zone)

**Example:**

```js
console.log(x); // undefined
var x = 5;
sayHi(); // Works
function sayHi() {
  console.log('Hi');
}
// console.log(y); // ReferenceError
let y = 10;
```

### Closures

A closure is a function that "remembers" variables from its outer scope, even after that scope has finished executing.

**Example:**

```js
function counter() {
  let count = 0;
  return function increment() {
    return ++count;
  };
}
const myCounter = counter();
console.log(myCounter()); // 1
console.log(myCounter()); // 2
```

**Interview Tip:**
Closures are used for data privacy and to create functions with persistent state.

### The `this` Keyword

- In a method, `this` refers to the object
- In a function (non-strict mode), `this` is the global object
- In an arrow function, `this` is inherited from the parent scope

**Example:**

```js
const obj = {
  name: 'Grok',
  greet() {
    console.log(this.name);
  },
};
obj.greet(); // "Grok"
const fn = obj.greet;
fn(); // undefined (or window.name in browsers)
```

### Prototypal Inheritance

Objects in JavaScript inherit from other objects via the prototype chain.

**Example:**

```js
function Animal(name) {
  this.name = name;
}
Animal.prototype.speak = function () {
  console.log(`${this.name} speaks`);
};
const dog = new Animal('Rex');
dog.speak(); // "Rex speaks"
```

### The Event Loop

JavaScript is single-threaded, meaning it can only execute one task at a time. However, it can handle asynchronous operations using the event loop, which allows non-blocking execution.

#### How the Event Loop Works

1. **Call Stack:** This is where JavaScript keeps track of function calls. It executes functions in a last-in, first-out order.
2. **Web APIs:** Asynchronous operations like setTimeout, fetch, and DOM events are handled outside the call stack in the browser's Web APIs.
3. **Task Queue (Macrotasks):** Once an asynchronous operation completes, its callback is placed in the task queue, waiting for the call stack to be empty.
4. **Microtask Queue:** Promises and other microtasks are placed in this queue, which has higher priority than the task queue.
5. **Event Loop:** Continuously checks if the call stack is empty and then processes tasks from the microtask queue first, followed by the task queue.

#### Example with Code

Let's see how the event loop processes different tasks:

```js
console.log('Start');

setTimeout(() => {
  console.log('Timeout');
}, 0);

Promise.resolve().then(() => {
  console.log('Promise');
});

console.log('End');
```

**Output Explanation:**

- **Step 1:** 'Start' is logged first because it's a synchronous operation in the call stack.
- **Step 2:** 'End' is logged next, as it's also synchronous and follows 'Start'.
- **Step 3:** The promise's `.then()` callback is a microtask, so 'Promise' is logged before 'Timeout', even though setTimeout was called first.
- **Step 4:** 'Timeout' is logged last because setTimeout is a macrotask, which is processed after the microtask queue is empty.

**Why This Order?**

- The event loop prioritizes the microtask queue over the task queue, ensuring that promises are resolved before moving on to macrotasks like setTimeout.

This mechanism allows JavaScript to handle asynchronous operations efficiently, providing a smooth user experience without blocking the main thread.

### Promises and async/await

Promises represent the result of an async operation. `async/await` makes working with promises easier.

**Example:**

```js
fetch('https://api.example.com/data')
  .then((resp) => resp.json())
  .then((data) => console.log(data))
  .catch((err) => console.error(err));

// With async/await
async function getData() {
  try {
    const resp = await fetch('https://api.example.com/data');
    if (!resp.ok) throw new Error(resp.statusText);
    return await resp.json();
  } catch (err) {
    console.error(err);
  }
}
```

**Interview Tip:**
Be ready to trace the order of output for event loop questions, and explain how closures and `this` work in different contexts.

### Function Declarations, Expressions, and Arrow Functions

Understanding the differences between function declarations, function expressions, and arrow functions is crucial for writing flexible and efficient JavaScript code.

- **Function Declarations:** These are hoisted, meaning they can be called before they are defined in the code. They are defined with the `function` keyword.

  **Example:**

  ```js
  function greet() {
    console.log('Hello');
  }
  greet(); // Can be called before its definition
  ```

- **Function Expressions:** These are not hoisted, so they cannot be called before they are defined. They can be anonymous or named and are often assigned to variables.

  **Example:**

  ```js
  const greet = function () {
    console.log('Hello');
  };
  greet(); // Must be called after its definition
  ```

- **Arrow Functions:** Introduced in ES6, they provide a more concise syntax and do not have their own `this` context, which makes them ideal for methods that do not require their own `this` or for callbacks.

  **Example:**

  ```js
  const greet = () => {
    console.log('Hello');
  };
  greet(); // Concise syntax, no own `this`
  ```

**Key Differences:**

- **Hoisting:** Function declarations are hoisted, while function expressions and arrow functions are not.
- **`this` Context:** Arrow functions do not have their own `this` context, making them unsuitable for methods that need to access the object they belong to.
- **Syntax:** Arrow functions offer a shorter syntax, especially useful for inline functions or callbacks.

### Difference Between Async/Await and .then()

Both `async/await` and `.then()` are used to handle promises in JavaScript, but they offer different approaches and benefits.

- **Syntax and Readability:**

  - **Async/Await:** Provides a more synchronous-looking code structure, making it easier to read and understand, especially for complex promise chains.
  - **.then():** Uses a chaining approach, which can become less readable with multiple nested promises.

- **Error Handling:**

  - **Async/Await:** Uses `try/catch` blocks for error handling, which is more intuitive and similar to synchronous code.
  - **.then():** Requires a `.catch()` method to handle errors, which can be less straightforward when dealing with multiple promises.

- **Control Flow:**

  - **Async/Await:** Allows for writing asynchronous code in a linear, top-to-bottom manner, which is easier to follow.
  - **.then():** Involves chaining, which can lead to more complex control flow, especially with multiple asynchronous operations.

- **Use Cases:**
  - **Async/Await:** Ideal for scenarios where you have multiple asynchronous operations that need to be executed in sequence, and you want to maintain readability.
  - **.then():** Suitable for simple promise handling or when you need to perform operations in parallel, as each `.then()` can return a new promise.

**Example Comparison:**

- **Async/Await:**

  ```js
  async function fetchData() {
    try {
      const response = await fetch('https://api.example.com/data');
      const data = await response.json();
      console.log(data);
    } catch (error) {
      console.error('Error fetching data:', error);
    }
  }
  fetchData();
  ```

- **.then():**
  ```js
  fetch('https://api.example.com/data')
    .then((response) => response.json())
    .then((data) => console.log(data))
    .catch((error) => console.error('Error fetching data:', error));
  ```

---

## PART 2: DOM & Browser APIs

The DOM (Document Object Model) and browser APIs are essential for interacting with web pages. Understanding how to manipulate the DOM, use browser storage, and make network requests is key for frontend interviews and real-world work.

### Promises and the Event Loop

Promises are a way to handle asynchronous operations in JavaScript, allowing you to write cleaner and more manageable code. They work in conjunction with the event loop to handle operations that take time, like network requests.

- **Promises:** A promise represents a value that may be available now, or in the future, or never. They allow you to attach callbacks for success or failure.

  **Example:**

  ```js
  const promise = new Promise((resolve, reject) => {
    setTimeout(() => resolve('Success!'), 1000);
  });
  promise.then((result) => console.log(result));
  ```

- **setTimeout:** This function is used to delay the execution of a function. It is a macrotask in the event loop, meaning it runs after the current stack and microtasks (like promises) are completed.

- **Event Loop and Promises:** The event loop processes the call stack, then microtasks (like promises), and finally macrotasks (like setTimeout). This order ensures that promises are resolved before any setTimeout callbacks.

  **Example:**

  ```js
  console.log('Start');
  setTimeout(() => console.log('Timeout'), 0);
  Promise.resolve().then(() => console.log('Promise'));
  console.log('End');
  // Output: Start, End, Promise, Timeout
  ```

### Async/Await Syntax

The async/await syntax is a more readable way to work with promises, introduced in ES2017. It allows you to write asynchronous code that looks synchronous, making it easier to understand and maintain.

- **Async Functions:** Declaring a function with `async` allows you to use `await` inside it, pausing execution until the promise is resolved.

- **Await Keyword:** Used to wait for a promise to resolve. It can only be used inside an async function.

  **Example:**

  ```js
  async function fetchData() {
    try {
      const response = await fetch('https://api.example.com/data');
      const data = await response.json();
      console.log(data);
    } catch (error) {
      console.error('Error fetching data:', error);
    }
  }
  fetchData();
  ```

**Why Async/Await Exists:**

- **Before Async/Await:** Asynchronous code was primarily handled using callbacks, leading to complex and hard-to-read code known as "callback hell."
- **Improvement:** Async/await provides a cleaner and more intuitive way to handle asynchronous operations, reducing the complexity and improving code readability.

### What is the DOM?

The DOM is a tree-like structure representing the HTML of a web page. JavaScript can use the DOM to read, change, add, or remove elements.

**Example:**

```js
const div = document.createElement('div');
div.textContent = 'Hello';
document.body.appendChild(div);
```

### DOM Manipulation & Performance

- Minimize direct DOM updates for better performance.
- Batch changes when possible.
- Use `document.createDocumentFragment` for bulk updates to avoid repeated reflows.

**Example:**

```js
const fragment = document.createDocumentFragment();
for (let i = 0; i < 100; i++) {
  const li = document.createElement('li');
  li.textContent = `Item ${i}`;
  fragment.appendChild(li);
}
document.querySelector('ul').appendChild(fragment);
```

**Interview Tip:**
Frequent DOM updates can slow down your app. Batch changes and minimize layout thrashing.

### Browser Storage

Browsers provide several ways to store data on the client:

- **Cookies:** Small, sent with every HTTP request. Used for authentication and tracking.
- **sessionStorage:** Stores data for one tab/session. Cleared when the tab closes.
- **localStorage:** Stores data with no expiration. Shared across tabs for the same origin.

**Example:**

```js
localStorage.setItem('theme', 'dark');
sessionStorage.setItem('temp', 'data');
document.cookie = 'user=John; Secure; HttpOnly';
```

### Fetch API

The Fetch API is the modern way to make HTTP requests in the browser. It returns a promise and supports async/await.

**Example:**

```js
async function fetchData() {
  const resp = await fetch('https://api.example.com/data');
  if (!resp.ok) throw new Error(resp.statusText);
  return await resp.json();
}
```

### CORS (Cross-Origin Resource Sharing)

CORS is a browser security feature that restricts requests to different origins unless the server allows it. If you see CORS errors, the server needs to send the right headers.

**Example (Node.js/Express):**

```js
app.use((req, res, next) => {
  res.setHeader('Access-Control-Allow-Origin', 'https://client.com');
  res.setHeader('Access-Control-Allow-Methods', 'GET, POST');
  next();
});
```

**Interview Tip:**
Be ready to explain what a preflight OPTIONS request is and why CORS errors happen.

---

## PART 3: CSS & Layout

CSS controls the look and layout of web pages. Understanding the box model, positioning, and layout systems is essential for building and debugging UIs.

### The Box Model

Every element is a box made up of content, padding, border, and margin.

- **Content:** The actual content (text, image, etc.)
- **Padding:** Space between content and border
- **Border:** The line around the padding
- **Margin:** Space outside the border

**Example:**

```css
div {
  width: 100px;
  padding: 10px;
  border: 2px solid;
  margin: 20px;
}
```

### CSS Specificity

Specificity determines which CSS rule applies if multiple rules match the same element. Inline styles > IDs > Classes/Attributes/Pseudo-classes > Elements.

**Example:**

```css
#myId {
  color: red;
} /* Wins */
div {
  color: blue;
}
```

**Interview Tip:**
Keep specificity low to avoid using `!important` and make your CSS easier to maintain.

### Flexbox and Grid

- **Flexbox:** One-dimensional layout (row or column). Great for aligning items in a row or column.
- **Grid:** Two-dimensional layout (rows and columns). Great for complex layouts.

**Example:**

```css
.container {
  display: flex;
  justify-content: space-between;
}
.grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
}
```

### Centering Elements

- **Flexbox:** `justify-content: center; align-items: center;`
- **Grid:** `place-items: center;`
- **Absolute:** `top: 50%; left: 50%; transform: translate(-50%, -50%);`

**Example:**

```css
.parent {
  display: flex;
  justify-content: center;
  align-items: center;
}
```

### Positioning

- **Static:** Default, follows normal flow
- **Relative:** Offset from normal position
- **Absolute:** Positioned relative to nearest ancestor with position
- **Sticky:** Sticks within parent when scrolling
- **Fixed:** Sticks to viewport

**Example:**

```css
.absolute {
  position: absolute;
  top: 10px;
}
```

### Responsive Design

- Use mobile-first styles and media queries
- Use relative units (`rem`, `vw`, `%`)
- Always include `<meta name="viewport" content="width=device-width, initial-scale=1">`

**Example:**

```css
body {
  font-size: 16px;
}
@media (min-width: 768px) {
  body {
    font-size: 18px;
  }
}
```

**Interview Tip:**
Be ready to explain how to make a layout responsive and how to center elements in different ways.

---

## PART 4: React Fundamentals

React is a popular library for building user interfaces. Understanding components, state, props, and hooks is essential for interviews and real-world React work.

### Key React Concepts

- **Components:** Reusable UI blocks (functions or classes)
- **JSX:** HTML-like syntax in JavaScript
- **State:** Data that changes over time, managed by the component
- **Props:** Data passed to components from parents (read-only)
- **Side Effects:** Operations like fetching data, handled with hooks

**Example:**

```js
function Hello({ name }) {
  return <h1>Hello, {name}</h1>;
}
```

### Virtual DOM

React uses a virtual DOM to efficiently update the real DOM. It compares the new virtual DOM with the previous one and updates only what changed.

### React Hooks

React Hooks allow you to use state and other React features in functional components, making them more powerful and flexible.

- **useState:** Use this hook to add local state to a functional component. It's ideal for managing simple state like form inputs or toggles. For example, use `useState` to track whether a modal is open or closed.

  **Example:**

  ```js
  const [isOpen, setIsOpen] = useState(false);
  const toggleModal = () => setIsOpen(!isOpen);
  ```

- **useEffect:** This hook is perfect for handling side effects such as data fetching, subscriptions, or manually changing the DOM. For instance, use `useEffect` to fetch data from an API when a component mounts or to set up a subscription to a data source.

  **Example:**

  ```js
  useEffect(() => {
    fetch('/api/data')
      .then((response) => response.json())
      .then((data) => console.log(data));
  }, []); // Empty dependency array means this runs once on mount
  ```

- **useRef:** Use `useRef` to persist values across renders without causing a re-render. It's commonly used for accessing DOM elements directly or storing mutable values like timers. For example, use `useRef` to keep a reference to an input element for focusing it programmatically.

  **Example:**

  ```js
  const inputRef = useRef(null);
  const focusInput = () => inputRef.current.focus();
  ```

- **useContext:** This hook is used to access global data provided by a React context. It's useful for themes, user authentication, or any data that needs to be accessible throughout the component tree. For example, use `useContext` to access the current theme in a deeply nested component.

  **Example:**

  ```js
  const theme = useContext(ThemeContext);
  console.log(`Current theme is ${theme}`);
  ```

- **useReducer:** Opt for `useReducer` when you have complex state logic that involves multiple sub-values or when the next state depends on the previous one. It's similar to `useState` but more suitable for managing state transitions in a predictable way, like in a form with multiple inputs.

  **Example:**

  ```js
  const initialState = { count: 0 };
  function reducer(state, action) {
    switch (action.type) {
      case 'increment':
        return { count: state.count + 1 };
      case 'decrement':
        return { count: state.count - 1 };
      default:
        throw new Error();
    }
  }
  const [state, dispatch] = useReducer(reducer, initialState);
  ```

- **useMemo:** Use this hook to memoize expensive calculations so that they are only recomputed when necessary. It's beneficial for optimizing performance in components with heavy computations or when passing props to child components that rely on reference equality.

  **Example:**

  ```js
  const memoizedValue = useMemo(() => computeExpensiveValue(a, b), [a, b]);
  ```

- **useCallback:** Similar to `useMemo`, `useCallback` memoizes functions to prevent unnecessary re-creations on every render. It's particularly useful when passing callbacks to optimized child components that rely on reference equality to prevent re-renders.

  **Example:**

  ```js
  const memoizedCallback = useCallback(() => {
    doSomething(a, b);
  }, [a, b]);
  ```

### useEffect vs useLayoutEffect

- `useEffect`: Runs after the DOM is painted (async)
- `useLayoutEffect`: Runs before the DOM is painted (sync, for measurements)

### State Immutability

Never mutate state directly. Always create a new object or array to trigger re-renders.

**Example:**

```js
const [items, setItems] = useState([]);
setItems([...items, newItem]); // Correct
// items.push(newItem); // Wrong
```

### Keys in Lists

Always use a unique, stable key for each item in a list to help React track changes.

**Example:**

```js
{
  items.map((item) => <li key={item.id}>{item.name}</li>);
}
```

### Performance Optimizations

- `React.memo`: Prevents unnecessary re-renders
- `useMemo`/`useCallback`: Memoize values/functions
- `React.lazy` + `<Suspense>`: Lazy-load components
- Virtualize long lists (e.g., react-window)

**Example:**

```js
const Memoized = React.memo(({ data }) => <div>{data}</div>);
const LazyComponent = React.lazy(() => import('./Component'));
```

### Controlled vs Uncontrolled Components

- **Controlled:** React manages the value (state-driven)
- **Uncontrolled:** DOM manages the value (use refs)

**Example:**

```js
function ControlledInput() {
  const [value, setValue] = useState('');
  return <input value={value} onChange={(e) => setValue(e.target.value)} />;
}
```

**Interview Tip:**
Be ready to explain the difference between controlled and uncontrolled components, and how to optimize React performance.

---

## PART 5: State Management

State management is how you keep track of and update data in your app. For small apps, local state is enough. For larger apps, you may need global state or a library like Redux.

### State Management Approaches

| Approach     | Description                         | Example                |
| ------------ | ----------------------------------- | ---------------------- |
| Local State  | Component-specific                  | `useState("light")`    |
| Global State | App-wide via Context                | `createContext()`      |
| Redux        | Complex state with actions/reducers | `createStore(reducer)` |

**Example:**

```js
// Local State
function ThemeToggle() {
  const [theme, setTheme] = useState('light');
  return (
    <button onClick={() => setTheme(theme === 'light' ? 'dark' : 'light')}>
      Toggle
    </button>
  );
}

// Context API
const ThemeContext = createContext();
function App() {
  return (
    <ThemeContext.Provider value="dark">
      <ThemeToggle />
    </ThemeContext.Provider>
  );
}
```

### Context vs Prop Drilling

Prop drilling occurs when you pass data through many layers of components to reach a deeply nested component. This can lead to code that is difficult to maintain and understand.

#### Why Prop Drilling is Considered Bad

- **Complexity:** As your component tree grows, passing props through multiple layers can make your codebase complex and hard to follow.
- **Maintenance:** Changes to the data structure or the components that need the data can require updates in multiple places, increasing the risk of bugs.
- **Readability:** It becomes challenging to track where data is coming from and how it is being used, reducing the readability of your code.

#### Solution: Context API and Global State Management

The Context API, along with other global state management tools like Redux or Zustand, can help manage state across your application without the need for prop drilling.

- **Centralized State:** These tools allow you to store state in a central location, making it accessible to any component that needs it without passing props through multiple layers.
- **Improved Readability:** By reducing the need for prop drilling, your code becomes more readable and easier to understand.
- **Ease of Maintenance:** With a centralized state, you can make changes in one place, reducing the risk of bugs and making your code easier to maintain.

Using the Context API or other global state management solutions can significantly improve the structure and maintainability of your application, especially as it grows in complexity.

### Keys in Lists

Always use a unique, stable key for each item in a list to help React track changes.

**Example:**

```js
{
  items.map((item) => <li key={item.id}>{item.name}</li>);
}
```

### Performance Optimizations

- `React.memo`: Prevents unnecessary re-renders
- `useMemo`/`useCallback`: Memoize values/functions
- `React.lazy` + `<Suspense>`: Lazy-load components
- Virtualize long lists (e.g., react-window)

**Example:**

```js
const Memoized = React.memo(({ data }) => <div>{data}</div>);
const LazyComponent = React.lazy(() => import('./Component'));
```

### Controlled vs Uncontrolled Components

- **Controlled:** React manages the value (state-driven)
- **Uncontrolled:** DOM manages the value (use refs)

**Example:**

```js
function ControlledInput() {
  const [value, setValue] = useState('');
  return <input value={value} onChange={(e) => setValue(e.target.value)} />;
}
```

**Interview Tip:**
Be ready to explain the difference between controlled and uncontrolled components, and how to optimize React performance.

---

## PART 6: Next.js Rendering Strategies

Next.js supports multiple ways to render pages, each with trade-offs for SEO, speed, and data freshness.

### Rendering Types

| Strategy | Description                         | Example                            |
| -------- | ----------------------------------- | ---------------------------------- |
| SSG      | Static Site Generation (build time) | `getStaticProps`                   |
| SSR      | Server-Side Rendering (per request) | `getServerSideProps`               |
| ISR      | Incremental Static Regeneration     | `getStaticProps` with `revalidate` |
| PPR      | Partial Pre-rendering (Next.js 15+) | Dynamic rendering of changed parts |

**Example:**

```js
// SSG
export async function getStaticProps() {
  const data = await fetchData();
  return { props: { data } };
}

// SSR
export async function getServerSideProps() {
  const data = await fetchData();
  return { props: { data } };
}

// ISR
export async function getStaticProps() {
  const data = await fetchData();
  return { props: { data }, revalidate: 60 };
}
```

**Interview Tip:**
Be ready to discuss when to use SSG, SSR, ISR, or PPR, and the trade-offs for SEO, speed, and dynamic data.

---

## PART 7: Web Performance Optimization

Fast websites provide a better user experience and rank higher in search engines. Know how to optimize loading, rendering, and interactivity.

### Best Practices

- Lazy-load images (`loading="lazy"`) and code (`React.lazy`)
- Use async/defer for scripts
- Reduce bundle size (tree-shaking)
- Code-split routes/components

**Example:**

```js
const LazyComponent = React.lazy(() => import('./Component'));
<Suspense fallback={<div>Loading...</div>}>
  <LazyComponent />
</Suspense>;
```

### Debounce vs Throttle

- **Debounce:** Waits until input stops before running a function (e.g., search box)
- **Throttle:** Limits a function to run at most once per interval (e.g., scroll events)

**Example:**

```js
function debounce(fn, delay) {
  let timer;
  return (...args) => {
    clearTimeout(timer);
    timer = setTimeout(() => fn(...args), delay);
  };
}
```

### Critical Rendering Path

- Inline critical CSS for faster first paint
- Defer non-critical JavaScript

### Image Optimization

- Use modern formats (WebP, AVIF)
- Use `srcset` for responsive images
- Use `loading="lazy"` for offscreen images

**Example:**

```html
<img src="small.jpg" srcset="large.jpg 2x" loading="lazy" alt="Description" />
```

**Interview Tip:**
Be ready to explain how to improve Core Web Vitals (LCP, FID, CLS) and why performance matters for users and SEO.

---

## PART 8: Security Fundamentals

Security is essential for protecting users and data. Know the basics of XSS, CSRF, CORS, and secure cookies.

### XSS, CSRF, and CORS

- **XSS (Cross-Site Scripting):** Sanitize user input, use Content Security Policy (CSP)
- **CSRF (Cross-Site Request Forgery):** Use anti-forgery tokens, SameSite cookies
- **CORS (Cross-Origin Resource Sharing):** Server must allow cross-origin requests

**Example:**

```html
<meta http-equiv="Content-Security-Policy" content="default-src 'self'" />
```

### HTTPS & Secure Cookies

- Always use HTTPS
- Set cookies as Secure, HttpOnly, and SameSite

**Example:**

```js
document.cookie = 'user=John; Secure; HttpOnly; SameSite=Strict';
```

**Interview Tip:**
Be ready to explain what XSS and CSRF are, and how to prevent them in a React or Next.js app.

---

## PART 9: Software Design Principles

System design is about structuring your app for scalability, maintainability, and performance.

### SPA vs MPA

- **SPA (Single Page App):** One HTML file, dynamic routing (React, Vue, etc.)
- **MPA (Multi Page App):** Each route is a separate HTML file, full page reloads

### SSR vs CSR

- **SSR (Server-Side Rendering):** HTML is rendered on the server, better for SEO and initial load
- **CSR (Client-Side Rendering):** HTML is rendered in the browser, better for interactivity

### Modular Architecture

- Use design systems for reusable components
- Organize code by feature (feature folders)

**Example:**

```
/components/Button.js
/features/auth/Login.js
/utils/api.js
```

### State Management Choices

- **Redux:** For complex, large-scale apps
- **Context:** For simple global state
- **Zustand:** Lightweight alternative

### SEO for SPAs

- Use SSR or prerendering for better SEO
- Add dynamic meta tags for each page

**Example:**

```js
<Helmet>
  <title>My Page</title>
  <meta name="description" content="My app" />
</Helmet>
```

**Interview Tip:**
Be ready to explain how you would structure a large React app, and how to make an SPA SEO-friendly.

### Software Design Principles

#### SOLID Principles

- **Single Responsibility Principle (SRP):** A class should have only one reason to change, meaning it should have only one job.

  - _Real-World Example:_ Imagine a restaurant where the chef is responsible for cooking, taking orders, and cleaning. This can lead to inefficiencies and errors. Similarly, in software, if a class handles multiple responsibilities, changes in one area can affect others, leading to bugs and maintenance challenges.

- **Open/Closed Principle (OCP):** Software entities should be open for extension but closed for modification.

  - _Real-World Example:_ Consider a smartphone that allows you to install new apps without altering the core operating system. This flexibility allows for new features without risking the stability of existing ones.

- **Liskov Substitution Principle (LSP):** Objects of a superclass should be replaceable with objects of a subclass without affecting the correctness of the program.

  - _Real-World Example:_ Think of a universal remote control that can replace any specific brand's remote without losing functionality. In software, this ensures that derived classes can stand in for their base classes without causing errors.

- **Interface Segregation Principle (ISP):** Clients should not be forced to depend on interfaces they do not use.

  - _Real-World Example:_ Imagine a multi-tool with too many functions, making it cumbersome to use for simple tasks. In software, large interfaces can lead to unnecessary dependencies and complexity.

- **Dependency Inversion Principle (DIP):** High-level modules should not depend on low-level modules. Both should depend on abstractions.
  - _Real-World Example:_ Consider a car's dashboard that interacts with the engine through a standard interface, allowing the engine to be replaced or upgraded without redesigning the dashboard. This separation of concerns enhances flexibility and maintainability.

**Example:**

```js
// SRP Example
class Report {
  generate() {
    // generate report
  }
}

class ReportPrinter {
  print(report) {
    // print report
  }
}
```

### DRY Principle

- **Don't Repeat Yourself (DRY):** Avoid code duplication by abstracting common logic into functions or modules.

**Example:**

```js
function calculateArea(width, height) {
  return width * height;
}

const area1 = calculateArea(5, 10);
const area2 = calculateArea(7, 3);
```

### Other Popular Concepts

- **KISS (Keep It Simple, Stupid):** Simplicity should be a key goal in design, and unnecessary complexity should be avoided.
- **YAGNI (You Aren't Gonna Need It):** Don't add functionality until it is necessary.

### Database Technologies

#### SQL vs NoSQL

- **SQL Databases:**

  - **Description:** SQL databases are relational databases that use structured query language (SQL) for defining and manipulating data. They are based on a table-based schema and are best suited for structured data with relationships.
  - **Advantages:**
    - Strong ACID compliance ensures data integrity and reliability.
    - Powerful query capabilities for complex joins and aggregations.
    - Mature ecosystem with extensive tools and community support.
  - **Disadvantages:**
    - Less flexible in handling unstructured data.
    - Vertical scaling can be costly and complex.
  - **Use Cases:** Financial systems, enterprise resource planning (ERP), customer relationship management (CRM), and applications requiring complex queries and transactions.

- **NoSQL Databases:**
  - **Description:** NoSQL databases are designed for unstructured data and can handle large volumes of data with high velocity. They are schema-less and provide flexibility in data modeling, often using key-value, document, column-family, or graph structures.
  - **Advantages:**
    - Highly scalable, supporting horizontal scaling across distributed systems.
    - Flexible data models allow for rapid development and iteration.
    - Suitable for handling large volumes of unstructured or semi-structured data.
  - **Disadvantages:**
    - Eventual consistency model may not be suitable for all applications.
    - Limited support for complex queries and transactions compared to SQL databases.
  - **Use Cases:** Real-time analytics, content management systems, IoT applications, and applications with rapidly changing data structures.

**Key Differences:**

- **Schema:** SQL databases have a fixed schema, while NoSQL databases are schema-less, allowing for more flexible data models.
- **Scalability:** SQL databases are typically vertically scalable, whereas NoSQL databases are designed for horizontal scalability across distributed systems.
- **Transactions:** SQL databases support ACID transactions, ensuring strong consistency, while NoSQL databases often use eventual consistency models, prioritizing availability and partition tolerance.

---

## PART 10: Accessibility & Semantic HTML

Accessibility ensures your app works for everyone, including people with disabilities. Semantic HTML helps browsers and assistive tech understand your content.

### Semantic HTML

Use elements that describe their meaning (e.g., `<header>`, `<nav>`, `<main>`, `<article>`, `<button>`). This improves accessibility and SEO.

**Example:**

```html
<main>
  <article>
    <h1>Title</h1>
    <p>Content goes here.</p>
  </article>
</main>
```

### Alt Text

Always provide meaningful `alt` text for images. Use `alt=""` for decorative images.

### ARIA Roles & Labels

Use ARIA attributes when native HTML is not enough. For example, to make a `div` act as a button:

**Example:**

```html
<div role="button" aria-label="Close" tabindex="0">X</div>
```

### Color Contrast & Focus

- Ensure text has enough contrast (WCAG 4.5:1 minimum)
- Make sure focus outlines are visible for keyboard users

**Interview Tip:**
Be ready to explain how to make a component accessible and why semantic HTML matters for users and SEO.

---

## PART 11: Common Pitfalls & Best Practices

- Always use `===` instead of `==` for comparisons
- Use event delegation for performance
- Clean up timers and event listeners in components
- Never mutate state directly
- Use stable keys in lists
- Avoid global variables
- Use web workers for heavy computations
- Don't skip accessibility
- Avoid `!important` in CSS
- Remove console logs in production
- Use environment variables for configuration

**Interview Tip:**
Be ready to discuss common mistakes in React, JavaScript, and CSS, and how to avoid them.

---

## PART 12: Modern Frontend Architecture

Modern frontend apps use advanced patterns for scalability and performance. Know the basics of micro-frontends, islands architecture, and edge computing.

### Micro-frontends

Split large apps into smaller, independently deployable pieces. Use Module Federation to share code between apps.

**Example:**

```js
// webpack.config.js
module.exports = {
  plugins: [
    new ModuleFederationPlugin({
      name: 'host',
      remotes: {
        shop: 'shop@http://localhost:3001/remoteEntry.js',
      },
      shared: ['react', 'react-dom'],
    }),
  ],
};
```

### Islands Architecture

Render static HTML for most of the page, hydrate only interactive parts. Great for content-heavy sites.

**Example (Astro):**

```js
---
import InteractiveCounter from './Counter.jsx';
---
<html>
  <body>
    <h1>Static Content</h1>
    <InteractiveCounter client:visible />
  </body>
</html>
```

### Edge Computing

Run code close to users for lower latency and better performance. Use edge functions in Next.js or similar frameworks.

**Example:**

```js
export const config = { runtime: 'edge' };
export default async function handler(req) {
  const geo = req.geo;
  return new Response(
    JSON.stringify({
      location: geo.city,
      content: await getLocalizedContent(geo.country),
    })
  );
}
```

---

## PART 13: Modern State Management

Modern state management focuses on simplicity and performance. Learn about signals and server state libraries.

### Signals

Signals are reactive primitives for fine-grained updates (e.g., Preact, SolidJS).

**Example:**

```js
import { signal, computed } from '@preact/signals-react';
const count = signal(0);
const doubled = computed(() => count.value * 2);
function Counter() {
  return (
    <button onClick={() => count.value++}>
      Count: {count} (Doubled: {doubled})
    </button>
  );
}
```

### Server State (TanStack Query)

Use libraries like TanStack Query or SWR to manage server data, caching, and background updates.

**Example:**

```js
function TodoList() {
  const { data, isLoading } = useQuery({
    queryKey: ['todos'],
    queryFn: fetchTodos,
    staleTime: 5000,
    cacheTime: 300000,
  });
  if (isLoading) return <Spinner />;
  return <List items={data} />;
}
```

---

## PART 14: Modern Performance Optimization

Modern web performance focuses on Core Web Vitals and resource loading.

### Core Web Vitals

- **LCP (Largest Contentful Paint):** <2.5s
- **FID (First Input Delay):** <100ms
- **CLS (Cumulative Layout Shift):** <0.1

**Example:**

```html
<!-- Preload critical image -->
<link rel="preload" as="image" href="hero.webp" fetchpriority="high" />
<!-- Responsive images -->
<picture>
  <source srcset="image.avif" type="image/avif" />
  <source srcset="image.webp" type="image/webp" />
  <img
    src="image.jpg"
    alt="Description"
    width="800"
    height="600"
    loading="eager"
  />
</picture>
```

### Resource Hints

Use `<preload>`, `<prefetch>`, and `<preconnect>` to optimize loading.

**Example:**

```html
<link rel="preconnect" href="https://api.example.com" />
<link rel="preload" href="critical.css" as="style" />
<link rel="prefetch" href="/likely-next-page" />
```

---

## PART 15: Modern Testing Approaches

Modern testing focuses on user behavior and reliability. Use component and E2E testing tools.

### Component Testing

Test components in isolation using tools like React Testing Library.

**Example:**

```js
import { render, screen, fireEvent } from '@testing-library/react';
test('counter increments when clicked', () => {
  render(<Counter />);
  fireEvent.click(screen.getByRole('button'));
  expect(screen.getByText('Count: 1')).toBeInTheDocument();
});
```

### E2E Testing

Test full user flows using Playwright or Cypress.

**Example:**

```js
test('user can complete checkout', async ({ page }) => {
  await page.goto('/shop');
  await page.getByRole('button', { name: 'Add to Cart' }).click();
  await page.getByRole('link', { name: 'Checkout' }).click();
  await page.fill('[name="email"]', 'test@example.com');
  await expect(page.getByText('Order Confirmed')).toBeVisible();
});
```

---

## PART 16: Modern CSS Features

Modern CSS enables powerful layouts and effects with less JavaScript.

### Container Queries

Use container queries to style elements based on their parent's size.

**Example:**

```css
.card-container {
  container-type: inline-size;
  container-name: card;
}
@container card (min-width: 400px) {
  .card {
    display: grid;
    grid-template-columns: 2fr 1fr;
  }
}
```

### CSS View Transitions

Use the View Transitions API for smooth UI changes.

**Example:**

```js
document.startViewTransition(() => {
  document.documentElement.classList.toggle('dark-theme');
});
// CSS
::view-transition-old(root),
::view-transition-new(root) {
  animation-duration: 0.5s;
}
```

---

## PART 17: Modern Build Tools

Modern build tools like Vite and Module Federation speed up development and improve performance.

### Vite

A fast build tool and dev server for modern web projects.

**Example:**

```js
// vite.config.js
import { defineConfig } from 'vite';
import react from '@vitejs/plugin-react';
export default defineConfig({
  plugins: [react()],
  build: {
    rollupOptions: {
      output: {
        manualChunks: {
          vendor: ['react', 'react-dom'],
          utils: ['./src/utils'],
        },
      },
    },
  },
});
```

### Module Federation

Share code between apps at runtime.

**Example:**

```js
// host/webpack.config.js
module.exports = {
  plugins: [
    new ModuleFederationPlugin({
      name: 'host',
      remotes: {
        shop: 'shop@http://localhost:3002/remoteEntry.js',
      },
      shared: {
        react: { singleton: true },
        'react-dom': { singleton: true },
      },
    }),
  ],
};
```

---

## PART 18: Modern React Patterns

Modern React patterns improve code organization and performance.

### Server Components

Server components fetch data and render on the server, reducing client bundle size.

**Example:**

```js
// app/page.tsx
async function BlogPosts() {
  const posts = await getPosts();
  return (
    <ul>
      {posts.map((post) => (
        <li key={post.id}>{post.title}</li>
      ))}
    </ul>
  );
}
```

### Compound Components

Build flexible, composable UI components.

**Example:**

```js
const Select = {
  Root: ({ children }) => {
    const [open, setOpen] = useState(false);
    return (
      <SelectContext.Provider value={{ open, setOpen }}>
        {children}
      </SelectContext.Provider>
    );
  },
  Trigger: () => {
    const { open, setOpen } = useSelectContext();
    return <button onClick={() => setOpen(!open)}>Toggle</button>;
  },
  Content: ({ children }) => {
    const { open } = useSelectContext();
    if (!open) return null;
    return <div className="content">{children}</div>;
  },
};
// Usage
<Select.Root>
  <Select.Trigger />
  <Select.Content>
    <div>Options here</div>
  </Select.Content>
</Select.Root>;
```

---

## PART 19: Modern API Patterns

Modern API patterns improve data fetching and state management, ensuring type safety and efficient communication between frontend and backend.

### tRPC

Type-safe API calls between frontend and backend.

**Example:**

```js
// API Definition
export const appRouter = createTRPCRouter({
  users: publicProcedure
    .input(z.object({ id: z.string() }))
    .query(async ({ input }) => {
      return await db.user.findUnique({
        where: { id: input.id },
      });
    }),
});
// Frontend Usage
function UserProfile() {
  const { data } = trpc.users.useQuery({ id: '123' });
  return <div>{data.name}</div>;
}
```

### Zod

Zod is a TypeScript-first schema declaration and validation library. It is often used in conjunction with tRPC to ensure that data structures are validated and type-safe, both on the client and server sides.

- **Schema Validation:** Zod allows you to define schemas for your data, which can be used to validate incoming and outgoing data in your API.

- **Type Inference:** Zod can infer TypeScript types from your schemas, ensuring that your code is type-safe and reducing the risk of runtime errors.

**Example:**

```js
import { z } from 'zod';

const UserSchema = z.object({
  id: z.string(),
  name: z.string(),
  email: z.string().email(),
});

// Validate data
const userData = UserSchema.parse({
  id: '123',
  name: 'John Doe',
  email: 'john.doe@example.com',
});
```

By combining tRPC with Zod, you can create robust, type-safe APIs that ensure data integrity and reduce the likelihood of errors in your application.

---

## PART 20: Modern Development Practices

Modern practices improve team efficiency and code quality.

### Feature Flags

Toggle features on/off for testing and gradual rollout.

**Example:**

```js
const flags = {
  newUI: process.env.NEXT_PUBLIC_ENABLE_NEW_UI === 'true',
  beta: process.env.NEXT_PUBLIC_ENABLE_BETA === 'true',
};
function FeatureWrapper({ flag, children, fallback = null }) {
  if (!flags[flag]) return fallback;
  return children;
}
// Usage
<FeatureWrapper flag="newUI">
  <NewDesign />
</FeatureWrapper>;
```

### A/B Testing

Test different versions of a feature to see which performs better.

**Example:**

```js
function ExperimentWrapper({ experimentId, variantA, variantB }) {
  const [variant, setVariant] = useState(null);
  useEffect(() => {
    const assigned = Math.random() > 0.5 ? 'A' : 'B';
    setVariant(assigned);
    analytics.track(`experiment_${experimentId}`, { variant: assigned });
  }, [experimentId]);
  if (variant === 'A') return variantA;
  if (variant === 'B') return variantB;
  return null;
}
// Usage
<ExperimentWrapper
  experimentId="new-header"
  variantA={<OldHeader />}
  variantB={<NewHeader />}
/>;
```

---

## PART 21: Modern Tooling & TypeScript

Modern tooling improves development experience and code quality.

### TypeScript Advanced Patterns

Use discriminated unions, type guards, and generics for safer code.

**Example:**

```ts
type State =
  | { status: 'idle' }
  | { status: 'loading' }
  | { status: 'success'; data: User }
  | { status: 'error'; error: Error };
function isSuccess(state: State): state is { status: 'success'; data: User } {
  return state.status === 'success';
}
function pick<T extends object, K extends keyof T>(
  obj: T,
  keys: K[]
): Pick<T, K> {
  const result = {} as Pick<T, K>;
  keys.forEach((key) => (result[key] = obj[key]));
  return result;
}
```

### Monorepo Management

Use tools like Turborepo or Nx to manage multiple packages in one repo.

**Example:**

```json
{
  "$schema": "https://turbo.build/schema.json",
  "pipeline": {
    "build": {
      "dependsOn": ["^build"],
      "outputs": ["dist/**"]
    },
    "test": {
      "dependsOn": ["build"],
      "inputs": ["src/**/*.tsx", "test/**/*.ts"]
    },
    "deploy": {
      "dependsOn": ["build", "test"]
    }
  }
}
```

---

## PART 22: AI Integration in Frontend

Modern apps use AI for smarter features and automation.

### AI-Powered Features

Use AI for search suggestions, recommendations, and more.

**Example:**

```js
function SearchBox() {
  const [query, setQuery] = useState('');
  const [suggestions, setSuggestions] = useState([]);
  const getSuggestions = useCallback(
    debounce(async (input) => {
      const response = await fetch('/api/ai/suggest', {
        method: 'POST',
        body: JSON.stringify({ query: input }),
      });
      const data = await response.json();
      setSuggestions(data.suggestions);
    }, 300),
    []
  );
  return (
    <div>
      <input
        value={query}
        onChange={(e) => {
          setQuery(e.target.value);
          getSuggestions(e.target.value);
        }}
      />
      <ul>
        {suggestions.map((s) => (
          <li key={s}>{s}</li>
        ))}
      </ul>
    </div>
  );
}
```

### Machine Learning Models

Integrate ML models in the browser with TensorFlow.js or similar.

**Example:**

```js
async function classifyImage(imageElement) {
  const model = await tf.loadLayersModel('/path/to/model.json');
  const tensor = tf.browser
    .fromPixels(imageElement)
    .resizeNearestNeighbor([224, 224])
    .toFloat()
    .expandDims();
  const prediction = await model.predict(tensor).data();
  return prediction;
}
```

---

## PART 23: Modern Security Practices

Modern security is critical for protecting users and data.

### Content Security Policy (CSP)

Set CSP headers to control what resources can load.

**Example:**

```js
const securityHeaders = [
  {
    key: 'Content-Security-Policy',
    value: `
      default-src 'self';
      script-src 'self' 'unsafe-eval' 'unsafe-inline';
      style-src 'self' 'unsafe-inline';
      img-src 'self' data: https:;
      font-src 'self';
      object-src 'none';
      base-uri 'self';
      form-action 'self';
      frame-ancestors 'none';
      block-all-mixed-content;
      upgrade-insecure-requests;
    `,
  },
];
module.exports = {
  async headers() {
    return [
      {
        source: '/:path*',
        headers: securityHeaders,
      },
    ];
  },
};
```

### OAuth 2.0 & PKCE

Use OAuth with PKCE for secure authentication.

**Example:**

```js
async function initiateOAuthFlow() {
  const codeVerifier = generateRandomString(64);
  const codeChallenge = await generateCodeChallenge(codeVerifier);
  sessionStorage.setItem('code_verifier', codeVerifier);
  const params = new URLSearchParams({
    client_id: CLIENT_ID,
    redirect_uri: REDIRECT_URI,
    response_type: 'code',
    code_challenge: codeChallenge,
    code_challenge_method: 'S256',
    scope: 'openid profile email',
  });
  window.location.href = `${AUTH_ENDPOINT}?${params}`;
}
async function handleOAuthCallback(code) {
  const codeVerifier = sessionStorage.getItem('code_verifier');
  const response = await fetch(TOKEN_ENDPOINT, {
    method: 'POST',
    body: new URLSearchParams({
      grant_type: 'authorization_code',
      code,
      code_verifier: codeVerifier,
      client_id: CLIENT_ID,
      redirect_uri: REDIRECT_URI,
    }),
  });
  const tokens = await response.json();
  securelyStoreTokens(tokens);
}
```

---

Happy studying, and you'll nail that interview!
