# Mobile-First Design for Responsive Web Apps

## What is it?

Mobile-first design is an approach that prioritizes designing the UI of web apps for mobile devices first before other larger screens. 

The reasoning behind this strategy is to promote _progressive enhancement_ — the UI’s mobile version will contain only the main functionalities required for the web app, and adding extra features that can be displayed on larger screens can come later. In contrast, using the method of desktop-first design and adding responsiveness after is called _graceful degradation _because a lot of the details and complexities incorporated in the desktop version of the UI will have to be simplified and condensed to fit on a much smaller screen.

## Benefits



* Enhanced UX for mobile users
    * As accessing web apps through phones has become the dominant mode of interaction — with more than [50%](https://www.statista.com/statistics/277125/share-of-website-traffic-coming-from-mobile-devices/#:~:text=Mobile%20accounts%20for%20approximately%20half,since%20the%20beginning%20of%202017.) of web traffic coming from mobile devices since 2022 — creating UIs with the mobile-first design approach ensures that the UX for mobile devices is not compromised from graceful degradation
* Prioritized content
    * With a smaller screen, the UI for mobile devices will likely have to cut out any unnecessary details or rearrange content, allowing your designs to be cleaner and more concise
    * For instance, having a large block of text that spans your entire phone screen might lead you to shorten the text or break it up for an improved UX; the lengthiness of that body of text might have been overlooked initially if using the desktop-first approach
* Improved accessibility
    * Mobile-first design emphasizes legible typography and text sizes, ensuring readability and navigability for your web app
* Reduced redesigning
    * Adopting this approach can reduce the need for extensive redesign efforts later in the process if some critical features on the desktop version, such as hover effects, cannot be easily translated into the mobile version
* Faster page loading times
    * With a reduced amount of code, images, and resources required for the web app, losing speed can also be reduced

## Drawbacks

* Learning curve
    * Most web app developers are accustomed to the desktop-first approach, thus shifting to this new strategy that requires a different way of thinking and planning requires some effort
* Restricted design creativity and flexibility
    * Mobile designs are more limited than desktop versions, which may put more restrictions on the content and features you can include
    * These constraints stem from the limited screen size and reliance on touch interactions, as designing the mobile version requires meticulous consideration to arrange the content in a touch-friendly and legible manner; this involves ensuring the buttons are sized appropriately for touch, accommodating all text within the narrow screen, and also minimizing the need for excessive scrolling

## General Steps

1. Content inventory
    * Plan out all the content and elements you need for your web pages
2. Visual hierarchy
    * Create a priority list of all the visuals you will include on the page, taking into consideration the size of images, colours, and typography, as these properties can guide the user’s eye to understand the relative significance of the elements
3. Design from smallest to largest screens
    * Create designs for the mobile version first, then tablet, then finally desktop
    * These designs can be made on Figma, Canva, Google Drawings/Slides, or whatever design tool that will help you plan out the exact format of your page
4. Start coding!
    * Use CSS media queries to adjust the size or style of elements depending on the screen size
    * Test your UI on Google Chrome using the dev tool (right click on the screen, select Inspect, at the top select your desired dimensions to see how your web app looks on different kinds of devices and screen sizes)

## Helpful Links for Further Guidance

* More tips for mobile-first design: [https://www.browserstack.com/guide/how-to-implement-mobile-first-design](https://www.browserstack.com/guide/how-to-implement-mobile-first-design)
* CSS media queries for mobile-first design: [https://developer.mozilla.org/en-US/docs/Learn/CSS/CSS_layout/Media_queries#active_learning_mobile_first_responsive_design](https://developer.mozilla.org/en-US/docs/Learn/CSS/CSS_layout/Media_queries#active_learning_mobile_first_responsive_design)
* Video tutorial for creating a web app using mobile-first design: [https://www.youtube.com/watch?v=NeThtWARdnY](https://www.youtube.com/watch?v=NeThtWARdnY)

## Key Takeaway

Given the recent prevalence of accessing web apps through mobile devices, the mobile-first design approach is recommended for enhanced UX, user accessibility, and adaptable design. This method is certainly not a one-size-fits-all solution, especially since the dominant type of device used to access the web app is dependent on the application itself. However, in the case of mobile-centric websites, this mobile-first approach fundamentally translates to a user-first approach, prioritizing the interface and convenience for the user, which is at the core of UX design.
