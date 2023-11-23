# Using shadcn/ui

## Table of Contents

#### [Introduction](#introduction-1)

#### [Installation](#installation-1)

#### [Example: Creating and Customizing a Button Component](#example-creating-and-customizing-a-button-component-1)

#### [Resources](#resources-1)

## Introduction

### What is shadcn/ui?

[Shadcn/ui](https://ui.shadcn.com/) is a component library that gives you the ability to use re-usable components that are built using [Radix UI](https://www.radix-ui.com/) and [Tailwind CSS](https://tailwindcss.com/). You are able to choose from their collection of pre-built components, add the code into your project, and then customize them using cva variants.

### Why use shadcn/ui?

Shadcn/ui helps you separate the design of your components from the implementation. This way, using shadcn/ui is a very modular and easy process. Additionally, there is no requirement to install any package; you only need to install the specific components you'd like to use.

### What to Expect

This document will go over how to install and integrate shadcn/ui into your project. Then, it will go through an example of building a `Button` component into your project and talk through the details in customizing it.

## Installation

You can use shadcn/ui components in any framework that supports React. Typescript is recommended for your projects but Javascript components are also available by making changes to your configurations.

Follow any of the links below depending on the framework you are using for your project:

- [Next.js](https://ui.shadcn.com/docs/installation/next)
- [Vite](https://ui.shadcn.com/docs/installation/vite)
- [Remix](https://ui.shadcn.com/docs/installation/remix)
- [Gatsby](https://ui.shadcn.com/docs/installation/gatsby)
- [Astro](https://ui.shadcn.com/docs/installation/astro)
- [Laravel](https://ui.shadcn.com/docs/installation/laravel)

If you want to manually install shadcn/ui, follow this [tutorial](https://ui.shadcn.com/docs/installation/manual).

## Example: Creating and Customizing a Button Component

<!-- This [document](https://ui.shadcn.com/docs/components/button) shows the steps you need to take in order to install and use a `Button` component in your project.  -->

In this example, we will walk through the steps to install, use, and customize a `Button` component in your own project:

1. **Installation:** Add the `Button` component to your project

   ```bash
   # npm
   npx shadcn-ui@latest add button

   # yarn
   npx shadcn-ui@latest add button

   # pnpm
   pnpm dlx shadcn-ui@latest add button

   # bun
   bunx --bun shadcn-ui@latest add button
   ```

   This will add a `button.tsx` file into `components/ui`.

   #### button.tsx

   ```Typescript
   import * as React from "react"
   import { Slot } from "@radix-ui/react-slot"
   import { cva, type VariantProps } from "class-variance-authority"

   import { cn } from "@/lib/utils"

   const buttonVariants = cva(
   "inline-flex items-center justify-center whitespace-nowrap rounded-md text-sm font-medium ring-offset-background transition-colors focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-ring focus-visible:ring-offset-2 disabled:pointer-events-none disabled:opacity-50",
   {
       variants: {
       variant: {
           default: "bg-primary text-primary-foreground hover:bg-primary/90",
           destructive:
           "bg-destructive text-destructive-foreground hover:bg-destructive/90",
           outline:
           "border border-input bg-background hover:bg-accent hover:text-accent-foreground",
           secondary:
           "bg-secondary text-secondary-foreground hover:bg-secondary/80",
           ghost: "hover:bg-accent hover:text-accent-foreground",
           link: "text-primary underline-offset-4 hover:underline",
       },
       size: {
           default: "h-10 px-4 py-2",
           sm: "h-9 rounded-md px-3",
           lg: "h-11 rounded-md px-8",
           icon: "h-10 w-10",
       },
       },
       defaultVariants: {
       variant: "default",
       size: "default",
       },
   }
   )

   export interface ButtonProps
   extends React.ButtonHTMLAttributes<HTMLButtonElement>,
       VariantProps<typeof buttonVariants> {
   asChild?: boolean
   }

   const Button = React.forwardRef<HTMLButtonElement, ButtonProps>(
   ({ className, variant, size, asChild = false, ...props }, ref) => {
       const Comp = asChild ? Slot : "button"
       return (
       <Comp
           className={cn(buttonVariants({ variant, size, className }))}
           ref={ref}
           {...props}
       />
       )
   }
   )
   Button.displayName = "Button"

   export { Button, buttonVariants }

   ```

2. **Usage:** Import the `Button` component in your project wherever you need to use it.

   ```Typescript
   import { Button } from "@/components/ui/button"
   ```

3. **Customization:** Add the imported component in your project. Edit the generated [button.tsx](#buttontsx) file and use `buttonVariants` to customize your button component.

   #### Customizing Using Variants

   The variants in your generated [button.tsx](#buttontsx) file can be used to have different styles for a Button component. See [examples](https://ui.shadcn.com/docs/components/button#examples) of how to use the different variants to style your component.

   Additionally, you can make changes to the default variants with Tailwind to fit your project's theme. You can also rename the variants or add your own variants to create more customization in your component. See below for an example of adding a new variant:

   ```Typescript
   // Customize your button.tsx file
   variant: {
           default: "bg-primary text-primary-foreground hover:bg-primary/90",
           destructive:
           "bg-destructive text-destructive-foreground hover:bg-destructive/90",
           outline:
           "border border-input bg-background hover:bg-accent hover:text-accent-foreground",
           secondary:
           "bg-secondary text-secondary-foreground hover:bg-secondary/80",
           ghost: "hover:bg-accent hover:text-accent-foreground",
           link: "text-primary underline-offset-4 hover:underline",
           // Your new variant!
           dark: "bg-foreground text-background font-bold hover:bg-background hover:text-foreground hover:border"
       },
   ```

   ```Typescript
   // Use your new variant in your Button component
   export function ButtonDark() {
        return <Button variant="dark">Dark</Button>
   }
   ```

   #### Customizing the Size

   Sizing of the component can be customized to easily create responsive designs. Similar to variants, you can customize different sizes (by editing generated sizes or adding new sizes) in [button.tsx](#buttontsx) and use them in your project:

   ```Typescript
   export function ButtonLarge() {
        return <Button size="lg">Large Button</Button>
   }
   ```

## Resources

See the shadcn/ui [documentation](https://ui.shadcn.com/docs/components/accordion) to see all the components that are available to use in your project.

Shadcn/ui uses CVA to introduce variants. See the [CVA documentation](https://cva.style/docs) to learn more about class variance authority.
