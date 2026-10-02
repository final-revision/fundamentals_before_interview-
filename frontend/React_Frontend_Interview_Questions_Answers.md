# React.js Frontend Interview Questions & Answers
## Fresher / Internship / Software Developer Interview Preparation

> **Focus:** React.js, JavaScript, HTML, CSS, frontend fundamentals, project-based questions, debugging, APIs, and practical React interview questions.

---

# 1. HTML & CSS Fundamentals

## Q1. What is HTML?
**Answer:**  
HTML (HyperText Markup Language) is used to structure the content of a web page. It defines elements such as headings, paragraphs, forms, buttons, images, links, tables, and sections.

Example:
```html
<h1>Hello World</h1>
<p>This is a paragraph.</p>
```

## Q2. What are semantic HTML elements?
**Answer:**  
Semantic elements clearly describe their purpose.

Examples:
- `<header>`
- `<nav>`
- `<main>`
- `<section>`
- `<article>`
- `<footer>`

They improve readability, accessibility, and SEO.

## Q3. Difference between `div` and `span`.
**Answer:**
- `div` is normally a block-level container.
- `span` is normally an inline container.
- Both are generic containers without semantic meaning.

## Q4. What is CSS?
**Answer:**  
CSS (Cascading Style Sheets) controls the appearance and layout of HTML elements.

It handles:
- colors
- fonts
- spacing
- positioning
- responsive design
- animations

## Q5. What is the CSS box model?
**Answer:**  
Every HTML element is treated as a box containing:

`Content → Padding → Border → Margin`

`box-sizing: border-box` makes width/height include padding and border.

## Q6. Difference between Flexbox and Grid.
**Answer:**
- **Flexbox:** Mainly one-dimensional layouts — row OR column.
- **Grid:** Two-dimensional layouts — rows AND columns.

Flexbox is useful for navigation bars and alignment. Grid is useful for page layouts and card grids.

## Q7. What is responsive design?
**Answer:**  
Responsive design makes a website adapt to different screen sizes such as mobile, tablet, and desktop.

Common techniques:
- CSS media queries
- Flexbox
- CSS Grid
- relative units
- responsive images

---

# 2. JavaScript Fundamentals

## Q8. What is JavaScript?
**Answer:**  
JavaScript is a programming language used to make web pages interactive and dynamic.

It can handle:
- events
- API requests
- DOM manipulation
- validation
- application logic
- asynchronous operations

## Q9. Difference between `var`, `let`, and `const`.
**Answer:**

| Feature | var | let | const |
|---|---|---|---|
| Scope | Function | Block | Block |
| Reassignment | Yes | Yes | No |
| Redeclaration | Yes | No | No |

In modern JavaScript, `let` and `const` are generally preferred.

## Q10. Difference between `==` and `===`.
**Answer:**
- `==` compares values after type conversion.
- `===` compares both value and type.

```js
5 == "5"   // true
5 === "5"  // false
```

Prefer `===` when strict comparison is required.

## Q11. What are arrow functions?
**Answer:**
Arrow functions provide shorter function syntax.

```js
const add = (a, b) => a + b;
```

They also handle `this` differently from regular functions: arrow functions don't create their own `this`.

## Q12. What is destructuring?
**Answer:**  
Destructuring extracts values from objects or arrays.

```js
const user = { name: "Digvijay", age: 21 };
const { name, age } = user;
```

## Q13. What is the spread operator?
**Answer:**  
The spread operator `...` expands elements of an array or properties of an object.

```js
const a = [1, 2];
const b = [...a, 3];
```

It is commonly used in React to create updated state without mutating the original state.

## Q14. Difference between `map()`, `filter()`, and `reduce()`.
**Answer:**

- `map()` transforms every element.
- `filter()` selects elements based on a condition.
- `reduce()` combines elements into a single result.

```js
numbers.map(x => x * 2);

numbers.filter(x => x > 10);

numbers.reduce((sum, x) => sum + x, 0);
```

## Q15. What is a Promise?
**Answer:**  
A Promise represents the eventual success or failure of an asynchronous operation.

States:
- pending
- fulfilled
- rejected

```js
fetch("/api/users")
  .then(response => response.json())
  .then(data => console.log(data))
  .catch(error => console.error(error));
```

## Q16. What is async/await?
**Answer:**  
`async/await` provides a cleaner way to work with Promises.

