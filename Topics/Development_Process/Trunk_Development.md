### Trunk-Based Development

Knowing how to manage the creation of large new features in your repository is an important skill, especially when working in large organizations or on projects with complete CI systems. It can be tempting to have large feature branches with hundreds of new lines of code and it can seem daunting to implement a large feature in small stages. Trunk-based development is a system to handle large changes like this. It focuses on creating small pull requests and using tools such as feature flags. The following article from Atlassian does a great job discussing all the benefits of trunk-based development (i.e. impact on automated testing, having fewer active branches, and more): **[Atlassian Article](https://www.atlassian.com/continuous-delivery/continuous-integration/trunk-based-development)**

A picture that can help you visualize what trunk-based development might look like on a large team can be found at [trunkbaseddevelopment.com](https://trunkbaseddevelopment.com/)

![Trunk Based Development Diagram](https://trunkbaseddevelopment.com/trunk1c.png)

#### Feature Flags

As mentioned above, feature flags are a fantastic tool to use when engaging in trunk-based development. The article above explains them abstractly, but a more concrete example might be:

- Let's say you are working on a deployed website. You want to change the search algorithm but don't want to remove your old algorithm until your new one is finished. Because you are an excellent trunk-based developer, you decide to use feature flags!

- You create your feature flag and set it to false. Then when coding your changes, you make sure that when the feature flag is false, all behaviour on your website remains the exact same. However, when you set your feature flag to true, your new feature becomes enabled.

- Once your new search engine capability is fully ready, tested, and customer-approved, you enable your feature flag on deployment, and everyone gains access to it.

Notice how in the above scenario, if the new feature breaks the deployment, all you have to do is turn your feature flag off again!

#### Branching By Abstraction

Instead of using feature flags, one can also use the "branch by abstraction" method found in [this article](https://trunkbaseddevelopment.com/branch-by-abstraction/). This is similar to referencing an interface instead of a class and much like dependency inversion, can both increase or reduce the complexity of your code. Using the same example by above, you might make a searchAlgorithmInterface, and have both your old and new algorithms implement it.

It is up to the developer which method is better for a given situation.
