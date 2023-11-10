## Resources for User Experience domain

### Overview

User Experience (UX) is a large and broad topic. It covers the overall experience of the user and how they interact with software systems and applications. The main focus of User Experience is to make a piece of software accessible, easy to follow (ie: user-friendly) and adaptable to the user's needs. There is no set of standard rules that make up a "great" user experience, as it often differs on the product and the consumers that are using the products. User Experience is not to be confused with UI and UX Design. While these topics have similarities with User Experience, they are also different in their ways. For example, UI could be how the interface is designed whereas UX is more about how users interact with the said design. Many notable links are differentiating the two areas. Here is one of the related websites.


- [The Definition of User Experience](https://www.nngroup.com/articles/definition-user-experience/)

### Areas of User Experience

User Experience is not easy to define. There are many areas that contribute to User Experience but there is not one answer. The following are a few examples.

___Button Design___ 
- [Amazon Button](https://medium.com/@cccalibour/how-ux-design-makes-a-difference-amazons-continue-button-901618a8b00e): The design of butt
ons that improves user experience by simplifying process.

___Established Norms___
- [Scrolls On Socials](https://forgeandsmith.com/blog/scrolling-vs-clicking-whats-the-preferred-user-experience/): Users are conditioned for scrolling, and now every new social media app conforms to scrolling.

___Color Theory___
- [Colors Influence Choice](https://usabilitygeek.com/colour-user-experience-psychology/#:~:text=Colour%20plays%20a%20crucial%20role,and%20identified%20with%20your%20industry.): Users are shown certain colors to enforce actions. For example, red is commonly linked to aggressive or bad emotions and as such can be used as a cancel to dissuade people from refunding items.

___Responsive Design___
- [Responsive Design](https://devrix.com/tutorial/important-responsive-design/): Responsive Design generally refers to a design where the software is adaptable to the consumer's device. The responsive design can be many things including screen sizes, collapsing of navbars, adjusting texts based on the screens, scrolling effects and more. The benefits of a responsive design make your software accessible across varying devices and overall improves the user experience. The article demonstrates the importance and benefits of responsive design, the flexibility they provide, and the easiblity for the consumers upon making the said software. 

___Nielsen's 10 Usability Heuristics___
- [Usability Heuristics](./User_Experience/Usability_Heuristics.md)

___A/B Testing to Optimize UI___
- [A/B Testing](./User_Experience/AB_Testing.md)

### Accessibility Features of User Experience

There are some things that have become a crucial part in making a software: Universal Design Principles. 

___The 7 Universal Design Principles___
- [Universal Design Principles](https://www.buffalo.edu/access/help-and-support/topic3/universaldesignprinciples.html): Universal Design Principles are not only used for software, but can be incorporated generally as well. These 7 principles ensure accessibility, consistency, and user-friendly software. 
This article provides the 7 Universal Design Principles that makes a software accessible to all users, which plays a important role in diversifying the User Experience. 

### Helpful Courses

There are many courses related to User Experience. This includes the U of T Course [The Design of Interactive Computational Media](https://artsci.calendar.utoronto.ca/course/csc318h1) which is highly recommended if interested in this topic. [The Design of Interactive Computational Media](https://artsci.calendar.utoronto.ca/course/csc318h1) expands on the work done before coding projects. For example, one of the projects is testing how users would interact with a prototype of a UI and modifying it so that the UX is better for the user.


### Tools Can Be Used In UX Design

In addition to Bootstrap, Ant Design is another popular UI library and design system. It is specifically designed for React applications and other frontend frameworks like Vue, Angular and etc, providing a complete set of high-quality React components that make user interface development simpler, more consistent, and modular. Ant Design is ideal for building enterprise-level applications and dashboards with a focus on high performance, usability, and aesthetics.

Ant Design provides a wide range of UI components, including buttons, icons, form elements, tables, and navigation menus. It also offers a consistent design language, making it easier for developers to create appealing user interfaces. The design ensures that your applications look great on different devices and screen sizes. More importantly, it is easy to use for beginners. Following steps are provided for you to start using Ant Design in your project.

First, you need to install Ant Design in your React application. You can do this by running the following command (also you can use yarn command to install, here I provide method using npm):

**npm install antd**

Next, you may want to import the components you want to use in your application. For example, if you want to change the style for your button in a webpage, simply import Button from antd package.

**import { Button } from 'antd';**

Finally, you are almost done. All you need to do is use the imported components in your application. For example, below code is a example using Button from antd package:

function App() {
  return (
    <div className="App">
      <Button type="primary">Click me!</Button>
    </div>
  );
}

export default App;


Besides, Ant Design allows you to customize the default theme by modifying the less variables. For instance, you can use tools like 'craco-less' or 'react-app-rewired' to customize your theme without ejecting from Create React App.

If you want to learn more about Ant Design. There are some useful documents or tutorials that can help you get started with Ant Design.

- [Ant Design official documentation](https://ant.design/docs/react/introduce): Actually, official documentation is always an excellent starting point for you to get started with an unfamiliar tool. It provides a comprehensive guide on installation, components, and customization. If you meet a trouble in using a component, read this guide!

- [ANT DESIGN - THE BEST REACT LIBRARY??](https://www.youtube.com/watch?v=IEqmSROj5Uc): This tutorial video can show you every basic thing about Ant Design in 5 minutes. After watching this video, you can have an overview about Ant Design. 

- [Reactjs with AntDesign](https://www.youtube.com/playlist?list=PL-JTnqZPF5z2qTGwNkYln3m0pA0qfgHFR): This playlist contains almost every useful components that you might want to use in your project. It is good for beginners to learn the usage of components and apply them step by step. 

By following these tutorials, I hope you can gain a solid understanding of how to use Ant Design in your React projects and create attractive, user-friendly interfaces.


### User Experience Orientated Games

User experience is unique, as practicing user experience design can be challenging. Since user experience has to do a lot with visuals, you can learn user design by playing games. User experience orientated games can be an engaging and fun way to get familiar with common UX practices. Here are unique games that can help develop better UX design skills.

- [Can't Unsee](https://cantunsee.space/): The game of choice! Can't Unsee is a game that presents the user with two designs and challenges the user to pick the most correct user experience design. Feedback on each selection allows the user to learn from their mistakes. Sharpen your knowledge of common user experience design practices while testing your attention to detail.


- [Designercize](https://designercize.com/): Leetcode for designers. This unique game gives the user a unique interview-style design challenge to prepare for future interviews. Each challenge comes with a set of constraints containing a time limit, providing a realistic scenario for practicing your design and problem-solving skills. From common user experience practices to visual design, this game is a great way to improve your on-the-fly design abilities and creativity. 

- [Laws of UX](https://lawsofux.com/): This is an interactive website with beautiful cards Informing users of the common laws of UX. Each card provides an example of how the principle can be applied in real-world design scenarios, making this a very valuable tool for learning and practicing user experience design.

- [It’s Centered That](https://www.supremo.co.uk/designers-eye/): Creating designs with alignment is an important concept for user experience. This game tests your designer’s eye by asking the user if the dot is centered or not on a shape. 

- [Boolean](https://boolean.method.ac/): Boolean is a fun and interactive game that challenges users to create an interface using essential user experience design elements. The game provides the user with different design challenges to help practice creating effective and visually appealing user interfaces. Each challenge tests the user's ability to apply specific design principles and create user-friendly interfaces.

- [Betterwebtype](https://betterwebtype.com/triangle/): This game was created by Better Web Type to help designers and developers use "The Equilateral Triangle of a Perfect Paragraph" user experience theory. This theory consists of three interconnected points, size, line height and length. It states that these are the three main factors that impact the legibility and readability of typography on the web. The game gives the user text and challenges the user to adjust the heights and widths of it in order to find the "perfect paragraph" size. This unique and interactive game is very informative and helps provide a simple and intuitive learning space for the most optimal typographic results for user experience. 