```js
async function getUsers() {
  try {
    const response = await fetch("/api/users");
    const data = await response.json();
    return data;
  } catch (error) {
    console.error(error);
  }
}
```

---

# 3. React.js Fundamentals

## Q17. What is React?
**Answer:**  
React is a JavaScript library for building user interfaces, especially component-based web applications.

Important concepts:
- Components
- JSX
- Props
- State
- Hooks
- Event handling
- Conditional rendering
- Lists and keys
- Context
- Routing

## Q18. Why do you use React?
**Answer:**  
I use React because it allows me to break the UI into reusable components, manage changing UI state efficiently, and build large applications in a structured way.

## Q19. What is a component?
**Answer:**  
A component is a reusable piece of UI.

Example:
```jsx
function Button() {
  return <button>Click Me</button>;
}
```

A page can be composed of components such as Navbar, Sidebar, Card, Form, and Footer.

## Q20. What is JSX?
**Answer:**  
JSX is a syntax extension that allows us to write HTML-like markup inside JavaScript.

```jsx
const element = <h1>Hello React</h1>;
```

JSX is transformed into JavaScript by the React build toolchain.

## Q21. What are props?
**Answer:**  
Props are inputs passed from a parent component to a child component.

```jsx
function User({ name }) {
  return <h2>{name}</h2>;
}

<User name="Digvijay" />
```

Props should be treated as read-only by the receiving component.

## Q22. What is state?
**Answer:**  
State is data managed by a component that can change over time and cause the UI to update.

```jsx
const [count, setCount] = useState(0);
```

## Q23. Props vs State.
**Answer:**

| Props | State |
|---|---|
| Passed by parent | Managed by component |
| Read-only | Can be updated |
| Used to configure components | Represents changing data |
| Helps component communication | Controls component behavior |

## Q24. What is `useState()`?
**Answer:**  
`useState` is a React Hook used to add state to a functional component.

```jsx
const [name, setName] = useState("");
```

`name` is the current state and `setName` updates it.

## Q25. What is `useEffect()`?
**Answer:**  
`useEffect` is used for side effects such as:
- API calls
- subscriptions
- timers
- interacting with external systems

Example:
```jsx
useEffect(() => {
  fetchUsers();
}, []);
```

## Q26. What does the dependency array in `useEffect` do?
**Answer:**
```jsx
useEffect(() => {
  console.log("Runs");
}, []);
```

- `[]` → runs after initial mount.
- `[value]` → runs after mount and when `value` changes.
- No dependency array → runs after every render.

## Q27. What is conditional rendering?
**Answer:**  
Displaying different UI based on a condition.

```jsx
{isLoggedIn ? <Dashboard /> : <Login />}
```

## Q28. How do you render a list in React?
**Answer:**
```jsx
const users = ["A", "B", "C"];

return (
  <ul>
    {users.map(user => (
      <li key={user}>{user}</li>
    ))}
  </ul>
);
```

## Q29. Why is `key` important in React lists?
**Answer:**  
A key gives React a stable identity for each list item. This helps React determine which items changed, were added, or removed.

Use a stable unique identifier when possible.

Avoid using array index as a key when list order can change.

---

# 4. React Hooks

## Q30. What are Hooks?
**Answer:**  
Hooks are functions that allow functional components to use React features such as state and lifecycle-related behavior.

Common Hooks:
- `useState`
- `useEffect`
- `useContext`
- `useRef`
- `useMemo`
- `useCallback`

## Q31. What is `useRef()`?
**Answer:**  
`useRef` stores a mutable value that persists between renders without causing a re-render when changed.

It is commonly used to:
- access DOM elements
- store timer IDs
- retain previous values

```jsx
const inputRef = useRef(null);

inputRef.current.focus();
```

## Q32. What is `useContext()`?
**Answer:**  
`useContext` allows components to consume values from React Context without passing props through every intermediate component.

Useful for:
- theme
- authentication state
- language
- shared application settings

## Q33. What is `useMemo()`?
**Answer:**  
`useMemo` memoizes a calculated value and recalculates it only when dependencies change.

```jsx
const result = useMemo(() => expensiveCalculation(data), [data]);
```

It should be used when there is a real performance benefit, not everywhere by default.

## Q34. What is `useCallback()`?
**Answer:**  
`useCallback` memoizes a function reference.

