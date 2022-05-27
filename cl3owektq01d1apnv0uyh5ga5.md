## Dependency Hell

This is where things get a scary turn! In this article, we are going to talk about a real concern that many maintainers and developers from the past decades were worried about. This topic does not rely on any specific framework, programming language, etc. Since our products need some requirements in order to work efficiently and we (developers) hate to waste our time on nothing, we need to think about this BIG issue.

We all know that our projects whether it's a mobile application software or a Python program that interacts with an API, need some necessities to be working fine. Those necessities are called "Dependencies" in our world.

I'm pretty sure that you've already been in some situations where you needed to install some packages in order to be able to work with some functionalities and implementations. Most of the time, you simply use a package manager and install your required packages. Each installed package may need some other modules and packages to provide you the facilities and so on.

Now, imagine your project getting bigger and bigger. As it grows and you add new features, it requires more dependencies and modules. We can shape the dependencies into a graph-like illustration that shows the actual application dependencies and the required packages by dependencies.

For this article, we use `PKG NAME:version` pattern to show the package name and the version number. We also use those routing lines to show the package dependency as well. In the following image, you can see that our `App` has some dependencies on `Q:3`, `Z:5`, `F:1`, and `S:4` packages. Some of those dependencies have their own requirements on `E:8`, `P:1`, and `H:2` and that's how it goes.

![Artboard 1@4x.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1653670363347/XOm_cpwAe.png align="left")

Let's see how things get messy!

### Many Dependencies Situation
You've probably seen this situation where your product has lots of dependencies on the different live/dead packages. I'm using live and dead words to show a package state. A dead package refers to a package that's totally abandoned and no one contributes to it anymore. Don't want to make a sad story out of this article so let's move on. :)

Overall, having tens of dependencies might bring you some troubles especially when you're planning for an urgent update. You've been working on a project for two years and now, you have tens of features in your project. You need to upgrade your main framework in order to fix some security bugs or even better performance. You are using `PKG A:1` and now, after two years of maintenance, you update the main framework so then your `PKG A:1` can't keep up with the new version of the framework anymore since it was released two years earlier. This is a common issue in the case of installing packages as 3rd party applications. That would be a huge mess.

The best approach is to implement things you need on your own as you can do. Like the **minimal** features and implementations that you may need in the different parts of your product. Why would you use a third-party package for getting the current system time since you can use the same functionality from the make-ready available local site-packages? (Also known as the standard libraries as well)

At the end of the article, we will talk about the solutions and best conventions.

### Chain of Dependencies Situation
In this situation, your project has a dependency on `PKG A:1` which depends on `PKG B:1` which depends on `PKG C:1` which depends on `PKG D:1`, and so on. This is a horrific situation where you have a chain of dependency behind your project. Whenever a piece of this chain breaks, your project won't work as usual. At least, some features may not respond correctly.

One of the common issues that maintainers run into in the case of having such a chain is when you have a conflict with the versions of packages in a system. Remember that you can not have multiple versions of the same package installed on a computer normally. For example, we are not able to keep both `PKG C:1` and `PKG C:2` at the same time in a project running system. (Just think of past decades. No advanced package managers)

Let's see how you might break the packages and run into conflict situations.

### Chain of Conflicts
We learned about dependencies and how our dependencies might get chained together. So, let's see a simple conflict that might happen in any project.

We have our `App` already designed on the left hand side. Our application depends on `PKG A:1` and `PKG B:1` and both of those requirements are depending on `PKG C:1` so far.

![Artboard 1@4x.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1653570625836/vLqVEy33E.png align="center")

Everything sounds cool and clean. After a few weeks, `PKG A:1` maintainers find a horrific security bug in their package and after a few days, they release `PKG A:2` with a higher security layer and they fix the issues.

Since we care about the security of our project, we decide to upgrade our `PKG A:1` to `PKG A:2` for fewer possible security threats and that's what happens!!

![Artboard 1@4x.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1653570532093/NnNYG9Rpt.png align="center")

As we described earlier, we can't keep two different versions of the same package in a running system. Once we prepare the `PKG A:2`, we see that the new `PKG A:2` now depends on `PKG C:2` which was `PKG C:1` in the previous version of `PKG A`. Since our `PKG B:1` still depends on `PKG C:1`, how can we prepare both `PKG A:2` and `PKG B:1` at the same time?!

Well, that's a simple versioning conflict. Today, package managers have their own algorithms for facing such a situation. In an upgrade situation, before they touch anything, they read from the databases and check for any possible conflict in the system. They draw the graphs, analyze the packages, and check the routes, and their last step will be upgrading/downgrading/installation or even uninstallation processes. That's a good convention but how this conflict can be solved?

As a maintainer, we can wait for a new release from `PKG C` which would probably support both `PKG B:1` and `PKG A:2`. Like we have to keep those threats till the new release comes out from the `PKG C` maintainers or even we can touch nothing and keep those threats on the hush!

![Artboard 1@4x.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1653570773139/nTfRNj8he.png align="center")

Also, there might be a new release as `PKG C:1.0.1` which is actually a minor change for supporting both packages. It actually backs to the maintainers' choice.

### Circular Dependency
There is another situation where our dependencies depend on each other. In the following situation, the package `PKG Q:3` only works if `PKG Z:5` works as well and vice versa. On the other hand, we have the package `PKG F:1` which depends on `PKG S:4`, and the package `PKG S:4` can't work without `PKG F:1`.

![Artboard 1@4x.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1653576441730/f2r7v_gZo.png align="center")

In this situation, we have a circular dependency on each package. If one breaks, the other one won't work anymore.

Now, let's describe the solutions and best practices to keep the hell's door closed.

### Package Managers, Microservices & Project-level Tests Solutions
In the monolithic infrastructures, there is way more possibility of having conflicts since we are serving the whole service from the same running system and scope. In the microservice structures, we have our services separated from each other so then we don't care about each service's dependencies since they are responsible for their own requirements. In this structure, debugging the issues would be way easier because we are talking about a smaller scope and service. That's actually another meaning of having isolated services. They have their developers, resources, tests, package managers, and so on.

Thinking of package managers. They are smart tools for managing the dependencies and they have advanced implementations to avoid any conflict on our machines.

Even nowadays, you can find some package managers still can't actually solve the conflict issues among the packages and their dependencies. In most cases, they suggest you the reinstallation process which is truly painful.

You might have been working with multiple package managers such as [Pacman](https://wiki.archlinux.org/title/pacman), [APT](https://ubuntu.com/server/docs/package-management), [YUM](https://www.redhat.com/sysadmin/how-manage-packages), or other ones. You can read about their history to find how they've been solving the different issues on the different machines. Choosing the right package managers (officially announced ones) would be the key to the dependency paradise!

Last but not least, a great solution to your dependency issues is writing tests for your projects. When your project has its own tests, it's actually testable in the different environments and situations. You can easily test your project with the different versions of packages and dependencies. Most testing tools will also notify you the news about the deprecation, substitutions, and things that might affect some of your project's features after the upgrade process.

### Conclusion
In this article, we described a simple situation where a tiny bit of dependency conflict might happen in the system. Then we moved to the conventions and solutions. Nowadays, with the rise of the powerful package management tools, we may never feel those conflicts anymore.