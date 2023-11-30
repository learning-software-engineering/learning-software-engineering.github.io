# How to Build Customizable Tables in React

## Introduction
Tanstack Table is a modern, headless UI library for building powerful and interactive tables in React applications. Known for its flexibility and performance, it allows developers to create tables that can handle large datasets with ease. This article assumes you are working with React 17 or later, possibly in a project initialized with Create React App.

## Why use it?
This library is designed to be headless, meaning that it doesn't ship with any inherent styling, and instead relies on the developer to style all features related to the table. The benefit of this is that if your preferred UI library in React does not provide any built-in advanced table functionality, you can customize Tanstack table to fit all your needs easily without needing to override any preexisting styles.

## Prerequisites
Before integrating Tanstack Table, ensure your environment has:
- React 17 or later.
- Typescript 5 or later.
- Node.js 12 or later.
To check your React version, run `react -v` in your terminal. For Node.js, use `node -v`.
Although Typescript is not fully required, it is highly recommended for this library and in general as it reinforces best practices with adding types to your Javascript code. With typescript, we can better define the table columns for other developers and the library does a lot of inference based on the types that you provide it.

## Installation
To install Tanstack Table, open your terminal and navigate to your project directory. Run one of the following commands:
- Using npm: `npm install @tanstack/react-table`
- Using Yarn: `yarn add @tanstack/react-table`

## Basic Setup
Start by importing Tanstack Table into your React component:
```typescript
import { useTable } from '@tanstack/react-table';
```

## Creating a simple table

To begin with, we will define the columns of our table. Say that we want to create the following table:

| Dog Breed       | Dog Name     | Dog Size    |
|-----------------|--------------|-------------|
| Labrador        | Bella        | 1.0         |
| Beagle          | Max          | 1.2         |
| German Shepherd | Luna         | 2.0         |
| Poodle          | Charlie      | 1.6         |
| Bulldog         | Daisy        | 1.0         |
| Chihuahua       | Rocky        | 0.8         |
| Siberian Husky  | Coco         | 1.4         |

Luckily, this is easy to do with Typescript. 

```typescript
// Define the shape of your columns
type Dog = {
    dogBreed: string
    dogName: string
    dogSize: number
}
```
First, we'll define the type of data that each of our columns should hold. We can also define some example data to provide our table.
```typescript
const exampleData: Dog[] = [
    {
        "dogBreed": "Labrador",
        "dogName": "Bella",
        "dogSize": 1.0
    },
    {
        "dogBreed": "Beagle",
        "dogName": "Max",
        "dogSize": 1.2
    },
    {
        "dogBreed": "German Shepherd",
        "dogName": "Luna",
        "dogSize": 2.0
    },
]
```
Our data does not need to exist as a constant, it can also be stored as a state variable in React, allowing you to change data on the fly and have the table react accordingly.

Next, we'll tell the library how we want it to render our columns. Here, you can customize the rendering method for each column however in this example, we have opted to use the default method. If you would like to learn more about special cell formatting, [click here](https://tanstack.com/table/v8/docs/guide/column-defs#cell-formatting). 
```typescript
// Converts your typescript type into an object that the library can use effectively
const columnHelper = createColumnHelper<Dog>()

// Tells the library how you should render the columns
// If you want columns to be grouped together you can define it here as well. 
// See: https://tanstack.com/table/v8/docs/guide/grouping
const defaultColumns = [
  columnHelper.accessor("dogBreed", {
    header: "Dog Breed",
    cell: (info) => info.getValue(),
  }),
  columnHelper.accessor("dogName", {
    header: "Dog Name",
    cell: (info) => info.getValue(),
  }),
  columnHelper.accessor("dogSize", {
    header: "Dog Size",
    cell: (info) => info.getValue(),
  })
]
```
Note: The accessor() function takes the name of the attribute you want to display.

Next, we can begin writing our full component, here's the code that we have so far:

```tsx
import { useReactTable } from '@tanstack/react-table'

type Dog = {
    dogBreed: string
    dogName: string
    dogSize: number
}

const exampleData: Dog[] = [
    {
        "dogBreed": "Labrador",
        "dogName": "Bella",
        "dogSize": 1.0
    },
    {
        "dogBreed": "Beagle",
        "dogName": "Max",
        "dogSize": 1.2
    },
    {
        "dogBreed": "German Shepherd",
        "dogName": "Luna",
        "dogSize": 2.0
    },
]

const columnHelper = createColumnHelper<Dog>()

const defaultColumns = [
  columnHelper.accessor("dogBreed", {
    header: "Dog Breed",
    cell: (info) => info.getValue(),
  }),
  columnHelper.accessor("dogName", {
    header: "Dog Name",
    cell: (info) => info.getValue(),
  }),
  columnHelper.accessor("dogSize", {
    header: "Dog Size",
    cell: (info) => info.getValue(),
  })
]

function DogTable() {
  const table = useReactTable({
    columns,
    data
    // You can insert other options you want to add to your table, such as being able to resize, the columns, sorting methods, etc.
  })

  return (
    ...
  )
}
```

For the final implementation, we need to render the table in the return function.

In the return function of the DogTable component, add the following code: 
```tsx
return (
    <table>
        <thead>
            {table.getHeaderGroups().map(headerGroup => (
                <tr key={headerGroup.id}>
                    {headerGroup.headers.map(header => (
                    <th key={header.id}>
                        {flexRender(
                            header.column.columnDef.header,
                            header.getContext()
                        )}
                    </th>
                    ))}
                </tr>
            ))}
        </thead>
        <tbody>
            {table.getRowModel().rows.map(row => (
                <tr key={row.id}>
                    {row.getVisibleCells().map(cell => (
                    <td key={cell.id}>
                        {flexRender(
                            cell.column.columnDef.cell,
                            cell.getContext()
                        )}
                    </td>
                    ))}
                </tr>
            ))}
        </tbody>
    </table>
)
```

This tells Tanstack Table to grab every single header we've provided it, and render each one in the ordinary table header HTML tag `<th>`

For the row data, it repeats the exact same process but in `<tbody>` and with `<tr>`

## Conclusion

As we've shown, this is an extremely flexible model for building customizable tables. With this example, you can extend it further by changing how the table cells are rendered, either through CSS styling, tailwind styling, or mixing it with an entirely different UI library. 

If you are interested in exploring how to build sorting functionality, you can explore it [here](https://tanstack.com/table/v8/docs/api/features/sorting).

With this library you can also build extendable [filters](https://tanstack.com/table/v8/docs/api/features/filters), similar to the ones you would find in powerful applications such as Excel or Google Sheets.

More resources on [pagination](https://tanstack.com/table/v8/docs/api/features/pagination), [pinning](https://tanstack.com/table/v8/docs/api/features/pinning) are also available.