```jsx
const handleClick = useCallback(() => {
  console.log("Clicked");
}, []);
```

It can be useful when passing callbacks to memoized child components.

## Q35. Difference between `useMemo` and `useCallback`.
**Answer:**
- `useMemo` memoizes a **value**.
- `useCallback` memoizes a **function**.

---

# 5. React Rendering & Performance

## Q36. What causes a React component to re-render?
**Answer:**  
A component can re-render when:
- its state changes
- its parent re-renders
- its props change
- a consumed context value changes

A re-render does not necessarily mean the DOM is fully rebuilt.

## Q37. What is the Virtual DOM?
**Answer:**  
The Virtual DOM is an in-memory representation of the UI. React uses it as part of its rendering process to determine the necessary DOM updates.

## Q38. What is reconciliation?
**Answer:**  
Reconciliation is React's process of comparing the previous rendered tree with the next one and determining what needs to change in the actual UI.

## Q39. How can you optimize a React application?
**Answer:**
- Avoid unnecessary state.
- Use stable list keys.
- Split large components.
- Lazy-load routes/components.
- Optimize large lists.
- Avoid unnecessary expensive calculations.
- Use `memo`, `useMemo`, or `useCallback` when justified.
- Avoid unnecessary effects.
- Optimize images and network requests.

## Q40. What is `React.memo()`?
**Answer:**  
`React.memo` prevents a component from re-rendering when its props have not changed according to its comparison.

```jsx
const UserCard = React.memo(function UserCard({ user }) {
  return <div>{user.name}</div>;
});
```

It is useful only when it actually avoids meaningful re-render work.

---

# 6. Forms & Events

## Q41. How do you handle forms in React?
**Answer:**  
A common approach is a controlled component where input values are stored in React state.

```jsx
const [email, setEmail] = useState("");

<input
  value={email}
  onChange={e => setEmail(e.target.value)}
/>
```

## Q42. What is a controlled component?
**Answer:**  
A controlled input gets its value from React state and updates that state through event handlers.

## Q43. What is an uncontrolled component?
**Answer:**  
An uncontrolled input stores its current value in the DOM rather than React state. `useRef` can be used to access it.

## Q44. How do you handle click events?
**Answer:**
```jsx
<button onClick={handleClick}>
  Submit
</button>
```

Do not call the function immediately:

```jsx
// Usually wrong
<button onClick={handleClick()}>
```

---

# 7. API Integration

## Q45. How do you connect React with a backend?
**Answer:**  
React can communicate with a backend through HTTP APIs.

Typical flow:

`React UI → fetch/axios → Backend API → Database → Backend response → React state → UI`

## Q46. How do you make an API request in React?
**Answer:**
```jsx
useEffect(() => {
  async function loadUsers() {
    const response = await fetch("/api/users");
    const data = await response.json();
    setUsers(data);
  }

  loadUsers();
}, []);
```

## Q47. What is Axios?
**Answer:**  
Axios is an HTTP client library used to make requests to APIs.

Example:
```js
const response = await axios.get("/api/users");
```

## Q48. What HTTP methods do you know?
**Answer:**
- `GET` — retrieve data
- `POST` — create data
- `PUT` — replace/update data
- `PATCH` — partially update data
- `DELETE` — delete data

## Q49. What are common HTTP status codes?
**Answer:**
- `200` — successful request
- `201` — resource created
- `400` — bad request
- `401` — unauthenticated
- `403` — forbidden
- `404` — not found
- `500` — server error

## Q50. How do you handle API loading and errors?
**Answer:**
Maintain separate state values.

```jsx
const [loading, setLoading] = useState(false);
const [error, setError] = useState(null);
const [users, setUsers] = useState([]);
```

Then show:
- loading UI while request is running
- data after success
- error message after failure

---

# 8. React Router

## Q51. What is React Router?
**Answer:**  
React Router is commonly used to implement client-side routing in React applications.

Example:
```jsx
<Route path="/login" element={<Login />} />
<Route path="/dashboard" element={<Dashboard />} />
```

## Q52. What is client-side routing?
**Answer:**  
Client-side routing changes the displayed view without requiring a complete browser page reload for every route.

## Q53. How would you protect a route?
**Answer:**  
Create a protected route component that checks authentication state.

