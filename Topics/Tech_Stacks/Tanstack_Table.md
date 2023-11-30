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

// Converts your typescript type into an object that the library can use effectively
const columnHelper = createColumnHelper<Dog>()

// Tells the library how you should render the columns
// If you want columns to be grouped together you can define it here as well. 
// See: https://tanstack.com/table/v8/docs/guide/grouping
const defaultColumns = [
  // Display Column, the accessor() function takes the name of the attribute you want to display.
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

// Follows the same format as Dog[]
const exampleData = [
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

Next, we can begin writing our component.

```tsx
import { useReactTable } from '@tanstack/react-table'

/* Insert code from above */

function DogTable() {
  const table = useReactTable({
    columns,
    data
    // You can insert other options you want to add to your table, such as being able to resize, the columns, sorting methods, etc.
  })
  
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
}
```