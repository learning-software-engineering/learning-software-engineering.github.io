# Using ChartJS with React

## Table of Content
1. [Setting Up](#setting-up)
2. [Creating Line Graphs](#creating-bar-graphs)
3. [Creating Bar Graphs](#creating-bar-graphs)
4. [Additional Resources](#additional-resources)

## Setting Up
This tutorial assumes basic React knowledge and that a React project has been set up locally. 

If you are completely new to React, the [official documentation](https://react.dev/learn) is a great place to get started on the basic React concepts.

If you have not set up React locally yet, checkout the React official documentation [here](https://react.dev/learn/installation) or the popular tool [Create React App](https://create-react-app.dev/docs/getting-started) to set up a React application.

We will be adding two dependencies to work with ChartJS in React:
- `chart.js`
- `react-chartjs-2`

**Note:** `react-chartjs-2` is a wrapper library for `chart.js`. It is particularly helpful for visualizing data in React applications as it allows us to directly import elements from `chart.js` as resuable React components.

To add the libraries, open the terminal from your React project folder and run the following command:

```
npm install chart.js react-chartjs-2
```
Then, start your React project by running:

```
npm start
```

## Creating Line Graphs

#### Create a Component
To create a line graph component in React using ChartJS, you can begin by creating a new folder called `components` inside the `src` folder. Then, inside the `components` folder, create a new file named `LineChart.js`.

#### Import Libraries
Navigate to the newly created component and add the following import statements at the top of your file:

```
import React from "react";
import Chart from "chart.js/auto";
import { Line } from "react-chartjs-2";
```

#### Define the Data
Before creating graphs, we first need to define some data to be visualized. 
**Note:** Even though we are defining static data in this tutorial, the data can be fetched dynamically if your application has a backend.

In the same component, add the following label and data definitions:

```
const data = {
  labels: ["Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday", "Sunday"],
  datasets: [
    {
      label: "My First dataset",
      backgroundColor: "rgba(53, 162, 235, 0.5)",
      borderColor: "rgb(53, 162, 235)",
      data: [0, 5, 20, 15, 45, 5, 35],
    },
  ],
};
```

#### Visualize the Data
Now that we have the data, we can visualize it by passing the data as a prop into the `Line` component imported from `react-chartjs-2` as follow:

```
export default function const LineChart() {
  return (
    <div>
      <Line data={data} />
    </div>
  );
};
```

Now, you can use the completed `LineChart.js` component by importing it as needed.

## Creating Bar Graphs

#### Create a Component
To create a bar graph component in React using ChartJS, you can begin by creating a new folder called `components` inside the `src` folder. Then, inside the `components` folder, create a new file named `BarChart.js`.

#### Import Libraries
Navigate to the newly created component and add the following import statements at the top of your file:

```
import React from "react";
import Chart from "chart.js/auto";
import { Bar } from "react-chartjs-2";
```

#### Define the Data
Before creating graphs, we first need to define some data to be visualized. 
**Note:** Even though we are defining static data in this tutorial, the data can be fetched dynamically if your application has a backend.

In the same component, add the following label and data definitions:

```
const data = {
  labels: ["Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday", "Sunday"],
  datasets: [
    {
      label: "My First dataset",
      backgroundColor: "rgba(53, 162, 235, 0.5)",
      borderColor: "rgb(53, 162, 235)",
      data: [0, 5, 20, 15, 45, 5, 35],
    },
  ],
};
```

#### Visualize the Data
Now that we have the data, we can visualize it by passing the data as a prop into the `Bar` component imported from `react-chartjs-2` as follow:

```
export default function const BarChart() {
  return (
    <div>
      <Bar data={data} />
    </div>
  );
};
```

Now, you can use the completed `BarChart.js` component by importing it as needed.

## Additional Resources
`chart.js` and `react-chartjs-2` supports many different types of graphs beyond the ones outlined in this tutorial. The libraries also allow users to customize graph options such as styling, scaling, animation and tooltips. For more information on these additional options, check out the following resources:

1. `react-chartjs-2` official [documentation](https://react-chartjs-2.js.org/)
2. `chart.js` official [documentation](https://www.chartjs.org/docs/latest/)