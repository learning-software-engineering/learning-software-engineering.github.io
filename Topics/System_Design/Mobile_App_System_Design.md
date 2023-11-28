# Essential Elements of Mobile App System Design

## Introduction
For the last 15 years, mobile apps have emerged as vital tools in our daily lives. The best mobile apps simplify our lives by helping us with daily tasks. What lies behind these apps is a thoughtful system design that has important considerations that differ from traditional desktop devices and must be taken into account when mobile app system design, namely: UI and Performance.


## User Interface Design

### 1. Screen Size
Compared to desktops, mobile screens are much smaller. The smaller screen size requires specific design considerations, in particular, mobile apps should prioritize essential features and focus on presenting relevant content. For example, in an e-commerce mobile app, the focus should be on the products being sold, in particular, the images of the products with more detailed information being hidden but still seamlessly accessible.

### 2. Touch Interface
The touch interface of mobile devices should be also kept in mind when designing mobile applications. Unlike mouse clicks, touch interactions are not as precise, requiring designing larger and more accessible touch targets. In the example of an e-commerce mobile app, the sold products should all have a large image that is tapable and clearly separated from the other products. A Sub consideration of the touch interface is also that most users operate their devices with one hand and therefore tap using the thumb. Therefore any important elements to an application should be at the bottom of the screen. For example, on Instagram, the navigation bar is at the bottom of the screen so it is easily accessible to the thumb of the user.

### 3. Contextual Use
Mobile apps are often used on-the-go, requiring a user experience such that any important functions can be done by quick and efficient interactions. To illustrate this a good example is Uber. The Uber app would often be used in situations where the user is outside or not necessarily in a situation where they want to take their time. The Uber app is clearly designed with this in mind requiring only three taps from opening the app to ordering a ride fulfilling its main function. 

## Performance 

### 1. Battery Life 
Mobile devices run on a battery and more often than not will be used in circumstances where the device is not connected to a power source. Therefore mobile apps should be designed to minimize battery usage, which can be achieved by reducing background activity and using power-efficient APIs. If an app causes the battery life to decrease more rapidly it could lead to user dissatisfaction. To expand on the power-efficient APIs, APIs should serve only the bare-minimum content needed for the app to work to limit the amount of information that is parsed and the number of API calls (In the case of a REST API) should be also reduced as much as possible to reduce the amount of processing power needed thus preserving batter life. 

### 2. Resource Constraints 
The hardware resources available to a mobile device are more limited when compared with a desktop. Therefore it is essential to use resources efficiently to prevent slow response times or app crashes. In general, any computationally expensive task should be outsourced to the backend if the application has one. For example, if an image is served in a mobile app the size of the image should be optimized to accommodate for the resource limitations faced by the mobile device. Another good example is that if an app is implementing a feed or a long list, lazy loading is essential as it will significantly reduce the initial load times of the desired screen.

### 3. Network Variability
As stated earlier mobile apps are often used on the go, which also means that the network strength may vary. With that in mind, mobile apps should minimize the number of API calls made to the backend. Apps should also cache the data retrieved from a backend API, that is store the retrieved data in a local data store like SQLite on Android or Core Data on iOS. A caching policy should be designed for the application, for example, the app should only make an API call if a particular piece of data is not available in the cache or a sufficient amount of time has passed thus assuming that the data could have changed. Caching will also improve performance, limiting the need for API calls while also making the app less reliant on a strong network.
