# Svelte: A Beginner's Guide

## Introduction to Svelte

Svelte is a modern JavaScript framework for building user interfaces. Unlike other frameworks like React or Vue, Svelte shifts much of the work to compile time, producing highly efficient, imperative code that updates the DOM.

## Key Features of Svelte

- **Zero-runtime overhead**: Svelte compiles your code to highly efficient, vanilla JavaScript at build time.
- **Reactivity**: Svelte makes state management simple and intuitive.
- **Component-based**: Build encapsulated components that manage their own state.

## Setting Up a Svelte Project

### Prerequisites

- Node.js installed on your system.

### Steps to Create a New Svelte Project

1. **Install the Svelte template**:
   Open your terminal and run:

    ```
    npx degit sveltejs/template svelte-app
    ```

2. **Navigate to your new project**:

    ```
    cd svelte-app
    ```

3. **Install dependencies**:

    ```
    npm install
    ```

4. **Start the development server**:

    ```
    npm run dev
    ```

### Project Structure

- `src`: Contains your Svelte components.
- `public`: Contains static assets.

## Basic Functionalities in Svelte

### Components

- Svelte applications are built with components. A Svelte component is a `.svelte` file.
- Components can contain HTML, CSS, and JavaScript.

### Reactivity

- Svelte's reactivity is straightforward. Just assign a new value to a variable, and the framework updates the DOM.
- Use `$:` to create reactive statements.

### Conditional Rendering

- Use `{#if}` and `{/if}` to conditionally render parts of your component.

### Loops

- Use `{#each}` and `{/each}` to iterate over arrays.

### Event Handling

- Use `on:eventname` to handle events.

### Bindings

- Bind values to your inputs using the `bind:value` syntax.

## Learning Resources

- **Official Documentation**: Visit [Svelte's official documentation](https://svelte.dev/docs) for comprehensive and detailed guides.
- **Tutorial Videos**: https://www.youtube.com/watch?v=zojEMeQGGHs
- **Advanced Concept: Store** https://www.youtube.com/watch?v=T64FIL1ii-0
   - https://svelte.dev/docs/svelte-store

## Conclusion

Svelte offers a unique approach to building web applications with its compile-time magic. It's simple, fast, and easy to learn, especially for those familiar with HTML, CSS, and JavaScript.

## Next Steps

- Explore Svelte's official tutorials and examples.
- Build a simple project to get hands-on experience.
- Join the Svelte community for support and to stay updated.

# Svelte Lifecycle Functions Guide (Extra Material)

Svelte offers several lifecycle functions that help manage different stages in the lifecycle of a component. These functions are crucial for tasks like resource management, initializing functionality, and cleaning up before a component is destroyed.

## onMount

### Description
`onMount` is used for code that needs to run after the component is initially rendered to the DOM. It's especially useful for tasks that require DOM elements to be present.

### Example Usage

    import { onMount } from 'svelte';

    onMount(() => {
        // Code that runs after the component is mounted
    });

## onDestroy

### Description
`onDestroy` is invoked right before the component is removed from the DOM. It's the perfect spot for cleaning up to prevent memory leaks, such as removing event listeners or canceling subscriptions.

### Example Usage

    import { onDestroy } from 'svelte';

    onDestroy(() => {
        // Cleanup code
    });

## beforeUpdate and afterUpdate

### Description
- `beforeUpdate` runs before the component's DOM is updated in response to state changes.
- `afterUpdate` is called after the component's DOM has been updated.

These functions are great for tasks that need to be executed right before or after the DOM updates, like recalculating layout or reading DOM measurements.

### Example Usage

    import { beforeUpdate, afterUpdate } from 'svelte';

    beforeUpdate(() => {
        // Code that runs before DOM updates
    });

    afterUpdate(() => {
        // Code that runs after DOM updates
    });

## tick

### Description
`tick` is a function that returns a promise. This promise resolves after Svelte has made changes to the DOM in response to state changes. It's useful for coordinating DOM updates with asynchronous operations.

### Example Usage

    import { tick } from 'svelte';

    async function updateAndAct() {
        // Make state changes
        await tick();
        // Code that runs after the DOM has updated
    }
