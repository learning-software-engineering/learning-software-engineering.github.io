# Resources for User Experience

## Table of Contents

1. [Overview](https://learning-software-engineering.github.io/Topics/User_Experience.html#overview)
2. [Fundamentals of User Experience](https://learning-software-engineering.github.io/Topics/User_Experience.html#fundamentals-of-user-experience)
   - [User-Friendly Search Algorithms](https://learning-software-engineering.github.io/Topics/User_Experience.html#user-friendly-search-algorithms)
   - [User Research](https://learning-software-engineering.github.io/Topics/User_Experience.html#user-research)
   - [Visual Elements of User Interface Design](https://learning-software-engineering.github.io/Topics/User_Experience.html#visual-elements-of-user-interface-design)
   - [User Experience Principles](https://learning-software-engineering.github.io/Topics/User_Experience.html#user-experience-principles)
   - [Site mapping, Wireframing, and Prototyping](https://learning-software-engineering.github.io/Topics/User_Experience.html#site-mapping-wireframing-and-prototyping)
   - [Accessibility](https://learning-software-engineering.github.io/Topics/User_Experience.html#accessibility)
3. [Helpful Courses](https://learning-software-engineering.github.io/Topics/User_Experience.html#helpful-courses)
4. [Tools Used in User Experience Design](https://learning-software-engineering.github.io/Topics/User_Experience.html#tools-used-in-user-experience-design)
   - [Design Tools](https://learning-software-engineering.github.io/Topics/User_Experience.html#design-tools)
   - [UI Component Libraries](https://learning-software-engineering.github.io/Topics/User_Experience.html#ui-component-libraries)
5. [User Experience-Oriented Games](https://learning-software-engineering.github.io/Topics/User_Experience.html#user-experience-oriented-games)

# Overview

User experience (UX) is a large and broad topic. It covers the overall experience of the user and how they interact with software systems and applications. The main focus of User Experience is to make a piece of software accessible, easy to follow (i.e., user-friendly) and adaptable to the user's needs. There is no set of standard rules that make up a "great" user experience, as it often depends on the product and the consumers who are using the products.

User experience is not to be confused with UI (User Interface) and UX _design_. While these topics have similarities with user experience, they are also different in their own ways:

- **UI design** is the process of creating an interface with a focus on how the interface will _look_ like -- think of aesthetics!
- **UX design** is the process of creating an interface with a focus on a smooth, meaningful user _experience_ -- think of usability and usefulness!
- **User experience** is a user's journey when interacting with your software/application.

There are many resources that differentiate between user experience, UI design, and UX design. Here are a few related websites:

- [The Definition of User Experience](https://www.nngroup.com/articles/definition-user-experience/)
- [Differences Between UX and UI Design](<https://bootcamp.cvn.columbia.edu/blog/what-is-ux-design/#:~:text=User%20experience%20(UX)%20refers%20to,usability%2C%20function%2C%20and%20design.>)

# Fundamentals of User Experience

As mentioned earlier, user experience is not easy to define as it is a large and broad topic. Here are a _few_ areas of UX that software engineers should pay attention to:

## User-Friendly Search Algorithms

- [Fuzzy Search](./User_Experience/Fuzzy.md)

## User Research

When it comes to user experience, conducting user research is very important as it lets us discover new problems and address deeper issues. As a software engineer, it may be extensive for you to conduct user research, but there are tools that you can use to understand your users better, such as the following:

### Point-of-View Statements

POV statements let you describe your user and their needs, and they can help you discover new problems/questions that you need to solve before creating your application.

The structure of a POV statement is:

> [WHO] needs to [VERB] because [WHY].

"Who" will refer to your users. For example, let's say we're making a grocery shopping app. A possible POV statement could be:

> A senior citizen who lives alone needs help with buying groceries because they have difficulty getting out of the house and reading small text.

Now that we've realized a possible pain point for a senior citizen, we can look into implementing our grocery shopping app such that it's accessible to this target audience.

### User Personas

User personas should be built from user research data, not stereotypes. In CSC301, your partner may guide you in creating personas, but in the worst case, you'll find yourself creating personas from no data since you don't have time to conduct research. Nonetheless, there are many benefits to creating personas, including, but not limited to:

- Provides you with a better understanding of your target user groups
- Helps prioritize design choices

User personas can be written down in a document, or created with design software such as [Xtensio](https://xtensio.com/) and [Figma](https://www.figma.com/). You can find user persona templates created by other people on Xtensio, Figma, and other design software.

If you use a template, it'll prompt you to fill in specific information about your target user. If you're writing your personas from scratch or want to consider extra information, here are some elements that a good user persona may include:

- Name, picture, target user group
- Biography
- Quote that sums up the persona
- Demographic characteristics
- Personality, habits, behaviour
- Goals, tasks, needs, motivations
- Challenges, pain points

A quick Google image search for "User Persona" will help tie all this information together.

### Design Requirements

#### [Design Requirements](./User_Experience/Design_Requirements.md)

## Visual Elements of User Interface Design

### Design Principles

UI designers achieve a visual hierarchy (i.e., the order a user processes the application's information) in their interfaces by using contrast. To create contrast, consider playing around with the following elements:

**_Scale_**

> <h1>Larger text attracts the eye,</h1> <h6>whereas smaller text is easier to ignore.</h6>

**_Weight_**

> **Bold text attracts the eye** much more than regular text.

**_Direction_**

You want to direct your users to a call to action. For example:

> <h1>Welcome!</h1> 
> <p>Please click the button.</p>
> <kbd> <br> Button <br> </kbd>
> Your eyes easily flow from the title to the smaller message. Then, you're inclined to click the button. Now, look at this:
> <kbd> <br> Button <br> </kbd>
> <h1>Welcome!</h1> 
> Please click the button. 
> At first, you feel confused as to why there's a button at the top. Then you read the message, and now your eyes have to flick back to the top to find the button. It's a minor detail, but it still negatively affects the flow of the application.

**_Form/shape_**

You can combine shapes with lines to make elements like buttons.

**_Texture_**

You can use texture to draw a user's eye to elements like titles, icons, and buttons. Keep in mind that texture and patterns are different -- patterns are small repetitive elements (like polka dots, while texture is not necessarily repetitive. Read more about texture [here](https://uxdesign.cc/web-design-theory-texture-1e07c29b10e5), and see examples of websites that use texture [here](https://www.webfx.com/blog/web-design/textured-website-designs-inspiration/).

**_Space_**

Make use of whitespace so users have an easier time reading your application's text.

**_Value/shade_**

Value can attract the eye. For example, you can use shading to create button shadows.

**_Colour_**

```diff
- Red text seems urgent,
+ whereas green usually indicates success.
! Orange feels like a warning of some sort.
```

### Design Layout and Cognitive Load

The design of a web application or mobile app may have some consquences in the cognitive load for a user. COnfusing layouts may feel like a huge cogntive task when navigating a button as simple as the menu or trying to find the exact information they need. You can read more on this topic [here](./User_Experience/Page_Layout_and_Cognitive_Load.md)

### Color Theory

- [Colors Influence Choice](https://usabilitygeek.com/colour-user-experience-psychology/#:~:text=Colour%20plays%20a%20crucial%20role,and%20identified%20with%20your%20industry.): Users are shown certain colours to enforce actions. For example, red is commonly linked to aggressive or bad emotions and as such can be used as a cancel to dissuade people from refunding items.
- Read an in depth analysis on color theory [here](./User_Experience/Color_Theory.md)

### Button Design

Your buttons need to look clickable. Otherwise, your user may not understand that your button is interactive. Your buttons can have certain states:

- Normal: communicates that the button is interactive
- Focused: the button is highlighted in some way
- Hovered: lets the user know that their cursor is on top of the button
- Active: the button has been clicked on
- Progress/loading: lets the user know that something is happening because they clicked the button
- Disabled: lets the user know that this button can't be clicked
  Learn more about button design [here](https://uxdesign.cc/button-design-user-interface-components-series-85243b6736c7).

You may find this article on [Amazon's One-Click Button](https://medium.com/@cccalibour/how-ux-design-makes-a-difference-amazons-continue-button-901618a8b00e) interesting. It discusses how the design of buttons can drastically improve user experience... and increase your revenue! :)

### Navigation Systems

Your users should feel comfortable with navigating through your application. Here are some elements to consider...

- Wayfinding: this includes breadcrumbs, convenient links to take you back to the home page, and "you are here" indicators.
- Call-to-action button
- Primary navigation (e.g., the main navbar)
- Secondary navigation (e.g., a smaller navbar that pops up underneath the main one)
- Utility navigation: important parts of the application that aren't part of the main content (e.g., help sections, social media links)
- Vertical navigation
- Search bars
- Shortcuts to related content

### Typography

Make sure the text on your application is **legible**! Body text should be at least 16px; on bigger screens, body text should be at least 20-24px. Your line height should also be around 1.5 times the font size for an easier reading experience. You may also want to consider using 40-70 characters per line so that your user's eyes aren't flicking back and forth all the time.

Make sure to use a universal, legible font style, and don't use extremely contrasting colours. For example, pure black text against a pure white background is too stark for the eyes and will eventually cause eye strain. Consider dimming it down.

### Established Norms

- [Scrolls On Socials](https://forgeandsmith.com/blog/scrolling-vs-clicking-whats-the-preferred-user-experience/): Users are conditioned for scrolling, and now every new social media app conforms to scrolling.

### Responsive Design

- [Responsive Design](https://devrix.com/tutorial/important-responsive-design/): Responsive Design generally refers to a design where the software is adaptable to the consumer's device. The responsive design can be many things including screen sizes, collapsing of navbars, adjusting texts based on the screens, scrolling effects and more. The benefits of a responsive design make your software accessible across varying devices and overall improves the user experience. The article demonstrates the importance and benefits of responsive design, the flexibility they provide, and the easiblity for the consumers upon making the said software.

### Optimizing UI with A/B Testing

- [A/B Testing](./User_Experience/AB_Testing.md): A/B testing is a randomized experiment used to compare two versions of a webpage to determine which is more effective.

## User Experience Principles

### Nielsen's 10 Usability Heuristics

Jakob Nielsen's [10 Heuristics for Interaction Design](./User_Experience/Usability_Heuristics.md) are principles/rules of thumb to follow if you want to create a clear, intuitive user experience for your application. The principles describe scenarios and elements that your application may want to account for.

## Site mapping, Wireframing, and Prototyping

**Site mapping** is essentially creating a bare-bones diagram of the flow of your application. Your diagram should communicate how your pages connect. It should answer the question, "Which page(s) comes after this current page?"

**Wireframing** comes before the **mock-up** process, though as a software engineer, you probably won't be making any wireframes. A **mock-up** of your application is essentially a static design of your application's pages. A benefit of creating a mock-up is that you can communicate your design ideas to your teammates and get feedback from your customer/partner if you have one. Mock-ups are also known as **low-fidelity prototypes**

### Accessibility Features of User Experience

**Wireframes** are the "skeleton" of your mock-up; they communicate the general layout of your application and don't include details like specific text or colour. This is why you create wireframes before your mock-up.

Finally, to create a **prototype**, or a **high-fidelity prototype**, you essentially make your mock-up interactive by connecting all the pages. Figma (discussed in the [Design Tools](https://learning-software-engineering.github.io/Topics/User_Experience.html#figma) section) is a free tool that you can use to create your mock-up and prototype. With prototyping tools like Figma, you can easily stimulate button clicks, screen swipes, etc. without any code.

## Accessibility

### What is accessibility in software?

Accessibility is an important, and often overlooked aspect of building applications. Although accessibility may be out of scope for projects built in this course, it is an important skill and consideration to learn as you go forward in your professional software development career.

Users may have a wide variety of accessibility needs. This may include users with vision, hearing, and mobility impairments, cognitive disabilities, and more. Examples of accessibility in software include:

- Screen readers for vision impairment
- Closed captions for hearing impairments
- Font size adjustability for older users
- Black and white filters for photosensitivity and colour blindness

### Why should I make my app accessible?

In Ontario, it is a [legal requirement](https://www.ontario.ca/page/how-make-websites-accessible) for websites and web apps to reach a certain level of accessibility. Aside from legal requirements, it is generally beneficial to build accessibility into your apps. As a business, supporting a diverse set of users will improve the experience of your customers, and as an individual your contributions will impact the friendliness and inclusion of the internet.

### Design Principles

The core of accessibility lies in acknowledging and catering to the diverse needs of users, which include visual, auditory, motor, and cognitive impairments. By implementing accessibility standards, developers can create products that are not only more usable for people with disabilities but also enhance the overall user experience for a broader audience. This involves designing software and interfaces that are flexible enough to meet different user needs and preferences, and are compatible with various assistive technologies.

[Universal Design Principles](https://www.buffalo.edu/access/help-and-support/topic3/universaldesignprinciples.html) are not only used for software but can be incorporated generally as well. These 7 principles ensure accessibility, consistency, and user-friendly software.
This article provides the 7 Universal Design Principles that make software accessible to all users, which plays an important role in diversifying the User Experience.

While it may feel overwhelming to come up with your own great design from scratch by following all these rules and principles, you may find it easier to learn from examples to avoid mistakes that others have made. [This article](https://www.interaction-design.org/literature/article/bad-design-vs-good-design-5-examples-we-can-learn-frombad-design-vs-good-design-5-examples-we-can-learn-from-130706) outlines 5 examples of bad design, with great explanations, takeaways, and lessons to learn.

### Web Content Accessibility Guidelines (WCAG)

The [Web Content Accessibility Guidelines (WCAG)](https://www.w3.org/WAI/standards-guidelines/wcag/) are a set of recommendations for making web content more accessible, primarily for people with disabilities, but also for all user interfaces and devices. Developed through the World Wide Web Consortium (W3C), specifically by the Web Accessibility Initiative (WAI), WCAG serves as the international standard for web accessibility. This guide is quite detailed so it may be difficult to know where to start as you are developing your web app, but a11y (a community-driven accessibilty initiative) has boiled down the most popular and important standards into an easy to follow [checklist](https://www.a11yproject.com/checklist/).

WCAG 2 is structured around four fundamental principles, often referred to by the acronym **POUR**, ensuring that web content is:

1. **Perceivable**: Information and user interface components must be presented in ways that users can perceive.

   - Provide text alternatives for non-text content.
   - Provide captions and other alternatives for multimedia.
   - Create content that can be presented in different ways, including by assistive technologies, without losing meaning.
   - Make it easier for users to see and hear content.

2. **Operable**: User interface components and navigation must be operable.

   - Make all functionality available from a keyboard.
   - Give users enough time to read and use content.
   - Do not use content that causes seizures or physical reactions.
   - Help users navigate and find content.
   - Make it easier to use inputs other than keyboard.

3. **Understandable**: Information and the operation of user interfaces must be understandable.

   - Make text readable and understandable.
   - Make content appear and operate in predictable ways.
   - Help users avoid and correct mistakes.

4. **Robust**: Content must be robust enough to be reliably interpreted by a wide variety of user agents, including assistive technologies.
   - Maximize compatibility with current and future user tools.

WCAG 2.0 is further divided into three levels of conformance:

- **Level A**: The most basic web accessibility features.
- **Level AA**: The most common barriers for disabled users
- **Level AAA**: The highest and most advanced level of accessibility.

Here are some questions that you can ask yourself when trying to make you work more accessible:
**Example 1 (Perceivable)**: Ensure that all images on your website have descriptive alt text. For videos, provide captions and audio descriptions.

> 1. Have all non-text content (like images, videos, audio) been given text alternatives?
> 2. Are there captions for all video content and transcripts for audio content?
> 3. Can all information conveyed with color be understood without color?

**Example 2 (Operable)**: Make sure that all functionalities of your website are accessible via keyboard, including navigation, forms, and custom controls.

> 1. Can all website functionalities be operated through a keyboard alone?
> 2. Are there mechanisms to help users navigate, find content, and determine where they are?
> 3. Have you ensured that no content flashes more than three times in any one second period?

**Example 3 (Understandable)**: Write content in clear, simple language and provide instructions or labels for complex forms or content.

> 1. Is the text content readable and understandable for the widest possible audience?
> 2. Does the website operate in predictable ways, such as consistent navigation and naming?
> 3. Are error messages clear and helpful, guiding users towards solving the problem?

**Example 4 (Robust)**: Use standard HTML tags and validate your HTML to ensure compatibility with current and future user agents, including assistive technologies.

> 1. Is the content compatible with current and future user agents, including assistive technologies?
> 2. Have you used clean, standards-compliant HTML/CSS?
> 3. Are there any custom components that might need ARIA roles to ensure they are accessible?

#### Tools:

[WebAIM Contrast Checker](https://webaim.org/resources/contrastchecker/): The Contrast Checker provides a straightforward interface where users can input the hexadecimal codes of the text and background colors they are using on their website. Upon entering these values, the tool automatically calculates the contrast ratio between the text and background. This ratio is crucial for readability, especially under the WCAG, which sets minimum contrast standards for visual presentation of text.

[Stark](https://www.getstark.co/): Stark is a plugin for design tools like Adobe XD, Sketch, and Figma, focusing on accessibility. It features color contrast checkers and color blindness simulations to ensure designs meet accessibility standards, particularly WCAG. Integrated directly into design platforms, Stark is essential for creating inclusive digital products.

[Google’s developer tools](https://developer.chrome.com/docs/lighthouse/accessibility/): Lighthouse is Google's accessibility auditing tool. It scores your webpage's accessbility and provides feedback on areas of improvement.

[Siteimprove](https://www.siteimprove.com/): Siteimprove is a product that aims to help businesses improve their website through improvement of inclusion, user experience, and SEO.

#### More readings:

- [Designing accessible products](https://uxdesign.cc/designing-accessible-products-e8aa79b55ebc) by Adhithya Ramakumar

- [Accessible Interface Design](https://babich.biz/blog/accessible-interface-design/) by Nick Babich

- [Designing For Accessibility And Inclusion](https://www.smashingmagazine.com/2018/04/designing-accessibility-inclusion/) by Steven Lambert

- [What is Accessibility?](https://www.interaction-design.org/literature/topics/accessibility) by Interaction Design Foundation

# Helpful Courses

- [The Design of Interactive Computational Media (CSC318) offered by U of T](https://artsci.calendar.utoronto.ca/course/csc318h1). CSC318 expands on the work done before coding projects. For example, the course will have you test how users would interact with your prototype of a UI and then modify it so that the UX is better for the user.
- [CalArt's UI/UX Design Specialization on Coursera](https://www.coursera.org/specializations/ui-ux-design). This is a package of 4 courses that teaches beginners the elements of UI design, fundamentals of UX design, and web design. This specialization will help you gain experience in wireframing, prototyping, and _designing_ (not coding) your own website/app. Plus, as a U of T student, you can get this specialization certificate for free once you finish the 4 courses!

# Tools Used in User Experience Design

## Design Tools

### Figma

Figma is a free (for the most part) collaborative tool that lets you design and build mock-ups and prototypes of your software/applications. You may not need to build prototypes as a software developer/engineer, but you'll probably find yourself viewing Figma design files to build your frontend. So, now's a great time to start learning how to use [Figma](https://www,figma.com)!

#### Figma Community

The [Figma Community](https://www.figma.com/community) is a platform where individuals, teams, and organizations can share files, plugins, and widgets, allowing you to explore valuable resources and collaborate with fellow creators.

Published resources are accessible to through either free or paid access.

For a more in depth guide to the Figma Community, click [here](https://help.figma.com/hc/en-us/articles/360038510693-Guide-to-the-Figma-Community)

#### UI Kits

UI kits from the Figma community are used for a variety of purposes related to user interface (UI) design and development. These kits typically include pre-designed components, templates, and styles that designers can use to create visually appealing and functional interfaces for websites, mobile apps, or other digital products. Here are some common uses and benefits of UI kits from the Figma community:

- Rapid Prototyping: UI kits allow designers to quickly create prototypes of their designs without starting from scratch. They can drag and drop pre-made components such as buttons, navigation bars, icons, and forms, speeding up the prototyping process.

- Consistency: By using UI kits, designers can ensure consistency in design elements across different screens or pages of a digital product. This helps in maintaining a cohesive user experience and brand identity.

- Time-saving: Instead of designing every element from scratch, designers can leverage UI kits to save time and effort, especially for common UI components that are used across multiple projects.

- Inspiration: UI kits often include modern design trends, styles, and best practices, which can serve as inspiration for designers when creating their own custom designs.

- Collaboration: Figma's collaborative features allow designers to work together on projects using UI kits. Team members can access and use the same components and styles, promoting collaboration, consistency, and efficiency in the design process.

- Accessibility: Some UI kits are designed with accessibility in mind, including color contrast ratios, accessible typography, and other elements that comply with web accessibility standards. This ensures that the final product is usable by a wide range of users, including those with disabilities.

For a step-by-step tutorial with visuals on how to use community built UI kits in your own projects, click [here](Topics/User_Experience/UI_Kit_Tutorial.md)

#### Developer Mode

With just a click of a button, you can switch to "developer mode" in Figma, which helps you translate design into code! Essentially, you can click on components like a button and get its corresponding code and styling. Read about how to use this feature [here](https://www.figma.com/dev-mode/).

#### Figma, MUI, and React

See the [UI Component Libraries](https://learning-software-engineering.github.io/Topics/User_Experience.html#ui-component-libraries) section for details on MUI. Note that MUI is a component library for React _only_. You can download the** MUI extension on Figma** and immediately use MUI components in your Figma design. Then, when you're ready to code, you can install MUI in your React project and easily create your frontend by entering "developer mode" on your Figma design and copying the code that Figma generated for you.

#### Optimizing Figma Design tools to easily convert into code

As mentioned above, “[developer mode](https://www.figma.com/dev-mode/)” is an essential base to translating your Figma designs into usable code. Additionally, there are many design tools within Figma that you can take advantage of to set yourself up for easy code conversion:

**Text Styles and Color Styles**

Figma allows for users to define their own list of text styles (see [the official Figma article](https://help.figma.com/hc/en-us/articles/360039957034-Create-and-apply-text-styles)). Take advantage of this feature and ensure that your list of Figma text styles corresponds to your code base’s text css definitions. By doing this, you can ensure that your font texts are always properly styled without having to manually adjust them. Consider defining and using the following Figma text styles: `H1`, `H2`, `H3`, `H4`, `Button Text`, `Subheading`, `Body`.

Similarly, Figma allows for users to define their own list of color styles (see [the official Figma article](https://help.figma.com/hc/en-us/articles/360039820134-Manage-and-share-styles)). Figma color styles is a very powerful tool and allows you to group various colors to organize into different modes and themes. In your actual frontend code, it’s likely that you will want a css file that defines your main color scheme and possible variations (ie. dark mode, secondary colors, etc.). Ensure that your Figma list of color styles corresponds to your code’s css definitions. Consider defining and using the following Figma color styles: `primary`, `secondary`, `primary text`, `secondary text`, `background`.

**Additional Styles**

On a related note, Figma allows for the options of Effect styling and Grid styling (see [the official Figma article](https://help.figma.com/hc/en-us/articles/360038746534-Create-color-text-effect-and-layout-grid-styles)). Both types of additional styling are valid attributes in css coding. Effect styling lets you define `drop shadow`, `inner shadow`, `layer blur`, and `background blur`. Grid styling lets you organize your frames in `row`, `column`, and `grid` formations. Consider using any of these additional styles and replicating them in your code with the same attribute keywords.

**Components**

Within Figma, you can define individual components, as explained in detail in [this official Figma article](https://help.figma.com/hc/en-us/articles/360038662654-Guide-to-components-in-Figma). In essence, Figma components work similarly to React components; components are reusable and modifying the characteristics of a component will modify every instance of the same component. Using these in your design can be especially helpful to create a good understanding for which components can/should be reusable in your actual codebase.

Tip: if you are designing for iOS/iPadOS, there is a very helpful Figma library with components styled with Apple's UI standards [here](https://www.figma.com/community/file/1248375255495415511).

**Plugin Extensions**

External plugin extensions are available in Figma to make your life easier and should definitely be taken advantage of. Plugin extensions are created by other community members and will usually have predefined components and icons that are relevant to certain libraries and frameworks that you are using in your own codebase.

For example, those that are using the [ShadCN](https://ui.shadcn.com/) component library with their React project can benefit from an existing [ShadCN Figma plugin](https://www.figma.com/community/plugin/1280731237276040017/design-with-shadcn-ui-plugin). This plugin has already predefined all ShadCN components and icons for users to integrate into their Figma canvas. Using these plugins will not only help save time but also ensure that your Figma design and your code looks exactly the same.

You can find a database of available plugins at [this Figma resource](https://www.figma.com/community/plugins).

**Exporting assets**

Within Figma, you are able to directly export assets (ie. images) in the exact dimensions that you define them as in your Figma canvas (see [the official Figma article](https://help.figma.com/hc/en-us/articles/360040028114-Export-from-Figma)). This can be especially useful to ensure your assets appear with the proper aspect ratio in your actual app. In particular, Figma allows you to export files in `jpg`, `png`, `svg`, and `pdf` format.

### Adobe XD

[Adobe XD](https://www.adobe.com/products/xd/learn/get-started/what-is-adobe-xd-used-for.html) is another popular prototyping tool. Unfortunately, the current author of this wiki doesn't know much about it, other than it requires a monthly subscription :(.

## UI Component Libraries

When building an application with a frontend framework (e.g., React, Vue, Angular, etc.), developers can import an UI design component library/libraries to help them easily build aesthetic, user-friendly interfaces.

### Material UI (MUI)

[MUI](https://mui.com/) is a popular library of UI design components made for React. These components are essentially pre-made "features" that you can immediately use, such as buttons, navbars, pop-ups, etc.

### Ant Design

View an introduction to Ant Design written by a CSC301 student [here](./User_Experience/Ant_Design.md)

# User Experience-Orientated Games

User experience is unique, as practicing user experience design can be challenging. Since user experience has to do a lot with visuals, you can learn user design by playing games. User experience orientated games can be an engaging and fun way to get familiar with common UX practices. Here are unique games that can help develop better UX design skills.

- [Can't Unsee](https://cantunsee.space/): The game of choice! Can't Unsee is a game that presents the user with two designs and challenges the user to pick the most correct user experience design. Feedback on each selection allows the user to learn from their mistakes. Sharpen your knowledge of common user experience design practices while testing your attention to detail.

- [Designercize](https://designercize.com/): Leetcode for designers. This unique game gives the user a unique interview-style design challenge to prepare for future interviews. Each challenge comes with a set of constraints containing a time limit, providing a realistic scenario for practicing your design and problem-solving skills. From common user experience practices to visual design, this game is a great way to improve your on-the-fly design abilities and creativity.

- [Laws of UX](https://lawsofux.com/): This is an interactive website with beautiful cards Informing users of the common laws of UX. Each card provides an example of how the principle can be applied in real-world design scenarios, making this a very valuable tool for learning and practicing user experience design.

- [It’s Centered That](https://www.supremo.co.uk/designers-eye/): Creating designs with alignment is an important concept for user experience. This game tests your designer’s eye by asking the user if the dot is centered or not on a shape.

- [Boolean](https://boolean.method.ac/): Boolean is a fun and interactive game that challenges users to create an interface using essential user experience design elements. The game provides the user with different design challenges to help practice creating effective and visually appealing user interfaces. Each challenge tests the user's ability to apply specific design principles and create user-friendly interfaces.

- [Betterwebtype](https://betterwebtype.com/triangle/): This game was created by Better Web Type to help designers and developers use "The Equilateral Triangle of a Perfect Paragraph" user experience theory. This theory consists of three interconnected points, size, line height and length. It states that these are the three main factors that impact the legibility and readability of typography on the web. The game gives the user text and challenges the user to adjust the heights and widths of it in order to find the "perfect paragraph" size. This unique and interactive game is very informative and helps provide a simple and intuitive learning space for the most optimal typographic results for user experience.
