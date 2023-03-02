---
title: "How Not to Debug: Spend  Less Time Debugging"
datePublished: Thu Mar 02 2023 15:15:11 GMT+0000 (Coordinated Universal Time)
cuid: cler907g4000b09jlfft19axh
slug: how-not-to-debug-spend-less-time-debugging
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1677421147208/e64cd2cc-ba0f-4a89-9182-d34e66a35324.png
tags: developer, tips, debugging, best-practices, debuggingfeb

---

Bugs.. they're everywhere but today we're going to end their life. While you're reading this blog post, tens of bugs might be celebrating and having fun through the lines of your codebases and source code logic. Somebody needs to rise, say enough is enough, and ruin their celebration.

> In spite, everyone has already talked about the ways you can debug better according to the implementations and new technologies on [#DebuggingFeb](https://hashnode.com/n/debuggingfeb), I decided to talk about the ways you can reduce the time you spend on debugging your codebases and stay more productive at work.

This article is about the methodologies and techniques that may sometimes take effort to implement but will save you time debugging your source code repeatedly. By using these smart tips, don't waste your time debugging anymore.

Follow towards the end and catch the ✨BONUS✨ section.

### I. Logging

It's highly recommended for you build a logging structure for your codebase if your project/service has an Accounting application or interacts with users and clients.

A good logging system takes effort to build but when it's ready to work and is being used everywhere in your project, it always gives you clues to each issue happening through your system and service.

Keep in mind, building a logging system for a project at the very beginning of its development phase is way easier than making one for an already made project as it might not be precisely clear for the developers seeking bugs.

By using third-party [Issue Tracking Services](https://en.wikipedia.org/wiki/Issue_tracking_system), you'll be able to track every single exception of your online service even in more detail. The following image is related to the exceptions of a Django service on [Sentry](https://sentry.io/). It acts like a board. You can make assignments on each issue and create tasks for fixing them.

![Issues | Sentry Documentation](https://docs.sentry.io/static/1952fe078726628cb4cf817f2ec967fd/21b4d/issues-homepage.png align="left")

Using different automation testing conventions would reduce the occurrence possibility of issues and exceptions. We'll talk about it a little later.

**Why logging..**

* It helps us keep track of bugs.
    
* It makes debugging easier and less time-consuming.
    

### II. Proper Exception Handling

Handling the exceptions properly helps you make your logs more accurate. Thinking of Exceptions reminds us of some familiar keywords depending on the programming languages we use.

We typically catch the exceptions without mentioning the exact Exception type and that's the main issue here. Let's say we're supposed to write a script to log the user's connection to the internet. Let's write it this way.

```python
# checking if the device is connected to the internet
try:
    _ = requests.get('https://google.com/')
    logging.success('device connected to the internet')
except:
    logging.error('device could not connect to the internet')
```

It looks pretty clean but there is a huge mistake here. If we cause a different type of exception raised in the `try` block such as a typo by any chance, our logger deals with the issue just like a network issue and that's the problem of bad exception handling. Instead, we could've handled the exceptions as follows.

```python
...
except requests.ConnectionError:
    logging.error('device could not connect to the internet')
```

Now, our logger won't eventually log the wrong phrase for any of the other exceptions raised and our logs will be perfectly straight and clueful.

**Why proper exception handling..**

* It helps us write accurate logs.
    
* It avoids misunderstandings throughout the debugging time.
    
* It helps us identify any potential issues with our code before they become what we call "Bugs".
    

### III. Testing

Running tests in different stages of development ensures that pieces work together correctly. Sometimes, dependent components cause bugs in our programs. It's tough watching out for every single module of every package of the service while developing. That's why we use testing to test each part of the service regarding the changes we make.

Writing good tests that cover almost all units of the service takes effort but with the help of automated CI testing tools such as [GitHub Actions](https://github.com/features/actions), you can test every change within the pull requests right before the bugs could even find their way to your projects.

**Why testing..**

* It watches out the whole project for any threatening issues.
    
* It prevents bugs from finding their way to your project with the help of automated CI tools.
    
* It ensures you focus on the part you're developing other than being concerned about your changes that might break something from another module or package.
    

### IV. Use Version Controllers

I personally can't agree more that the reverting action is life-saving. Using tools such as Git, allows us to keep track of even every single character we change in the source code. If you screw something up, there is always a way to revert that in version controllers. Of course, it's not enough. Hooks are the true bug-catchers.

Git Hooks act like gates. For instance, [pre-commit](https://pre-commit.com/) hooks will run some checks on your changes before you make a commit. You can run various checks on each change you have staged. Here are some popular hooks.

* Running tests.
    
* Check linting and formatting.
    
* Checking the commit message pattern.
    
* Re-generating docs.
    
* Re-generating internationalization files.
    

Here is a simple preview of how pre-commit hooks start working right after you decide to commit the staged changes.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1677750897214/6760c844-280f-4c50-a040-cba89dfaf072.png align="center")

**Why use version controllers..**

* It helps us keep track of changes we make to the source code.
    
* It makes inverting changes easier even in higher-scale collaborations.
    
* Its hooks (pre-commit) help us run automated checks right before making commits.
    

### V. First Plan, Then Code

Before you get your hands dirty with codes, take the pen and architect your project. Sketch its structures, dependencies, capabilities, features, and possible weak spots. Create tables and diagrams. Draw the needed flows. You may not notice but lots of bugs could be fixed on paper.

Once everything looks obvious and ready for implementation, then `git init`.

### VI. Relax & Get a Rest

Programming is the work of the mind. You may not feel tired physically, but your brain needs rest. Sometimes, it's better to turn your PC off and take some time for yourself. Go for a walk, and get some fresh air. Humans' anatomy works just like smartphones. It needs battery power in order to work efficiently. In some cases, some bugs may tick you off and run on your nerve. The following exercises help you recharge yourself and come up with brilliant solutions at the debugging time.

* Go exercising.
    
* Sleep enough.
    
* Relax and listen to calm (chilling) playlists.
    
* Read non-technical books. (novels)
    

Here is my [**Burnout: The Time You Hate Everything**](https://imsadra.me/burnout-the-time-you-hate-everything) article talking about the same specific subject.

### ✨BONUS✨. Practice Makes Perfect

I still believe that this section should've been the first section of this article since it does but it's ✨BONUS✨.

Practice does make you perfect. It's easier to make bugs than to write a program and the only thing that proves the opposite is how experienced you are. As you're coding more along and work on more projects, you experience some bug-making situations frequently and that's how you get better at something.

It's alright dealing with tons of bugs in your first experiences of coding. In fact, it won't seem normal if you don't make bugs. You have got to be a machine that way.

Practice different procedures, techniques, and best practices regarding your technical stack and programming language, and always keep them in mind and observe them through your daily coding tasks.

Follow these tips. They'll give you a precise road for finding valuable connections and knowing various techniques as a software developer.

* Contribute to open-source.
    
* Join coding communities.
    
* Create an active profile on Stack Overflow.
    
* Team up and contribute to online Hackathons and in-person coding challenges.
    
* Read from others, write for others.
    
* Listen to coding podcasts and join online or in-person conferences.
    

### Conclusion

In conclusion, debugging is an essential part of software development, but it can be time-consuming and frustrating. By implementing the methodologies and techniques discussed in this article, you can reduce the time you spend on debugging and become more productive at work. Building a logging system, handling exceptions properly, testing, using version controllers, planning before coding, taking breaks, and practicing are all valuable tips that can help you become a better software developer. Remember, practice makes perfect, and by following these tips, you can become more efficient and effective in your work.