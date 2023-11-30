## Introduction to Matplotlib
### What is Matplotlib?
Matplotlib is a powerful, versatile library in Python used for creating static, interactive, and animated visualizations. It was initially developed by John D. Hunter in 2003 and has since become a fundamental tool in the data science and analytics community.

### What is pyplot?
- `pyplot` is a module in the Matplotlib library – a widely used data visualization library in Python. 
- It provides an interface that is similar to MATLAB's plotting functions, making it familiar to users of MATLAB and easy to use for beginners in Python. 
- The `pyplot` module contains functions that allow you to create a figure, plot area, decorate the plot with labels, etc., and essentially control the overall layout and presentation of your data in a graphical format.

### Why Matplotlib?
1. **versatility**: Matplotlib allows you to create a wide range of graphs and plots, including line plots, scatter plots, bar charts, histograms, 3D plots, and much more.

2. **Ease of Use**: Its simple syntax and commands make it accessible to beginners while still being powerful enough for advanced users.
   
3. **Integration with Python**: Matplotlib integrates with other Python libraries like NumPy and pandas, making it a cornerstone in the Python data visualization ecosystem.
   
4. **Customization**: It offers extensive customization options, enabling you to tailor your graphs and plots to your exact needs.

## Setting Up the Environment for Matplotlib
Before diving into the real application, this section will teach you how to set up your Python environment for Matplotlib. 

### Installing Matplotlib
You can install it using Python's package manager, `pip`. Here are the steps:
1. **Open your terminal or command prompt**

