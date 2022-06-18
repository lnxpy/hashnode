## Become an Open Source Contributor

We have used many open-source tools and software in our career life and technical journey so far but how are they being developed? How do people make an effort to do open source and make use of them? How can we be part of an open-source community?

In this article, we'll talk about some concepts behind the Open Source world. The way you should start your open source journey as a developer and professional ethics in an open-source community. If you're interested in open-source collaboration and you want to be a better open-source maintainer, this is a good point to start.

> You may not find this article that technical, but I tried my best to share my thoughts and experiences since I started working on open-source projects on the GitHub platform.

I assume you are already familiar with some basic development tools and platforms and you are about to work on your favorite repositories.

### 1. How to Start the Journey
In this section, we are going to talk about some tips before you start contributing to the Open Source.

- **Be humble and sociable**. An open-source community is where members from all across the world are grouped together to help each other and make awesome solutions for the problems existing in the real world. Everyone is contributing with love. Many of them are not paid to contribute. Being kind and affable in open source communities is the most positive ethical habit. Since you may not be familiar with other regions' cultures, so always be kind and respectful.

- **Always start small**. That's how you improve. When you start from small projects, you won't be stuck at much complexity and the development path and issues are much more sensible compared to the bigger tools.

- **Find the active projects**. As a contributor, you are happy with a project that has active maintainers and communities so your changes will be reviewed quickly and your questions will be answered faster. You can choose whatever project you find cool for contribution. Make sure they are not abandoned and they do accept contributions. Check out the `README` and/or the `CONTRIBUTING` file in the repository. You may look for the projects that your product relies on or even you may contribute to more popular projects to make a better resume and career experience.

- **Contribution is not just contributing to the actual code**. Many tools have their documentation in different languages. The documentation section is where most new contributors start their contributions from. You can find typo issues or even start translating the entire document into another language for example. Since many projects don't care about test developments sometimes, writing their tests is another good way to start.

- **Using an open-source tool may make you a contributor**. You may work with an open-source tool/framework. You see that the tool you are using is showing some unusual errors and there is something wrong with the tool. You check its repository and you find the issue. You decide to work on it and fix that bug. That's counted as a contribution as well.

- **Start from the issues**. You can simply fix an issue that another member faced a while ago. You don't need to experience it yourself to be able to fix the issue. Most repositories use GitHub's issue tab. That's a good section for starting. Make sure you keep your conversation public. Your decisions may help other developers/users one day.

- **Make friends out of the open-source**. One of the coolest parts of open-source is when you can contact other people from other countries and make connections. Making new friends in the open-source world allows you to grow up faster. Join communities, forums, and conferences, and try reaching out to others.

- **No room for panicking**! If your reasonable feature request gets rejected by a maintainer, or it's been months since you opened a PR and no one has reviewed it yet (a dead/abandoned repository), don't get disappointed. If your PR gets closed, there is a reason for that. With all respect, ask for the reason and remember that in your further contributions. They want to grow the project as you do that's why I suggest you open an issue first and talk about the improvements you think would be perfect and once they agreed, you can start the development. You'll save more time for sure.

### 2. Contributing to Large-Scale Projects
You may be wondering about contributions to larger popular repositories. As we understood, you always better start from smaller-scale projects first. You can figure out the contribution phases much easier since there is less complexity in those types of projects.

You can find the following files and directories in your desired repository. Let's see what they are for and how you can use them.

- **Git-based components**
 - `.git` - The actual git initiated folder used in the project.
 - `.gitignore` - Contains ignored patterns that git doesn't care of.
 - `.gitattributes` - To set attributes for files.
- **GitHub-based components**
 - `.github` - A directory where GitHub looks for action workflows, templates, and etc documents in.
 - `README` - It might be an `rst`, `txt`, or `md` file that contains explanations about an app or the repository.
 - `LICENSE` - A document that the repository is licensed under.
 - `CONTRIBUTING` - Contains the contribution steps you need to know about the repository.

The first step is to always check the `README` file first. Make sure the repository is active and then navigate to the "Contribution" section or the `CONTRIBUTING` file. Here is a `CONTRIBUTING` file sample depicted.

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1655550421367/LaUW65Tgg.png align="center")