Concept:
```jsx
return isAuthenticated
  ? <Dashboard />
  : <Navigate to="/login" />;
```

The backend must still enforce authorization; hiding a frontend route is not a security boundary.

---

# 9. Authentication

## Q54. What is JWT?
**Answer:**  
JWT (JSON Web Token) is a token format commonly used to represent authenticated claims between a client and server.

Typical flow:

`Login → Backend verifies credentials → Backend issues token → Client sends token with protected requests → Backend verifies token`

## Q55. Where can authentication tokens be stored?
**Answer:**  
The choice depends on the application security model. A common browser approach is an HttpOnly, Secure cookie because JavaScript cannot directly read it, which can reduce exposure to token theft through some XSS scenarios.

If tokens are stored in browser-accessible storage, XSS becomes an important concern.

## Q56. Authentication vs Authorization.
**Answer:**
- **Authentication:** Who are you?
- **Authorization:** What are you allowed to do?

Example:
A user logs in → authentication.  
Only an admin can delete users → authorization.

---

# 10. State Management

## Q57. What is prop drilling?
**Answer:**  
Prop drilling occurs when data is passed through multiple intermediate components even though those components do not need the data themselves.

## Q58. How can prop drilling be reduced?
**Answer:**
- Component composition
- Context API
- State management libraries when appropriate

## Q59. What is Context API?
**Answer:**  
Context provides a way to share values across a component tree without passing props manually through every level.

## Q60. When would you use Redux?
**Answer:**  
Redux can be useful when an application has substantial shared state and complex update flows that benefit from centralized state management.

For small applications, local state and Context may be sufficient.

---

# 11. Project-Based Interview Questions

## Q61. Explain one React project you built.
**Sample Answer:**

"I built a React-based web application where I divided the UI into reusable components such as Navbar, forms, cards, and pages. I used React state for dynamic data, React Router for navigation, and API calls to communicate with the backend. I also handled loading states, errors, form validation, and responsive UI."

> Replace this answer with the exact features of your actual project.

## Q62. Why did you choose React for your project?
**Sample Answer:**

"I chose React because the application contains multiple reusable UI components and dynamic data. React's component architecture made the code easier to organize and reuse. Hooks also made state and side-effect management straightforward."

## Q63. How did you structure your React project?
**Sample Answer:**

"A typical structure I used was:

```text
src/
├── components/
├── pages/
├── services/
├── hooks/
├── assets/
├── context/
├── App.jsx
└── main.jsx
```

Components contain reusable UI, pages represent screens, services contain API-related logic, and context is used for shared state when required."

## Q64. How did your frontend communicate with your backend?
**Sample Answer:**

"The React frontend sent HTTP requests to backend REST APIs using fetch/Axios. The backend processed the request and interacted with the database. The response was stored in React state and displayed through components."

## Q65. What was the most difficult part of your project?
**Sample Answer:**

"One challenging part was managing asynchronous API data and UI states. I had to handle loading, successful responses, errors, and empty results correctly. I solved it by separating API logic from UI components and maintaining clear loading/error/data states."

## Q66. How did you debug your React project?
**Answer:**
I used:
- Browser DevTools
- Console logs
- Network tab
- React Developer Tools
- API testing tools such as Postman
- checking component props/state
- checking backend API responses

## Q67. Tell me about a bug you fixed.
**Sample Answer:**

"One issue I faced was that the UI was not updating after an API operation. I checked the Network tab to verify the API response and then checked the React state update. I found that I was not updating the state correctly after the operation. I fixed the state update and verified the complete flow."

---

# 12. Practical React Questions

## Q68. Why should we not mutate React state directly?
**Answer:**

Avoid:
```js
user.name = "New Name";
```

Prefer:
```js
setUser({
  ...user,
  name: "New Name"
});
```

Creating a new state value makes React state updates predictable and allows React to detect changes correctly.

## Q69. How do you update an object in state?
```jsx
setUser(prev => ({
  ...prev,
  name: "New Name"
}));
```

## Q70. How do you update an array in state?
Add:
```jsx
setItems(prev => [...prev, newItem]);
```

Remove:
```jsx
setItems(prev => prev.filter(item => item.id !== id));
```

Update:
```jsx
setItems(prev =>
  prev.map(item =>
    item.id === id ? { ...item, completed: true } : item
  )
);
```

