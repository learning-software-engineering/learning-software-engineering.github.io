# React Bad Practices - Prop Drilling

# Table of Contents
1. [What is Props Drilling?](#what-is-props-drilling)
2. [Why is Props Drilling Bad?](#why-is-props-drilling-bad)
3. [Example of Props Drilling](#example-of-props-drilling)
4. [Avoiding Props Drilling](#avoiding-props-drilling)
5. [Alternative Solutions](#alternative-solutions)
6. [Final Remark](#final-remark)
7. [Sources](#sources)

## What is Props Drilling?
In React.js, props drilling refers to the process of passing props down through multiple layers of components. It happens when a component needs to pass data to a deeply nested child component, and each intermediate parent component in the hierarchy needs to receive and pass along the props. This is not a huge issue in small lightweight applications but can become a large issue when the application scales.

## Why is Props Drilling Bad?
Props drilling can lead to several issues in a React application:

- **Maintenance:** As the application grows, managing and updating props through multiple layers becomes extremely cumbersome and error-prone. It makes the codebase harder to understand and maintain.

- **Code Smells:** Props drilling often indicates a design flaw in the application's component hierarchy. It violates the principles of encapsulation and modularity, making components less reusable and more tightly coupled.

- **Reduced Component Isolation:** Components become overly dependent on their parent components, breaking the idea of encapsulation. Changes in one layer may require modifications in several other layers. This problem is evident when the application is large.

## Example of Props Drilling
Consider the following example where data needs to be passed from the top-level component to a deeply nested one:
```jsx
// Top-level component
const App = () => {
  const data = "Hello, Props Drilling!";

  return (
    <div>
      <ParentComponent data={data} />
    </div>
  );
};

// Intermediate parent component
const ParentComponent = ({ data }) => {
  return (
    <div>
      <ChildComponent data={data} />
    </div>
  );
};

// Deeply nested child component
const ChildComponent = ({ data }) => {
  return (
    <div>
      <p>{data}</p>
    </div>
  );
};
```
In this example, ChildComponent needs the data prop, and ParentComponent serves as an intermediary just to pass it down.

## Avoiding Props Drilling
To mitigate props drilling, React provides the Context API. Context allows you to share values, such as props, across components without explicitly passing them through each level.

Below is a modified version of the previous example using the Context API:

```jsx
// Creating a context
const DataContext = React.createContext();

// Top-level component
const App = () => {
  const data = "Hello, Context API!";

  return (
    <DataContext.Provider value={data}>
      <ParentComponent />
    </DataContext.Provider>
  );
};

// Intermediate parent component
const ParentComponent = () => {
  return (
    <div>
      <ChildComponent />
    </div>
  );
};

// Deeply nested child component
const ChildComponent = () => {
  // Accessing the context value
  const data = useContext(DataContext);

  return (
    <div>
      <p>{data}</p>
    </div>
  );
};
```

By using the Context API, the ChildComponent can directly access the data prop without involving its parent (ParentComponent). This results in cleaner, more maintainable code.

## Alternative Solutions
- **Redux or MobX:** State management libraries like Redux or MobX can be used to centralize and manage state across the application, reducing the need for props drilling.

- **Component Composition:** Instead of passing data down through props, consider breaking down complex components into smaller, more focused components. Each component should have a single responsibility, promoting better modularity.

## Final Remark
While props drilling might be a quick solution in small applications, it becomes problematic as the codebase expands. Embracing the Context API or other state management solutions is crucial to preserve a scalable and maintainable React codebase.

## Sources
- [React Context](https://legacy.reactjs.org/docs/context.html)
- [Prop Drilling In React](https://kentcdodds.com/blog/prop-drilling)
- [What is Prop Drilling in React? (And how to prevent it)](https://www.youtube.com/watch?v=MCTB_w0Guso)