To contribute to larger-scale projects, you should know the project first. Read its official documentation and [docstrings](https://en.wikipedia.org/wiki/Docstring) to understand each part. Dive through the project's files and directories. Understand its structure and architecture whether it could be monolithic or microservice. Whether it's Procedural or OOP.

Larger projects are separated into different applications and modules so the development will be much easier for the contributors. If you want to improve a function, you find both the module and tests much easier. A good practice could be reading the project's tests so you can find what kind of role each part do in the project.

In larger projects such as programming languages, there would be a guideline called "Developer Guideline" for those who are planning to contribute to the project. For example, [Python has its own development guideline](https://devguide.python.org/) and there is everything described there.

The tips we reviewed earlier would help you to become a better Open Source contributor. However, in most cases, you might be the maintainer of a project. In terms of maintenance, this road might be a bit challenging but in the following topics, we'll talk about some maintenance tips that make you a better open-source manager.

### 3. Jack of All Trades, Master of *Something*
As an open-source maintainer, sometimes you are in a circumstance where you need to start everything on your own. You need logos, banners, perfect documentation, and a clean well-structured repository and you are the only one standing. Having experience in some different out-of-circle skills may survive you in that situation. I personally believe that an open-source maintainer should be familiar with all technical fields. However, he/she must be an expert in a specific field. That's how you can give birth to a new idea and make it ready to fly. A little bit of marketing skill is always handy.

You should not only be highly skilled in your technical field to build a perfect foundation, but you better know about side skills as well. At least be able to satisfy your project's requirements.

> Open Source leadership requires significant technical skills in open source and the audacity in boldly using them – but only after you’ve studied the lay of the land, understood the group dynamics, and done some of the dirty work yourself. (The Linux Foundation)

### 4. Why Making it Open-Source
We are living in a world full of problems and difficulties. As a software developer, you are here to solve problems using your skills. No matter whether it's open-source or closed. Each project you work on is actually nothing but an idea. Let me explain with an example.

Consider you have an operating system installed on your computer. You've installed an application that you want once your system boots up, that application gets executed as well. You write a Python script to do that thing and it's working now. You have solved your problem. You can keep the script and use it whenever you face this issue again. You will no longer need to solve this issue again since you have a reusable solution for it. That script is nothing but plain text. The idea behind that is the most important thing.

When you make your script open-source, you are actually making that idea publically available to others. There are tons of benefits to open-source development. Maybe the most important one is that you figure out whether your idea/solution has the potential to improve.

Most of today's popular repositories were only an idea one day that was published publically and now they have many contributors and collaborators. The companies that are using those open-source projects are their awesome supporters.

### 5. Licensing
An open-source product is something that is licensed under an open-source license. When your project has no license, it doesn't mean that your project is open-source. Since licensing is a crucial part, I suggest you choose them carefully. If you don't feel comfortable with the existing [open-source licenses](https://choosealicense.com/licenses/) and you think they might not fit with your work, you can design your own license which I don't recommend.

### 6. No One Cares About my Projects
Many developers find it a bit tough to host their projects on platforms like Github and develop them in open source. Not technically but basically. You might have asked the following questions so I got my answers for you.

#### 6.1. My code is not that clean and perfect to push to GitHub!
There is no necessity for your project to be AWESOME to be able to be hosted on a platform like GitHub. You push the idea to make its implementation perfect. The idea you are working on might be a solution for another popular repository issue.

#### 6.2. No one reaches my projects and it has only a few stars!
You don't need to compare your new idea to those that have hundreds of contributors and stars. Keep making it better. Ask for help. Make issues on your own project. Join communities and ask them about your idea. Let them give you perspectives. Find out whether your idea has the potential to grow or not.

These are the most concerns that I myself faced many times in my journey whenever I wanted to start an open-source project. Please let me know if you have any questions about this journey in the comments. :)

### Conclusion
In this article, we talked about the crucial tips that you can use in your open-source journey to have a better experience and enjoy working on different projects even the popular ones. We also explained the licensing phase and at the end, we took a quick look and open-source maintenance.