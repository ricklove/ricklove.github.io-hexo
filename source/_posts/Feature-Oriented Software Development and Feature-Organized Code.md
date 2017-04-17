title: Feature-Oriented Software Development and Feature-Organized Code
date: 2014/2/4
---

Software development is all about the apps. If you don't have a user interface, then your software is pointless. There must be a way for somebody to work with your software to accomplish what they want to do. These are the features: what your app can actually do. Really, an app is nothing more than a collection of features. The best apps have few features that are closely related and are exceptional in quality.

Therefore, *software development should focus on developing features.*

All too often, we developers focus on the code, "Look how cool that code is." Users don't care. They want a cool feature that works – that is all. They don't care about your hard work. If you don't give them exceptional features, they will trash your app (1-star) and nobody will ever touch it again. 

We must focus on the features. We must make exceptional features that shine. That is the entire purpose of software development. In fact, maybe we should just drop that term and call ourselves "feature developers". Software is pointless unless it contributes towards exceptional features.


### Background

We developers are overly focused on our code. Look at the OOP (Object Oriented Programming) paradigm for example. It's main concern is how you design your class hierarchy. 

That has little to do with a feature. So we have Use Cases where we try to figure out every possible way an object might be used. That is getting closer to the features, but it is putting the developer's concern (class design) ahead of the user's concern (features).

OOP solves many problems, but it also introduces a way of thinking that produces unnecessary complexity. A developer has the impression that he must design perfectly defined types that can handle all possible scenarios before programming can begin.This results in the common tendency of unexperienced programmers of trying to solve "world hunger" with every project. Many times he doesn't even remember what feature he is trying to implement.

However, even a developer with an idea of the desired features can face a complex project. At the beginning of a project, each class is well defined and exists in a small easy to read and understand file. However, each new feature introduces changes that can span multiple class files. Over time, these files grow bloated with unrelated code. Even more, as multiple developers modify those files for their own needs, they can contain multiple styles and design patterns that make the code for that class very difficult to understand. Feature dependencies can be strung throughout the code base. "You can't change that because it will break this. Oh and users have become used to that bug so don't fix it." 

The entire project becomes a dark and dangerous place where you might violate some unwritten law by changing something you weren't supposed to change. Then, you make yourself an enemy of the whole team who has to waste hours trying to trace down all the unexpected bugs caused by your change. As stress builds, the team becomes more concerned with who to blame rather than developing good software together. Obviously, this does not contribute to a positive development team.

My observation is that the end result of traditional OOP is an exponential growth in the cost of adding each new feature to a project.

Software development should not be object-oriented. In fact it should not be oriented to anything to do with the code itself. Software development should be feature-oriented. Developers should always have in mind what feature they are contributing towards. 

With the big picture of the target feature in mind, then a developer can use whatever code most simply implements that target feature.

(Keep in mind that there are "system features" which provide the foundation on which the "user features" are built.)

### Thinking Differently about Code Organization

My experience with C# and it's changes over the years eventually led me to a different way of organizing my code. 

The introduction of partial classes to C# initially allowed a simple way to separate designer generated code from human code.

Then later, extension methods allowed me, being used to strictly defined traditional OOP types, to start thinking about types that could be extended at a later time.

Then, my exposure to javascript with its purely dynamic types made me realize even more possibilities about objects and type definitions and how they could be extended even at runtime as needed. 

In the end, these experiences led me to organize my code differently than I had been taught or had ever done before. In my latest project, I unintentionally organized my code in what I will call feature-organized.

### Towards Feature-Organized Code

As I was working on this project, I wanted a clean working space so that I could focus solely on a single feature at a time. Therefore, each time I started implementing a new feature, I added a new file to the project and kept all the code related to that feature in that file.

However, I was still working with the same set of objects and their classes. Still, I wanted to keep all the additions to the classes near to the features that needed to use those additions. For example, when I needed to add another property to a class, I wanted that property to be defined right there in the same file with the logic that used that property, instead of going to the file where the class was originally defined. 

This was simple to do because of partial classes in C#. I was able to continue the definition of any classes in that feature file. I added whatever properties or methods needed to exist for that feature to work. Also included were classes that only had meaning for that specific feature and any processing for it.

This would have been possible in
many languages, not just C#. It would be simple to implement in any language that has a mechanism to allow open type definitions that span multiple files or any language that supports dynamic types. (It is also possible in languages with closed type definitions, but not as simple.)

### What is Feature-Organized Code?

Feature-organized code is code that keeps all properties, methods, and any logic related to a single feature in the same place. 

The source files are grouped together by features rather than by class definitions.

Instead of having everything about a  class exist in its own file, the parts of the class are defined where they are needed. 

Obviously, balance is needed. A good balance is to define the primary set of classes in the "core feature". These core definitions would basically represent the data of each class by implementing a constructor to create the object and fields or properties to hold the data for that object. Then in the feature files, these core definitions can be extended with calculated properties and methods needed for that feature.

The core feature is concerned about the construction of objects. Other features are concerned about using those objects. 


The code to implement each feature could be organized as a single file or a collection of closely related files:

