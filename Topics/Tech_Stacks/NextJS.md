# Learning Next.js, a React Framework

## Table of Contents
### [Introduction](#introduction-1)
### [What is Next.js](#what-is-nextjs-1)
### [Getting Started](#getting-started-1)
### [Next.js Basics](#nextjs-basics-1)
### [Pages and Routing](#pages-and-routing-1)
### [Dynamic Routes](#dynamic-routes-1)
### [API Routes](#api-routes-1)
### [Styling in Next.js](#styling-in-nextjs-1)
### [Optimizations](#optimizations-1)
### [References](#references-and-links-1)

## Introduction
This guide will help you understand the fundamentals of Next.js, a powerful React framework designed for building modern web applications. Before diving into Next.js, it's recommended to have a basic understanding of React and JavaScript. If you need to brush up on React, please checkout our [React page](react).

## What is Next.js
Next.js is a React framework known for simplifying the development of React applications with a focus on server-side rendering, efficient routing, and improved developer experience. Its file-system-based router supports layouts, nested routing, loading states, and error handling. Next.js offers both client-side and server-side rendering, utilizing Client and Server Components for optimized rendering. The framework streamlines data fetching with async/await in Server Components and extends the fetch API for features like request memoization and data caching. Next.js supports various styling methods, including CSS Modules, Tailwind CSS, and CSS-in-JS. Furthermore it includes optimizations for images, fonts, and scripts to improve Core Web Vitals and user experience. For these reasons it is a popular choice for building full-stack web applications.

## Getting Started
To begin using Next.js, you need to set up a new project. To create a project run the following command:

`npx create-next-app@latest`

You will then see some prompts that ask for details of your application. Once this is completed, a new folder with your project name should be created!

If you need to install manually or for a more detailed guide, please follow the official guide on [getting started with Next.js](https://nextjs.org/docs/getting-started/installation).

## Next.js Basics
Once your Next.js project is set up, you can start exploring its basic features.

### Components
Next.js utilizes React components. You can create components in the `components` directory and use them throughout your application. This is the same as with standard React apps.

### Pages and Routing
One notable feature of Next.js is the automatic routing of pages. In Next.js, each file inside the `pages` directory becomes a route. For example, a file named `about.js` inside `pages` will be accessible at the `/about` route. This simple and intuitive routing system helps you structure your application without having to manually add routes like in standard React apps.

### Optimizations
Next.js optimizes performance and efficiency in many ways. One such optimization is the Image component. We import the component as follows:

`import Image from 'next/image'`

Since the Image component extends the HTML `<img>` element, you can use the standard HTML attributes such as `src`, `alt`, etc. The Image component will automatically perform optimizations such as size optimizations, faster page loads, and visual stability.

There are many more optimzations the Next.js offers. To learn more, please visit the [optimizing page](https://nextjs.org/docs/app/building-your-application/optimizing) on the official documentation.

### Dynamic Routes
Next.js supports dynamic routes, allowing you to create pages with dynamic content. For example, a file named `[id].js` inside `pages/posts` can match routes like `/posts/1`, `/posts/2`, and so on. This enables you to build flexible and dynamic applications.

### API Routes
Next.js allows you to create API routes easily. By adding files to the `pages/api` directory, you can define serverless functions that handle API requests. This feature simplifies the development of server-side logic without the need for a dedicated server.

## Styling in Next.js
Styling in Next.js can be done using various approaches. You can use CSS modules, styled-jsx, or integrate popular styling libraries like Tailwind CSS or SCSS. The choice of styling method depends on your project requirements and personal preferences.

## References and Links
- [Official Next.js Documentation](https://nextjs.org/docs/getting-started)
- [React Documentation](https://react.dev/)
- [Next.js Dynamic Routes](https://nextjs.org/docs/routing/dynamic-routes)
- [Next.js API Routes](https://nextjs.org/docs/api-routes/introduction)
- [Next.js Styling](https://nextjs.org/docs/basic-features/built-in-css-support)
- [Next.js Optimizing](https://nextjs.org/docs/pages/building-your-application/optimizing)
- [Tailwind CSS Documentation](https://tailwindcss.com/docs)
