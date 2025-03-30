# Creating Elements

---

# **1. Vanilla JavaScript (`document.createElement`)**

```jsx
const heading = document.createElement("h1");
heading.innerHTML = "Hello from JavaScript";
const root = document.getElementById("root");
root.appendChild(heading);
```

### **How It Works**

- Creates an actual `<h1>` element.
- Modifies it directly in the DOM.
- Updates happen instantly but can be inefficient for large-scale changes.

---

# **2. React Without JSX (`React.createElement`)**

```jsx
import React from "react";
import ReactDOM from "react-dom/client";

const heading = React.createElement(
  "h1",
  null,
  "Hello from React"
);
const root = ReactDOM.createRoot(document.getElementById("root"));
root.render(heading);
```

When you use `React.createElement()`, it does **not** create an actual DOM element immediately. Instead, it creates a **JavaScript object** representing the element (Virtual DOM). Later, React's **Reconciliation Algorithm** compares this virtual representation to the previous one and efficiently updates the real DOM.

### **Step-by-Step Breakdown**

Let's consider this example:

```jsx
const heading = React.createElement(
  "h1",
  { id: "heading", className: "title" },
  "Hello from React"
);
```

- Converts it into an **object representation** of the element:

```jsx
{
  type: "h1",
  props: {
    id: "heading",
    className: "title",
    children: "Hello from React"
  }
}
```

## **🚨 Problem: Deeply Nested `React.createElement()` Calls**

When UI components contain multiple nested elements, using `React.createElement()` quickly becomes unreadable.

### **Example: A Simple UI Component**

A basic structure in **pure `React.createElement()`**:

```jsx
const app = React.createElement(
  "div",
  { id: "container" },
  React.createElement("header", null,
    React.createElement("h1", null, "Welcome to React"),
    React.createElement("p", null, "This is a simple UI")
  ),
  React.createElement("main", null,
    React.createElement("section", null,
      React.createElement("ul", null,
        React.createElement("li", null, "Item 1"),
        React.createElement("li", null, "Item 2"),
        React.createElement("li", null, "Item 3")
      )
    )
  )
);
```

### **Problems with this Approach:**

1. **Deeply Nested Function Calls** – Hard to track element hierarchy.
2. **Unmanageable as Components Grow** – More elements = more **nested calls**, making debugging difficult.
3. **Difficult to Visualize Structure** – The UI structure isn’t **intuitive** at a glance.

---

# **3. React Using JSX (Compiled to `React.createElement`)**

JSX is just a cleaner syntax for `React.createElement`.

```jsx
import React from "react";
import ReactDOM from "react-dom/client";

const heading = <h1>Hello from JSX</h1>;
const root = ReactDOM.createRoot(document.getElementById("root"));
root.render(heading);
```

### **How It Works**

- JSX is converted into `React.createElement` by Babel.
- The virtual DOM gets updated efficiently.
- React only modifies the necessary parts of the real DOM.

## **JSX Compilation to `React.createElement`**

When using JSX:

```jsx
const heading = <h1 id="heading" className="title">Hello from JSX</h1>;
```

It gets **compiled** by Babel into:

```jsx
const heading = React.createElement(
  "h1",
  { id: "heading", className: "title" },
  "Hello from JSX"
);
```

This means **JSX is just a syntactic sugar** for `React.createElement`!

## **✅ JSX Solves the Complexity that arises while using** `React.createElement`

With **JSX**, the same structure is much more readable:

```jsx
const app = (
  <div id="container">
    <header>
      <h1>Welcome to React</h1>
      <p>This is a simple UI</p>
    </header>
    <main>
      <section>
        <ul>
          <li>Item 1</li>
          <li>Item 2</li>
          <li>Item 3</li>
        </ul>
      </section>
    </main>
  </div>
);
```

### **How JSX Fixes the Problem:**

✅ **Cleaner & More Readable** – Looks like HTML, easy to follow.

✅ **Maintains Clear Hierarchy** – No excessive nesting of function calls.

✅ **Easier to Modify & Debug** – Intuitive structure for large components.