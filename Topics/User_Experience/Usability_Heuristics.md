# **Nielsen's 10 Usability Heuristics**

## **Introduction and Background**

Conceptualized and developed by Danish human-computer interaction research Jakob Nielsen in the early 1990s (1), Nielsen's ten heuristics are general principles for designing user interfaces that have become one of the most commonly-used frameworks used in improving usability and the user experience within all manner of software products. 

Heuristic frameworks like Nielsen's are generally employed for evaluating the usability of a user interface and, broadly, for informing its design. While heuristics by their nature are not guaranteed to present an optimal solution in all circumstances, the offered shortcuts are helpful in providing guidelines that can be used in building the interfaces themselves, as well as for determining flaws that may impede an end user (2).

According to the Nielsen Norman group, Nielsen's UX consulting group, usability is defined as a "quality attribute that assesses how easy user interfaces are to use". Usability, as defined by Nielsen, is evaluated on five components (3):

Learnability: How easy is it for users to accomplish basic tasks the first time they encounter the design?
Efficiency: Once users have learned the design, how quickly can they perform tasks?
Memorability: When users return to the design after a period of not using it, how easily can they reestablish proficiency?
Errors: How many errors do users make, how severe are these errors, and how easily can they recover from the errors?
Satisfaction: How pleasant is it to use the design?

Thus, Nielsen's usability heuristics have the stated purpose of helping to maintain usability through supporting these five components. Adhering to these heuristic guidelines allow software engineers to create applications that are accessible, usable, and useful for a broad range of purposes. 

## **The Heuristics**

For more information, consider Nielsen's webpage: https://www.nngroup.com/articles/ten-usability-heuristics/ (4)

### **1: Visbility of system status**
The system should always keep users informed about what is going on within the system, through appropriate feedback that is provided within a reasonable time. Communication between the user and the system allows the user to be aware of what is happening, and make decisions based on this knowledge. 

__Why is this important?__