- One file (Simple Features that require only a few types)
- Multiple files with a similar name prefix (In a project with a small number of features)
- A sub folder (In a medium project with complex features that only work when many objects coordinate)
- A sub folder for each app layer with similar naming (In a large project that includes multiple layers that each exist in their own projects: i.e. a Data Access Layer, Business Logic Layer, Application Layer, Unit Testing, etc.)

### Advantages of Feature-Organized Code

- Singular Focus

The developer sees only code that is relevant to a single feature in each file. He can focus entirely on that one feature without thinking about the concerns of other features. 

- Predictable Locating of Feature Code

Each feature has its own specific place among the many files of the project. Everything about that feature's implementation can be found in those files.

- Clear Dependencies

Every class and the properties and methods that are needed to implement a feature are all together in the same place. This provides a complete picture of all dependencies required for that feature.

Also, if a feature depends on another feature, that can be clearly indicated in a comment at the top of the file. I refer to these as parent and child features.

- Isolation of Features

The implementation of each feature is isolated from other unrelated features. In many cases, it is even possible to remove an entire feature and all the changes it introduces to the class hierarchy simply by removing those files from the project. This can be done without affecting any other features (except it's child features).

- Rapid Orientation

Since all code for a single feature is together, a developer can quickly orient himself with the entire scope of a feature. There is no need for him to comprehend the entire class hierarchy of the entire project. He must only understand the properties and methods currently being used by that single feature. This is simple because their definition is right there with the code that uses them. He has no need to dig through multiple files of class definitions looking for the various properties and methods of concern, being distracted and overwhelmed by everything not currently relevant. 

In addition, if each layer of the application is organized in a similar fashion he can quickly locate the business logic and data access relevant to that feature. In fact, if the data access layer is segmented in the same way, then he can also see what tables, columns, and other db objects are relevant to that feature.

In this way, a developer can quickly get a full picture of everything relevant to that feature from the database all the way to the user interface. 

This is the key to development that does not scale up in cost as the project grows. Whether the project has 5 classes or 1,000, the developer can learn everything relevant by simply looking at the feature files. He doesn't even need an IDE to help him randomly browse through the code, jumping to definitions that are scattered across thousands of files. He can simply read the files of that single feature to get a complete picture of it.

- Isolated Development

One possibility that this provides is isolated development of features. Because all code for a feature must be in a certain location, developers can easily work on different features without conflicting with one another. Developers can make changes independently and quickly without worrying about who else might be affected by their work. Also, if a change is required beyond the current feature (like in a parent feature), they can communicate those needed changes to a senior developer who can then coordinate how to proceed.

- Secure and Simple Outsourcing

For large projects, a sub project can be created which includes only a copy of the necessary features (the target feature and it's parent features).

This sub project would greatly improve the performance of the outsourcer because it presents him with only the relevant code. This reduces the likelihood that he will make changes in the wrong location or be overwhelmed by the complexity of a large project.

It also improves security because the entire source code is no longer being passed on to a partially trusted party, nor is it necessary to allow him access to the team's source control or other servers. This can be very important for large closed-source projects that have sensitive code.

Also, the outsourcer can send his changes in just by zipping up the subfolder for the target feature. This outside code can then be code reviewed just by reading that small group of files without even needing an IDE. (This could even be done on a smart phone through email where the developer in charge of the outsourcing can quickly provide feedback to the outsourcer.)

When the outsourced code reaches an acceptable point, it can easily be merged back into the main project simply by copying those files (likely into an isolated branch in source control). All affected files would be in one location and could easily be code reviewed and tested before being accepted into the main project.

If this were a common scenario, it would even be possible to make some build tools that automate the process of creating these isolated sub projects for a single feature. The build tool would need only a list of features (the target feature and its parent features). Then it could simply include those folders and produce a new project file with references to only those items.

This may even be the preferred means of development for the entire development team. It would greatly improve build times for large projects and would boost developer productivity by allowing them more freedom of control over their development environment. (They could work from home on their own machine for example.) This also introduces great training possibilities for new developers that would help them ease into familiarity with the main project without being overwhelmed by its large scope.

- No Ownership of Code

Because every feature is isolated and relatively small in comparison to the entire project, it also remains as simple as possible. 

This prevents ownership concerns in the development team. Each developer works on a feature until it reaches maturity, then he moves onto another feature. Another developer may revisit that feature at a later point to improve it. Because of rapid orientation, any of the developers should be able to work with any feature. There are no hidden dependencies that will remain the secret of the "owner" of that code. Everything relevant and every dependency is contained in one small set of files.

- High Quality Features

It can be simple to ensure that each feature contains every component that ensures high quality: Documentation, conformance to code conventions, unit tests, code coverage, code contracts, a polished user interface to that feature, etc.

A feature would not be considered mature until it reaches the highest standards of your application. It can easily be excluded from release until it can meet those standards. 

This compels the development team to complete fewer high quality features instead of many mediocre features. 

This brings us back to feature-orientation. Again, an app is nothing more than a collection of features. This focus on high quality features produces apps that users enjoy and will outshine their competitors.

### Conclusion

Feature-organization of code is a key to promoting a feature-oriented paradigm for software development.

I will be using this concept in my own development and will later come back with some practical tips on how best to implement feature-organization.