2. **Ensuring you have Python installed:** You can check this by typing `python --version` at your opened terminal. If Python is not installed, download and install it from [python.org](https://www.python.org/)
3. **Install Matplotlib** by typing the following command
```
pip install matplotlib
```

### Test Your Setup
To ensure that Matplotlib is installed correctly and your environment, try running a simple test:
```python
# First import matplotlib at the beginning of your test file
import matplotlib.pyplot as plt
plt.plot([1, 2, 3, 4])
plt.ylabel("Some number")
plt.show()
```
If you see a line chart, then congratulation! Your environment set up correctly. 

## Basic Concepts of Matplotlib
This section will introduce you to the core components of Matplotlib, namely **figures, axes, and plots**, along with an overview of the pyplot interface. 

### Introduction to core concepts
#### Figure:
The entire window or page where the graph displayed on. Think it as a canvas where you can draw your graph on. Note that A figure can contains may axes. 

#### Axes
An axes object is a part of a figure where we plot our data, it can contain two(2D) or three(3D) axis objects representing the X, Y and Z axes. Each axes object provides a coordinate system to plot your data. 

#### Pyplot interface
Matplotlib offers several interfaces for creating plots, but the most commonly used is `pyplot` where it is extremely convenient for interactive work. Moreover, the whole tutorial will focus on this pyplot interface:
- **Simple and Convenient**: `Pyplot` automates the creation of figures and axes, allowing you to just focus more on plotting the data.
- **Ideal for Beginners**: Its simplicity makes it very accessible for beginners.
- 
#### Understanding Plot Functions
`pyplot` module provides functions for different types of plot. Here we just show some simple examples, we will dive into them in later section. 

**plot()**
For line plot. 
Example:
```python
import matplotlib.pyplot as plt

x = [1, 2, 3, 4, 5]
y = [1, 4, 9, 16, 25]

plt.plot(x, y)
plt.title("Line Plot")
plt.xlabel("X Axis")
plt.ylabel("Y Axis")
plt.show()
```
Running this will generate a simple line showing a quadratic relationship:
![Line Plot](./images/Pasted%20image%2020231126224825.png)

**scatter()**
For Scatter plots
Example:
```python
import matplotlib.pyplot as plt

# Lists of x and y coordinates
x = [5, 20, 40, 60, 80]
y = [12, 24, 36, 48, 60]

# Size and color for each point
sizes = [100, 200, 300, 400, 500]  # Sizes of the markers
colors = ['red', 'green', 'blue', 'purple', 'orange']  # Colors of the markers

plt.scatter(x, y, s=sizes, c=colors, alpha=0.5)

plt.title("Scatter Plot")
plt.xlabel("X Axis")
plt.ylabel("Y Axis")

plt.show()

```
This will generate a scatter plot where each point has a unique size and color, based on the provided lists. 

![](./images/Pasted%20image%2020231126225111.png)

**bar()**
Example:
```python
import matplotlib.pyplot as plt

categories = ['Category A', 'Category B', 'Category C', 'Category D']
values = [23, 45, 56, 78]

plt.bar(categories, values)
plt.title("Bar Chart")
plt.xlabel("Categories")
plt.ylabel("Values")
plt.show()
```
This will generate a simple bar chart showing data in a categorical format:

![](./images/Pasted%20image%2020231126225345.png)

**hist()**
For Histograms
Example:
```python
import matplotlib.pyplot as plt
import numpy as np

data = np.random.normal(100, 20, 200)

plt.hist(data, bins=20, color='blue', alpha=0.7)
plt.title("Histogram")
plt.xlabel("Data Values")
plt.ylabel("Frequency")
plt.show()
```
This will generate a histogram showing the distribution of a dataset. 

![](./images/Pasted%20image%2020231126225540.png)


## Customizing Plots in Matplotlib
Creating effective visualizations in Matplotlib involves more than just plotting data; it's about making the data speak. Customizing plots is crucial for clarity, aesthetics, and making complex data more understandable. This section will guide you through various customization options in Matplotlib.

### Colours, Line Styles and Markers
In Matplotlib, the visual appeal and clarity of a plot can be significantly enhanced by customizing its colors, line styles, and markers. Here are some ways to use these features:

We will demonstrate our examples by initializing
```python
x = [1, 2, 3, 4]
y = [1, 4, 9, 16]
z = [1, 2, 3, 4]
```
1. **Colors**: Change the color of the plot lines.
    - Example:
```python
plt.plot(x, y, color='green')
plt.show()
```

 - ![](./images/Pasted%20image%2020231127110532.png)

1. **Line Styles**: Alter the style of the plot lines.
    - Example:
```python
plt.plot(x, y, linestyle='dashed')
plt.show()
```

 - ![](./images/Pasted%20image%2020231127110651.png)
1. **Markers**: Add markers to your plot points.
    - Example: 
```python
plt.plot(x, y, marker='o')
plt.show()
```
- ![](./images/Pasted%20image%2020231127110736.png)

### Adding Labels, Titles, and Legends
Effective labeling is key to making plots understandable and informative.

1. **Labels**: Add labels to the x and y axes.
2. **Titles**: Add a title to your plot.
3. **Legends**: Incorporate legends when plotting multiple datasets.
Example of putting labels, titles, legends into one plot. 
```python
plt.plot(x, y)
plt.plot(x, z)
plt.xlabel('Time')
plt.ylabel('Value')
plt.title('My plot title')
plt.legend(['x and y', 'x and z'])
plt.show()
```
- ![](./images/Pasted%20image%2020231127111257.png)


### Adjusting Axes
Controlling the axes in Matplotlib allows for better representation of data.
1. **Axis Limits**: Set the range of the axes you want to see.
    - Example:
```python
x = range(-1000, 1000)
y = range(-2000, 2000, 2)
plt.plot(x, y)
plt.xlim(0, 10) 
plt.ylim(-1, 1)
plt.show()
```
- Graph without adding axis limits:
- ![](./images/Pasted%20image%2020231127112426.png)
- Applying the axis limits we can get:
- ![](./images/Pasted%20image%2020231127112338.png)
1. **Tick Marks**: Customize the ticks on the axes for better precision.
```python
x = range(0, 10)  
y = range(-10, 0)  
plt.plot(x, y)  
plt.xticks([0, 2,4, 8, 10])  
plt.yticks([-1, 0, 1])  
plt.title("Customized Tick Marks")  
plt.show()
```

- ![](./images/Pasted%20image%2020231127112911.png)

### Grids
Gridlines are helpful for reading and interpreting graphs more easily.
    - Example: 
```python
x = range(0, 10)
y = range(0, 10)
plt.plot(x, y)  
plt.grid(True)  
plt.title("Graph with grid lines show")  
plt.show()
```

- ![](./images/Pasted%20image%2020231127113201.png)

### Annotating Plots
Properly labeled axes and a descriptive title can greatly enhance the understandability of a plot.
1. **Text Annotations**: Add text annotations to highlight key points.
```python
x = range(0, 10)
y = range(0, 10)
plt.plot(x, y, marker = 'o')  
plt.text(5, 5, 'Important Point')  
plt.title("Graph with text annotation")  
plt.show()
```

- ![](./images/Pasted%20image%2020231127113641.png)
2. **Arrows**: Draw arrows to direct attention.
`plt.annote()` method provides helper functionality to make annotations easy. 
- `xy`: The point (x, y) to annotate
- `xytext`: The position (x, y) to place the text at.
- `arrowprops`: The properties used to draw a arrow between the positions `xy` and `xytext`. Defaults to None, i.e. no arrow is drawn.
- Example: 
```python
x = range(0, 10)  
y = range(0, 10)  
plt.plot(x, y)  

plt.annotate('Start Here', xy=(1, 1), xytext=(0, 2), arrowprops=dict(facecolor='black'))  
plt.title("Graph with Arrow Annotated")  
plt.show()
```

- ![](./images/Pasted%20image%2020231127130606.png)


## Working with Multiple Plots and Figures in Matplotlib
Creating multiple plots and figures is essential in data visualization for comparing different datasets or aspects of data. Matplotlib provides several ways to manage and display multiple plots effectively.

### Understanding Subplots
Subplots are individual plots that exist within a single figure. They allow you to display multiple plots in a grid-like format within one figure.

#### Creating Subplots
- **Basic Subplots**: Use `plt.subplots()` to create a figure and one or more axes (subplots).
    - Syntax: `fig, axs = plt.subplots(nrows, ncols)`
    - Example: `fig, axs = plt.subplots(2, 3)` creates a 2x3 grid of subplots.

#### Indexing Subplots
- **Accessing Individual Subplots**: Each subplot in the grid can be accessed using array indexing.
    - Example: `axs[0, 1].plot(x, y)` to plot in the second subplot of the first row.

#### Customizing Individual Subplots
- **Plot Types**: Different types of plots can be used in each subplot.
- **Titles and Labels**: Each subplot can have its own title, x-label, and y-label.

#### Adding a Title to the Entire Figure
Unlike individual subplot titles, you can add a title to the whole figure by using `plt.suptitle()`

Example: 
```python
# Create a 2x2 grid of subplots
fig, axs = plt.subplots(2, 2)

# Plot data in each subplot
# Top left: Plot an plot graph
axs[0, 0].plot([1, 2, 3], [1, 2, 3])
axs[0, 0].set_title('Subplot 1')

# Top right: Plot an bar graph
axs[0, 1].bar([1, 2, 3], [3, 2, 1])
axs[0, 1].set_title('Subplot 2')

# Bottom left: Plot an scatter graph
axs[1, 0].scatter([1, 2, 3], [3, 2, 1])
axs[1, 0].set_title('Subplot 3')

# Bottom right: Plot a histogram graph
axs[1, 1].hist([1, 2, 1, 3], bins=3)
axs[1, 1].set_title('Subplot 4')

plt.suptitle("Figure of differnt types of subplots")
plt.tight_layout()
plt.show()
```

- ![](./images/Pasted%20image%2020231127121909.png)

### Adjusting the Layout

When working with multiple plots, managing the spacing and layout is crucial to ensure that the plots don't overlap and are easily readable.

If we don't adjust the layout, the graph may be overlapping and  looks something like:

- ![](./images/Pasted%20image%2020231127120702.png)
#### Spacing
- **Adjusting Spacing**: Control the space between subplots using `subplots_adjust()`.
    - Example: `plt.subplots_adjust(wspace=0.5, hspace=0.5)` adjusts the width and height spacing.
```python
# Create a 2x2 grid of subplots  
fig, axs = plt.subplots(2, 2)  
  
# Plot data in each subplot  
# Top left: Plot an plot graph  
axs[0, 0].plot([1, 2, 3], [1, 2, 3])  
axs[0, 0].set_title('Subplot 1')  
  
# Top right: Plot an bar graph  
axs[0, 1].bar([1, 2, 3], [3, 2, 1])  
axs[0, 1].set_title('Subplot 2')  
  
# Bottom left: Plot an scatter graph  
axs[1, 0].scatter([1, 2, 3], [3, 2, 1])  
axs[1, 0].set_title('Subplot 3')  
  
# Bottom right: Plot a histogram graph  
axs[1, 1].hist([1, 2, 1, 3], bins=3)  
axs[1, 1].set_title('Subplot 4')  
  
plt.suptitle("Subplots with adjusting the layout by Spacing")  
plt.subplots_adjust(wspace=0.5, hspace=0.5)  
plt.show()
```

- ![](./images/Pasted%20image%2020231127120818.png)

#### Automatic Adjustment
- **Using `tight_layout()`**: This method automatically adjusts subplot params to fit the figure area neatly.
    - Syntax: `plt.tight_layout()`
    - The example is showed at section: Understanding Subplots

#### Shared Axes
For comparative visualizations, you might want to share the x or y-axis across multiple plots.
- **Shared Axis**: Use the `sharex` and `sharey` parameters.
    - Example: `plt.subplots(2, 2, sharex='col', sharey='row')` shares x-axis across columns and y-axis across rows.
```python
# Sample data  
x = [1, 2, 3, 4, 5]  
y1 = [i ** 2 for i in x]  # Quadratic relationship  
y2 = [i ** 1.5 for i in x]  # Power relationship  
  
# Create two subplots, sharing the x-axis  
fig, (ax1, ax2) = plt.subplots(2, sharex=True)  
  
# Plot on the first subplot  
ax1.plot(x, y1, color='r')  
ax1.set_title('Quadratic Relationship')  
ax1.set_ylabel('y1 values')  
  
# Plot on the second subplot  
ax2.plot(x, y2, color='b')  
ax2.set_title('Power Relationship')  
ax2.set_ylabel('y2 values')  
ax2.set_xlabel('Shared X-axis')  
  
plt.tight_layout()  
plt.show()
```

- ![](./images/Pasted%20image%2020231127121648.png)

## Advanced Plot Types in Matplotlib
Matplotlib provides several advanced plot types for specialized data visualization needs. Here, we'll explore histograms, boxplots, heatmaps, 3D plots, and radar plots in more detail.

### Histogram
Histograms are powerful tools in data analysis for visualizing the distribution of data sets. They show how many data points fall into specified ranges (bins) and are crucial for understanding the spread and shape of your data.
#### Basic  Histogram Creation
First generate some sample data
```python
# Generate Sample data
import numpy as np
data = np.random.normal(100, 20, 1000)
```
Create a histogram using `plt.hist()`:
```python
plt.hist(data, bins = 30)
plt.show()
```

- ![](./images/Pasted%20image%2020231127131857.png)


#### Histogram Customization
1. **hanging Bin Size**: Adjust the `bins` parameter. Fewer bins simplify the histogram but may obscure details.
```python
plt.hist(data, bins=15)
```

- ![](./images/Pasted%20image%2020231127132239.png)


2. **Changing Colors and Transparency**: Use the `color` and `alpha` parameters for aesthetic adjustments.
```python
plt.hist(data, bins=30, color='green', alpha=0.5)
```
- ![](./images/Pasted%20image%2020231127132335.png)



### Boxplots
Boxplots provide a concise summary of the distribution of data, showing the median, quartiles, and outliers.
#### Boxplots creation:
Just like the histograms, we first generate an example dataset for boxplots
```python
import numpy as np
data = np.random.normal(0, 1, 100)
```
After this, just call `plt.boxplot()` on the generated data 
```python
plt.boxplot(data)
plt.show()
```
- ![](./images/Pasted%20image%2020231127133958.png)

Understanding Boxplots Element:
- **Central Box**: Represents the interquartile range (IQR), the middle 50% of the dataset.
- **Horizontal Line in the Box**: Indicates the median.
- **Whiskers**: Extend to show the range of the data. Their length can be adjusted.
- **Outliers**: Points lying beyond the whiskers are often considered outliers.

#### Customizing Boxplots
We will create a subplot and see how does the customized boxplots differs from non-customized boxplot. 
```python
fig, axs = plt.subplots(2, tight_layout = True)  
axs[1].boxplot(data)  
axs[1].set_title("Non-customized Box Plot")
```
1. **Changing Whiskers Length**
```python
# Whiskers cover 5th to 95th percentile
axs[0].boxplot(data, whis=[5, 95])  
axs[0].set_title("Customized Whiskers Length")
```

- ![](./images/Pasted%20image%2020231127140236.png)

2. **Adding Colours**
```python
axs[0].boxplot(data, patch_artist=True, boxprops=dict(facecolor='blue'))
axs[0].set_title("Customized Colour")
```
- ![](./images/Pasted%20image%2020231127140350.png)

3. **Horizontal Boxplots**
```python
axs[0].boxplot(data, vert=False)
axs[0].set_title("Change to horizontal Boxplots")
```

- ![](./images/Pasted%20image%2020231127140633.png)


### Radar Plot
Radar plots are useful for displaying multivariate data, where each variable is represented on a separate axis that starts from the same point.
#### Basic Radar Plot Creation
Just like before, we first prepare for the data to be plot. 
- **Data Setup**: `labels` and `stats` hold your variable names and their respective values.
```python
import numpy as np
labels = np.array(['A', 'B', 'C', 'D', 'E'])  # Variable names
stats = np.array([20, 34, 30, 35, 27])  # Data points for each variable
```
- **Angle Calculation**: The radar chart is circular, so each variable needs an angle. `np.linspace` is used for even distribution.
This following line creates an array `angles` where each component corresponding to each category (label) for the radar plot.
```python
angles = np.linspace(0, 2 * np.pi, len(labels), endpoint=False).tolist()
```

Since radar plots are circular, so the starting point and the ending point need to be the same for the plot to be joined up. 
Hence we need to use
- `np.concatenate` to close the loop on the radar point 
- use `+= angles[:1]` where appends the first angle in the `angles` array to the end of `angles` array. 
```python
stats = np.concatenate((stats,[stats[0]]))
angles += angles[:1]
```

- **Plot Setup**: `subplot_kw=dict(polar=True)` converts the subplot to polar coordinates, essential for a radar chart.
```python
fig, ax = plt.subplots(figsize=(6, 6), subplot_kw=dict(polar=True))
```

- **Data Plotting**: `ax.fill` fills the area under the plot. `angles` and `stats` are used to plot data points.
```python
ax.fill(angles, stats, alpha=0.25)
ax.set_yticklabels([])
ax.set_xticks(angles[:-1])
ax.set_xticklabels(labels)
plt.show()
```

- ![](./images/Pasted%20image%2020231127143330.png)


#### Customizing Radar Plot
1. **Changing Color and Transparency**: Adjust the color and transparency of the plot.
```python
ax.fill(angles, stats, color='blue', alpha=0.4)
```
- ![](./images/Pasted%20image%2020231127144512.png)

3. **Adjusting Line Style**: Change the line style for the perimeter and spokes.    
```python
ax.plot(angles, stats, linestyle='dashed', color='black')
```
- ![](./images/Pasted%20image%2020231127144825.png)


