## Lights, Camera, GitHub Actions

In this article, we are going to discover this cool GitHub feature with a simple scenario that GitHub Actions will help us maintaining that. What's more, I show you why GitHub Actions is not a CI/CD tool. After you got familiar with the techs and basics, we will hop into the real-world issues and implement everything we talked about in a Pythonic way.

### Continuous Integration (CI)
In a sentence, this technique allows maintainers to keep their development healthier like a policy to keep track of all changes and modifications. An automated well-configured system that is intelligent enough to validate the changes that developers have done to the project. Implementing this automation system will separate to a few tasks. Since we are discovering Actions, we can be a DevOps guy but we don't need to. Anyone could learn it so let's hop into it.

### GitHub Actions
GitHub describes this feature as "A continuous integration and continuous delivery (CI/CD) platform that allows you to automate your build, test, and deployment pipeline" but you can do a lot more with Actions. You can simply trigger actions for whatever happens in/to your repository. GitHub Actions allows maintainers to manage all events that happen in/to their repositories.

#### Events
Any status that a third-party thing might occur in your repository is known as an event. Enough talking. Let me explain some of these events.

* When someone creates a new issue to your repository.
* When someone creates a new pull request.
* When someone or something pushes some commits to the origin remote which is the actual repository in most cases on GitHub.
* When someone forks your repository.

And more and more. You can find the full list of events [here](https://docs.github.com/en/actions/using-workflows/events-that-trigger-workflows). Now we both know what does an event actually look like. Using GitHub Actions, you can trigger a job (or multiple jobs) when an event occurs. (Like when someone creates a new issue to the repo)

#### Jobs
A set of tasks you need to do when an event is triggered. You can do multiple jobs in a workflow and Runners are responsible for running them. Each Runner can run only a single job at a time. You can have your jobs running distributedly on the different Runners. Depending on the job's dependencies, jobs could be run concurrently or parallel.

#### Runners
Runners mostly look like containers responsible for running your jobs. If you have tens of independent jobs so then you'll have tens of runners running your jobs at the same time.

Imagine you have two jobs. The first one does the following tasks.

* Preparing `ubuntu-18.04` environment.
* Updating `apt` packages for some reason.
* Installing `python3.10.2` and `pip`.

And the second job needs to do the following two tasks.

* Installing `django==4.0.3`
* Running `./manage.py test`

In this case, our second job has a dependency on the first one and the reason is that the second job can not install the `django==4.0.3` on NOTHING. There is actually no environment, no container, nothing at all. Once you define the dependency in your second job, Runner makes sure to run the first job first and the second one after it succeeds in completing the first job's tasks. So we have a sequential job running that Runner will keep track of. I told you they are brilliant, didn't I?

#### Actions and GitHub Marketplace
Let me bring you a Docker example, then start this section. You are a web developer trying to containerize your Django application. You start from scratch. Starting with `FROM ubuntu-18.04` in your first line of DockerFile and installing Python and so on.

Well, your main requirement will be `python3.10` so then why don't you use it as your base image?

Actions are quite similar to the official DockerFiles. An Action is a set of tasks that allow you to implement a service, application, configuration, or even a policy in your Runner container. You don't need to install Python on your own. You can easily use the Python Installation Actions and send them the `python-version` key to get your preferred Python version installed on your container. You can find tons of Actions on GitHub's marketplace [here](https://github.com/actions). You can also make yours for your company.

### Scenario
I'm a Python backend developer. I need to create a package to interact with an API service. I want others to contribute to my project so I aim to develop it on GitHub so that everyone can keep track of changes and commit their improvements and make PRs at the end as they wish. After a few years, my project gets viral. A lot of newbie developers try to contribute to my project in order to have something in their resumes. Since I realized the popularity of my package, I developed all my project's test cases and they work very well but the thing is that when someone forks my repository and makes his changes and asks for a merge, I have to clone his repository on my `/tmp` directory and test the project by myself since a lot of those newbies don't care about the syntax linting and test running at all.

Since I do some routines when I clone others' forked repositories, I need an automated runner to run those routines and show the results in the PR forum. Like a JSON-like configuration file that does the work.

```json
{
    ...
    "image": "ubuntu-18.04",
    "packages": [
        ...
        "python3.10.2",
        "pip",
        ...
    ],
    "commands": ["
        git clone https://github.com/foo/bar && cd bar |
        pip install -r requirements.txt |
        flake8 . --count --select=E9,F63,F7,F82 --show-source --statistics |
        flake8 . --count --exit-zero --max-complexity=10 --max-line-length=127 --statistics |
        python3 tests.py
    "]
     ...
}
```

Actually, there is. You can easily create your YAML configurations. You can also use the available configurations. All these configurations are called workflows. You can easily set up your preferred workflows on your repositories by browsing the available workflows. You better re-configure the YAML file for better results. For example, Github's Python App workflow uses `PyTest` by default in order to run tests, however, I used the [unittest](https://docs.python.org/3/library/unittest.html) standard library and running the `pytest` command brings me trouble so I change it to `python tests.py` and there we go.

> [Here is the scenario I implemented on GitHub](https://github.com/lnxpy/test-actions). You can check the `.github/workflow/` directory for more information about the tasks I'm running on the repository!

### Third-party Applications
You can run CI applications on your repositories like a code coverage tool that shows the statistics or even a tool to run the entire tests of the project. Since when you install a new CI application on your repository, you are actually giving them some privileges and you need to have credits in order to use some of them, a lot of them are useless in most cases and you are easily able to implement whatever you need in a few lines. Why would you install a CI UnitTest Runner Application when you can run the entire tests with a command?!

### Conclusion
All these technologies are designed to make development easier. You can have your project being developed by some contributors from all over the world when you're having fun with your friends on a trip. Learn them first, make use of them after.