## Q71. What is the problem with using an effect for everything?
**Answer:**  
Effects are intended for synchronizing with external systems. Using them for ordinary derived values or event-specific logic can create unnecessary renders and complicated code.

For example, if `fullName` can be calculated directly from `firstName` and `lastName`, it usually does not need a `useEffect`.

## Q72. What is a custom Hook?
**Answer:**  
A custom Hook is a reusable JavaScript function whose name starts with `use` and that can use other Hooks.

Example:
```jsx
function useUsers() {
  const [users, setUsers] = useState([]);
  // API logic
  return { users, setUsers };
}
```

---

# 13. Advanced React Questions

## Q73. What is code splitting?
**Answer:**  
Code splitting divides JavaScript into smaller chunks that can be loaded when needed.

React supports lazy loading:

```jsx
const Dashboard = lazy(() => import("./Dashboard"));
```

This can reduce the initial JavaScript load.

## Q74. What is lazy loading?
**Answer:**  
Lazy loading means loading a component/resource only when it is required rather than loading everything initially.

## Q75. What is Suspense?
**Answer:**  
`Suspense` allows React to display fallback UI while certain lazy-loaded content is waiting.

```jsx
<Suspense fallback={<p>Loading...</p>}>
  <Dashboard />
</Suspense>
```

## Q76. What is a Higher-Order Component?
**Answer:**  
A Higher-Order Component (HOC) is a function that takes a component and returns an enhanced component.

It is an older reusable pattern. Modern React code often prefers Hooks and component composition.

## Q77. What is lifting state up?
**Answer:**  
When two or more components need to share state, the state can be moved to their closest common parent, which then passes the required data and callbacks to the children.

---

# 14. Frontend Security

## Q78. What is XSS?
**Answer:**  
XSS (Cross-Site Scripting) occurs when an attacker manages to execute malicious JavaScript in a user's browser through application-controlled content.

Prevention includes:
- proper output handling
- avoiding unsafe HTML injection
- sanitizing untrusted HTML when required
- Content Security Policy
- secure coding practices

## Q79. What is CORS?
**Answer:**  
CORS (Cross-Origin Resource Sharing) is a browser security mechanism that controls whether a web page from one origin can access resources from another origin.

Example:
Frontend:
`http://localhost:5173`

Backend:
`http://localhost:5000`

The backend needs appropriate CORS configuration for allowed origins.

---

# 15. HTML/CSS/React Rapid-Fire Questions

## Q80. What is DOM?
**Answer:**  
DOM stands for Document Object Model. It represents an HTML document as a tree of objects that JavaScript can interact with.

## Q81. What is event bubbling?
**Answer:**  
An event can propagate from the target element upward through its ancestors.

## Q82. What is event delegation?
**Answer:**  
Event delegation attaches an event handler to a parent and uses event bubbling to handle events from child elements.

## Q83. What is accessibility?
**Answer:**  
Accessibility means making applications usable by people with different abilities.

Use:
- semantic HTML
- labels for form fields
- keyboard-friendly controls
- meaningful alt text
- sufficient focus visibility

## Q84. Difference between `display: none` and `visibility: hidden`.
**Answer:**
- `display: none` removes the element from the layout.
- `visibility: hidden` keeps its layout space but hides the element.

---

# 16. Scenario-Based Questions

## Q85. API is taking 5 seconds. What will you do?
**Answer:**
1. Check the Network tab.
2. Determine whether delay is frontend, backend, database, or network related.
3. Check API response time.
4. Avoid unnecessary duplicate requests.
5. Add loading UI.
6. Optimize the backend/database if that is the bottleneck.
7. Consider caching or pagination where appropriate.

## Q86. React page is rendering too many times. What will you check?
**Answer:**
- State updates
- Parent re-renders
- Context updates
- Effect dependencies
- Unstable object/function props
- Whether expensive work runs during render

Use React DevTools Profiler to investigate before optimizing.

## Q87. API returns data but UI does not show it. What will you check?
**Answer:**
1. Network response.
2. API response structure.
3. State update.
4. Component props.
5. Rendering condition.
6. Array/object structure.
7. Console errors.

## Q88. Login works but dashboard does not open. What will you check?
**Answer:**
- authentication state
- token/cookie
- protected route
- API authorization
- browser console
- Network request status
- backend response
- route configuration