Information is power. Every time we make a decision in real life, whether it is to switch lanes on the highway or purchase an appliance, we must do so based on the information we have of the current state (in our first example this might be our car's position on the highway, the position of other vehicles, or when the exit we want to take is coming up). It is no different when a user must interact with a software system. "Only by knowing what the current system status is can you change it — that is, you can (...) figure out what you need to do next in order to reach your goal (5)". To make sure the user is able to achieve their goals and doesn't become frustrated, they must understand how the system responds to their action and be able to figure out the next steps to take based on the current status. When they feel in control— that is, their actions clearly affect the system in predictable and consistent ways— they are able to build trust with the software product.

__How can we implement this?__

- Explicitly convey the system status. An application may provide a loading screen or a progress bar while the user waits for an action to complete.
- Responsive design choices that indicate whether an action was successful or not; for example, an online marketplace should inform the user when an order goes through or fails to go through.
- If the user makes a mistake, the system should inform them and invite them to fix that mistake. 

Opaque systems frustrate users and lower usability. Aim for transparency.


### **2: Match between system and the real world**
The system should use words, phrases, and concepts that are familiar to the user. Avoid using technical or system-oriented terms, and use real-world conventions that provide information in a natural and logical order that will make sense to the users of the system. If your application relates to things in the real world, ensure that the system accurately matches them.

__Why is this important?__
Engineers often communicate in technical terms that are familiar to them, but the end user for most non-specialist products is not likely to be well-versed with the same concepts and words. The user experience designer should avoid assuming that their interpretation of terminology, UI elements, etc. match with the interpretation of future users; to improve usability and user satisfaction, users should be able to intuitively understand the interface and its elements (6). Elaborate terminology and contrived interfaces are liable to confuse the users, while familiar terminology and commonly recognizable UI elements support this intuition.

__How can we implement this?__
- Use clear, simple terminology. When dealing with complex text like the terms of service for an application, a summary in plain language will improve accessibility.
- For interface elements, we may use visual design to reflect a familiar object used to perform that task in real life. For a date-setting functionality, a small symbol of a calendar is suitable. Certain design elements are commonly understood (a symbol of a gear may often represent settings for an application).


**Example:** An e-reading application that allows users to "highlight" words and phrases using a bright colour might use a symbol of a marker to toggle the setting.

### **3: User control and freedom**
Allow users to have an "emergency exit" for when they select certain system functions by mistake and want to return to their original state. Support options for undo and redo so users have more freedom over how they interact with the system. Users will change their minds or make mistakes, and will need a way to go back to the previous state.

__Why is this important?__
A sense of control and predictability is important for usability and for the end users, allowing them to build trust with the product and use it effectively (3). When a system does not tolerate mistakes, user errors cause major disruptions to the user's workflow and result in them losing control. Letting users undo potential mistakes easily will improve usability.

For the end user, the ability to reverse errors encourages users to explore, which "facilitates learning and discovery of features". It also increases overall use and sales (in the case of exploring a product space). When the user experience doesn't allow for mistakes to be easily undone, users feel a loss of control and may become frustrated (7).

__How can we implement this?__

- From the Nielsen webpage (7), there are four primary standard features.

A Back link which returns users to a previous page or screen
A Cancel link which allows the user to quit a task or multi-step process
A Close link which allows users to close a new view
An Undo option (and a corresponding redo option) to allow users to backtrack on a change to a UI element

These features should attempt to provide the 'exit' while maintaining a reflection of user expectations. For instance, a form with multiple pages may have a 'back' link. This link should perform the action that would best fit the user's needs; in this case, this would be going back a single page in the form instead of exiting the form in its entirety. The website may also cache previously entered information so that accidentally clicking a redirect does not erase previously entered information.

**Example:** An application where a user is required to submit a form as part of their registration. If they change their mind or made a mistake, the app should support the ability to undo the submission and/or modify previous submissions.

### **4: Consistency and standards**
Users should not have to wonder whether different words, situations, or actions mean the same thing. Follow platform and industry conventions. (4)

__Why is this important?__

As we've discussed earlier, a sense of control and predictability is important for usability and for the end users' satisfaction. 

An inconsistent scheme results in a confusing user experience, makes it difficult to learn, and decreases usability. For example, a faulty website may use strange, esoteric symbols as part of the navigation menu. This may be functional, but will confuse users. Using commonly recognized symbols will avoid this particular issue, improving consistency with external standards. Another faulty website may use commonly recognized UI elements but position them inconsistently between pages or change their functionality depending on context. This will also confuse users.

Consistent design choices in the context of your product improves internal consistency and thus improves predictability, learnability, and control for users familiarizing themselves with your product. Adopting popular conventions for user interfaces improves external consistency and thus improves predictability and learnability for new users (8). 

__How can we implement this?__

Internal Consistency: Once we have designed UX elements, we should be consistent in how they are presented to the user (the layout) and how they function (functional consistency). A 'back button' should be in the same place across all pages, and should ideally perform the same functionality (of going back an iteration whenever it is introduced). 

External Consistency: We may research commonly-used UX standards and apply them to our own product in order to improve external consistency. For instance, the generic concept for a component that allows users to scroll through a set of images has a schema (image, buttons, light box) that is implemented to varying degrees of fidelity by different engineers. This schema is likely to be familiar to the end user, so basing our design off it will improve predictability.


**Example:** An application consistently uses an "X" symbol to represent an exit, instead of using a undo button or a back button in some areas.  

### **5: Error prevention**
Design the system to avoid problems from occurring in the first place by eliminating error-prone conditions or offering a solution if an error does occur. If the user makes a mistake, give them the opportunity to confirm if they would like to continue before committing to the action.

__Why is this important?__
"Users are often distracted from the task at hand, so prevent unconscious errors by offering suggestions, utilizing constraints, and being flexible." (9)

According to the article "Preventing User Errors: Avoiding Unconscious Slips" (9), there are two types of user error.

Slips occur when users intend to perform one action but accidentally perform another action. Examples may include making a spelling mistake when writing an essay or putting bleach into the washing machine while washing dyed clothing. These errors often occur as a result of inattention.


Mistakes occur when "users have goals that are inappropriate for the current problem or task; even if they take the right steps to complete their goals, the steps will result in an error." For instance, a person attempting to debug a software program may follow all testing and problem-solving steps within the context of the code but be unable to find the error, if the problem is actually caused by an incorrectly installed external dependency.

"Mistakes are conscious errors, and often (though not exclusively) arise when a user has incomplete or incorrect information about the task, and develops a mental model that doesn’t match how the interface actually works." (9)

__How can we implement this?__
Reducing Slips:

As stated in the article, slip-type mistakes often happen when the user knows how to achieve their goal but make mistakes when trying to achieve it. While the user is in control, a successful software application may reduce slips by providing guidance and correction when slips occur and allowing the user to rectify problems.

- User Constraints: Constraining the user in some circumstances can reduce the likelihood of error. For example, when the user is asked for their date of birth the system should reject the answer if that date is in the future; we may further implement input-validation features to ensure that nonsensical information (like incorrect postal codes) is not entered and that formatting is correct.

- Offer Suggestions: We may provide suggestions to the user based on context. A website may offer completed results in the search bar based on what the user has entered instead of requiring an exact match.

- Choose Good Defaults: Based on established user stories, we can offer defaults that fit an expected user requirement. The user will not need to specify all information if they use this default, eliminating the potential for error. For example, a website for booking restaurant reservations may suggest available timeslots.

- Use Forgiving Formatting: "Some tasks really do require users to type very detailed or precise information, but forcing people to provide this information in a very specific format can be at odds with good usability practices: If you are asking users to input numerical information into a form, be flexible, and format that information in a way that is easily scannable (by humans, not machines) in order to prevent mistakes." (9) We may format user input automatically, or sanitize user input, or provide clear restrictions.

Reducing Mistakes:

When users interact with an application, they have a goal they want to achieve. Based on the user's understanding of how the system operates, the user forms a plan. Then they take action based on this plan, and see whether their goal has been achieved. Mistakes occur when there is a mismatch between user understanding of the software and how the software actually works, leading the user to create a plan that results in an unexpected outcome (10). Generally, to reduce mistakes it is necessary to both convey the designer's model of the application to the user and to design the application in such a way that it is intuitive and easy to learn.


**Example:** 

### **6: Recognition rather than recall**
Minimize the user having to memorize and intake a lot of information by making objects, actions, and options clearly visible. The user should not have to remember how to get from one point of the application to another. Instructions for how to use the system should be easily accessible and visible as well, if appropriate. 

__Why is this important?__

"Recognition refers to our ability to “recognize” an event or piece of information as being familiar, while recall designates the retrieval of related details from memory (11)." According to this heuristic, we should design our software product to help users recognize elements and desired choices without needing them to recall too many specifics.

A modern user employs a variety of different software applications in their everyday life, and our application often will not occupy any special role for them that justifies the effort of memorizing exactly how to operate it. A dense and difficult to decipher user experience will discourage all users and drive them to seek alternatives, while a clear user interface is easier to learn and navigate. Users should not be expected to go out of their way to memorize how your system works (11).

__How can we implement this?__

- Research common user stories and use cases, and design the interface to enable users to go through these processes with minimal confusion. Users should be able to recognize information in-context instead of needing to remember it.

- Streamline user experience. Avoid nesting functionality if possible (i.e. users should not need to memorize certain paths to certain functionality)

- When instructions and help needs to be provided, try to provide this in context as opposed to requiring them to look it up. Reduce the amount of information the user must memorize.

**Example:** Having a navigation bar on a web application will allow users to go between different tabs without remembering how to get to them. 

### **7: Flexibility and efficiency of use**
Provide accelerators or shortcuts for experienced users so they can complete common interactions in a more efficient manner. This allows both experienced and inexperienced users to utilize the system to their own personal abilities and preferences. This will allow expert users to take advantage of the feature, and newer users can ignore it. 

__Why is this important?__



__How can we implement this?__

**Example:** Having a keyboard shortcut for a common interaction on your website.



### **8: Aesthetic and minimalist design**
Avoid providing unnecessary or irrelevant information to users. Keep dialogue concise and relevant to ensure that users are able to focus on the important aspects of the system and they are not overloaded with information that they don't need. 

__Why is this important?__



__How can we implement this?__

**Example:** Having a simple introduction page for the website, that can be expanded upon when the "More Details" button is clicked.

### **9: Help users recognize, diagnose, and recover from errors**
Provide accurate and straightforward error messages to users so they are able to understand and potentially fix the error. Ensure that error messages are written in simple terms, they clearly indicate the issue, and suggest potential fixes. 

__Why is this important?__


__How can we implement this?__

**Example:** When the user incorrectly enters their email to log into a website, it gives an error message saying "There is no account with this email associated. Please carefully re-enter your information or sign up."

### **10: Help and documentation**
It is better if a system can be easily used without documentation, but it may be necessary. In the case that your system is complicated and needs instructions, provide clear and concise instructions without any jargon that can be easily understood by new users. Ensure that the help documentation is easily found, searchable, and lists concrete steps.

__Why is this important?__


__How can we implement this?__


**Example:** A web application has a "help" tab with detailed instructions and documentation. 

## **Additional Resources**

Heuristics Applied to Videogames: https://www.nngroup.com/articles/usability-heuristics-applied-video-games/

Heuristics for Web Applications: http://designingwebinterfaces.com/6-tips-for-a-great-flex-ux-part-5

Heuristics Applied to Everyday Life: https://www.zenhaiku.com/archives/usability_applied_to_life.html



## **Citations**

1. Nielsen, J.; Molich, R. (1989). Teaching user interface design based on usability engineering. ACM SIGCHI Bulletin. doi:10.1145/67880.67885. ISSN 0736-6906. S2CID 41663689.

2. Molich, Rolf; Nielsen, Jakob (1990). "Improving a human-computer dialogue". Communications of the ACM. 33 (3): 338–348. doi:10.1145/77481.77486. ISSN 0001-0782. S2CID 11462820. Retrieved 4 February 2022.

3. Nielsen, J. (2012, January 3). Usability 101: Introduction to usability. Nielsen Norman Group. https://www.nngroup.com/articles/usability-101-introduction-to-usability/ 

4. Nielsen, J. (1994, April 24). 10 usability heuristics for user interface design. Nielsen Norman Group. https://www.nngroup.com/articles/ten-usability-heuristics/ 

5. Harley, A. (2018, June 3). Visibility of system status. Nielsen Norman Group. https://www.nngroup.com/articles/visibility-system-status/ 

6. Kayley, A. (2018, July 1). Match between the system and the real world (usability heuristic #2). Nielsen Norman Group. https://www.nngroup.com/articles/match-system-real-world/ 

7. Rosala, M. (2020, November 29). User control and freedom (usability heuristic #3). Nielsen Norman Group. https://www.nngroup.com/articles/user-control-and-freedom/ 

8. Krause, R. (2021, January 10). Maintain consistency and adhere to standards (usability heuristic #4). Nielsen Norman Group. https://www.nngroup.com/articles/consistency-and-standards/ 

9. Laubheimer, P. (2015, August 23). Preventing user errors: Avoiding unconscious slips. Nielsen Norman Group. https://www.nngroup.com/articles/slips/ 

10. Laubheimer, P. (2015, September 7). Preventing user errors: Avoiding conscious mistakes. Nielsen Norman Group. https://www.nngroup.com/articles/user-mistakes/ 

11. Budiu, R. (2014, July 6). Memory recognition and recall in user interfaces. Nielsen Norman Group. https://www.nngroup.com/articles/recognition-and-recall/ 