## Q89. Website works on desktop but not mobile. What will you check?
**Answer:**
- viewport meta tag
- CSS media queries
- fixed widths
- Flexbox/Grid behavior
- overflowing elements
- image sizes
- font sizes
- browser DevTools responsive mode

---

# 17. Questions Interviewers Can Ask About Your Coding

## Q90. Explain this code:
```jsx
const [count, setCount] = useState(0);

<button onClick={() => setCount(count + 1)}>
  {count}
</button>
```

**Answer:**  
`count` stores the current state. `setCount` updates it. Clicking the button calls the updater, React schedules a re-render, and the displayed count changes.

## Q91. What happens when state changes?
**Answer:**  
React schedules the component to render again. React then determines the required UI changes and updates the DOM accordingly.

## Q92. Why use functional state updates?
**Answer:**  
When the new state depends on the previous state, functional updates are safer:

```jsx
setCount(prev => prev + 1);
```

This is especially useful when multiple updates may be queued.

---

# 18. Questions About Your React Skill Level

## Q93. How much React do you know?
**Sample Answer:**

"I have built 2–3 projects using React.js, so I have practical experience rather than only theoretical knowledge. I am comfortable with components, JSX, props, state, Hooks such as useState and useEffect, forms, API integration, routing, conditional rendering, and responsive UI. I am currently improving my knowledge of performance optimization and advanced React patterns."

## Q94. Have you worked with APIs?
**Sample Answer:**

"Yes. In my React projects, I have consumed REST APIs from the frontend. I handled GET/POST/PUT/DELETE operations, stored the response in state, displayed loading and error states, and connected frontend actions with backend endpoints."

## Q95. Have you used Git?
**Answer:**

"Yes. I use Git for version control and GitHub for storing and managing my projects. I know commands such as `git clone`, `git add`, `git commit`, `git push`, `git pull`, `git branch`, and `git merge`."

---

# 19. Very Important: Explain Your Project Architecture

Use this structure during an interview:

```text
User
  ↓
React UI
  ↓
Components / Pages
  ↓
Event Handler
  ↓
API Service
  ↓
REST API
  ↓
Node.js / Express Backend
  ↓
Database
  ↓
Response
  ↓
React State
  ↓
Updated UI
```

### Sample explanation

"My frontend is built using React. I divided the application into reusable components and pages. User interactions trigger event handlers, which call API functions. The backend processes the request and communicates with the database. The response comes back to React, where I update the relevant state and React re-renders the UI."

---

# 20. Interviewer May Ask You to Write Code

## Question: Create a counter.
```jsx
import { useState } from "react";

function Counter() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>{count}</p>
      <button onClick={() => setCount(prev => prev + 1)}>
        Increment
      </button>
      <button onClick={() => setCount(prev => prev - 1)}>
        Decrement
      </button>
    </div>
  );
}

export default Counter;
```

## Question: Create a search filter.
```jsx
const filteredUsers = users.filter(user =>
  user.name.toLowerCase().includes(search.toLowerCase())
);
```

## Question: Fetch API data.
```jsx
useEffect(() => {
  async function fetchData() {
    try {
      const response = await fetch("/api/users");
      const data = await response.json();
      setUsers(data);
    } catch (error) {
      setError(error.message);
    }
  }

  fetchData();
}, []);
```

## Question: Render cards from an array.
```jsx
{products.map(product => (
  <ProductCard
    key={product.id}
    product={product}
  />
))}
```

---

# 21. Common HR + Technical Combination Questions

## Q96. Why should we hire you for a frontend role?
**Sample Answer:**

"I have practical experience building React projects, not just learning the theory. I understand the fundamentals of JavaScript, React components, Hooks, API integration, routing, forms, and responsive UI. I am also comfortable learning new technologies and debugging problems independently."

## Q97. What are your strengths as a developer?
**Sample Answer:**

"My strengths are problem solving, willingness to learn, and practical project development. When I face an issue, I try to reproduce it, identify the actual cause, and then implement and test the fix."

## Q98. What do you need to improve?
**Sample Answer:**

"I am continuously improving my advanced React knowledge, especially performance optimization, scalable state management, and deeper frontend architecture. I am already practicing these concepts through projects."

---

# 22. Questions You Should Ask the Interviewer

At the end, you can ask:

1. "What frontend technologies does the team currently use?"
2. "What would be the typical responsibilities of an intern or fresher in this role?"
3. "How is the development team structured?"
4. "What kind of projects would I initially work on?"
5. "What skills would you recommend I strengthen before joining?"

---

# 23. Final High-Priority Revision List

Before the interview, make sure you can explain these **without memorizing blindly**:

### JavaScript
- `let`, `const`, `var`
- `==` vs `===`
- functions and arrow functions
- arrays and objects
- map/filter/reduce
- destructuring
- spread operator
- promises
- async/await
- DOM
- events

### React
- React basics
- Components
- JSX
- Props
- State
- `useState`
- `useEffect`
- `useRef`
- `useContext`
- `useMemo`
- `useCallback`
- `React.memo`
- Conditional rendering
- Lists and keys
- Forms
- API integration
- React Router
- Authentication
- Context API
- State management
- Performance optimization

### Frontend
- HTML semantics
- CSS box model
- Flexbox
- Grid
- Responsive design
- HTTP methods
- HTTP status codes
- REST APIs
- CORS
- XSS
- Git/GitHub
- Browser DevTools

### Project
Be ready to explain:
1. Project objective
2. Why you selected React
3. Features
4. Component structure
5. State management
6. API integration
7. Backend communication
8. Authentication
9. Database interaction
10. Biggest challenge
11. Bug you solved
12. What you would improve
13. How the project can scale

---

# 24. Most Likely Questions for Your Profile

Because you have built **2–3 React.js projects**, interviewers are likely to move quickly from theory to your actual implementation.

Prepare especially for:

1. Explain your React project.
2. Why React instead of plain JavaScript?
3. Explain your component structure.
4. Which Hooks did you use?
5. Why did you use `useEffect`?
6. Explain the dependency array.
7. How did you call your backend API?
8. How did you handle loading and errors?
9. How did you implement forms?
10. How did you validate user input?
11. How did you implement routing?
12. How did you implement login/authentication?
13. Where did you store authentication information?
14. How did you manage global state?
15. What was the hardest bug you faced?
16. How did you debug it?
17. How would you improve the project?
18. How would you make the application responsive?
19. How would you optimize a slow React page?
20. Write a React component during the interview.

---

# 25. Golden Rule for Project Questions

**Never claim a feature that you did not actually implement.**

If the interviewer asks:

> "Did you use Redux?"

If you did not:

> "No, I didn't use Redux in that project. I used local state and Context where required. I understand the purpose of Redux and I am learning it."

This is much better than claiming experience you cannot explain.

---

# 26. 30-Second React Introduction

Use this if the interviewer asks:

> "Tell me about your React experience."

**Answer:**

"I have practical experience with React.js through 2–3 projects. I have worked with functional components, JSX, props, state, useState, useEffect, API integration, forms, routing, conditional rendering, and responsive UI. I have also connected React applications with backend REST APIs. Through these projects I learned how to structure components, manage application state, debug frontend issues, and build reusable UI."

---

# 27. One-Minute Project Explanation Template

Use this structure:

**1. Problem:**  
"What problem does the project solve?"

**2. Solution:**  
"What does your application do?"

**3. Technology:**  
"I used React.js for the frontend and [your backend/database] for the backend."

**4. Architecture:**  
"The React frontend communicates with the backend through REST APIs."

**5. Your contribution:**  
"I personally worked on [specific features]."

**6. Challenge:**  
"The main challenge was [real challenge]."

**7. Result:**  
"I solved it by [solution]."

---

# Final Preparation Strategy

For a React-focused interview, do not spend all your time memorizing definitions.

Use this order:

### Priority 1 — Your Projects
Be able to explain every important file, component, API, feature, and decision.

### Priority 2 — React
Master:
`Components → JSX → Props → State → useState → useEffect → Forms → API → Router`

### Priority 3 — JavaScript
Master:
`Arrays → Objects → map/filter/reduce → async/await → Promises → destructuring → spread`

### Priority 4 — Frontend Fundamentals
Master:
`HTML → CSS → Flexbox → Grid → Responsive Design → HTTP → REST → CORS`

### Priority 5 — Advanced React
Then revise:
`Context → useRef → memo → useMemo → useCallback → lazy loading → performance`

**The most important point:** If you mention a technology on your resume, be prepared to explain **what it is, why you used it, how you implemented it, and one problem you solved with it.**
