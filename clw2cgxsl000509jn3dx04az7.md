---
title: "PyAction - Create GitHub Actions Using Python!"
datePublished: Sat May 11 2024 16:52:38 GMT+0000 (Coordinated Universal Time)
cuid: clw2cgxsl000509jn3dx04az7
slug: pyaction-create-github-actions-using-python
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1715301543194/b148ed33-3be3-4237-b430-ff652da393f0.png
tags: github, python, continuous-integration, opensource, continuous-deployment, python3, devops, cicd-cjy1vtdk2005kjjs17n8couc3, github-actions, github-actions-1, mindsdb, pyaction

---

GitHub Actions was introduced in 2018. Since then, GitHub Marketplace has witnessed numerous brilliant ideas that have impacted the Continuous Integration and Delivery world.

As GitHub says..

> Actions are individual tasks that you can combine to create jobs and customize your workflow. You can create your own actions, or use and customize actions shared by the GitHub community \[aka Marketplace\].

In this article, we will demonstrate a simple implementation using PyAction, a tool that allows you to create actions using Python. This way, you can take advantage of Python libraries and bring your ideas to pipelines!

Additionally, we will discuss the recent release of PyAction and the new features that have been introduced in version 0.6.x.

### Actions in a Nutshell

In the following example, you see a simple pipeline in GitHub Actions that triggers on the `push` event and executes the bash script `echo Hello world!`. You can place any bash script there to run, including an API call using `curl` maybe!

```yaml
name: CI Example

on:
  push:
    branches: [main]

jobs:
  Builder:
    runs-on: ubuntu-latest

    steps:
    - name: Greeting
      run: echo Hello world!
```

We have a `Builder` job with just one step, which is executing a shell script. Actions are like functions. Considering the earlier example, what if you wanted to send an email instead of running a bash script?!

```yaml
    ...
    steps:
    - name: Sending email
      run: python send_email.py # hmm.. let's see.
```

Well, thanks to @[Dawid Dziurla](@dawidd6), there is already an action designed for this purpose. You can modify your pipeline to use it in this manner.

```yaml
    ...
    steps:
    - name: Send mail
      uses: dawidd6/action-send-mail@v3
      with:
        subject: Github Actions job result
        to: someone@somewhere.com
        from: Sadra Yahyapour
        body: CI workflow executed successfully!
```

As you can see, we are now using the `dawidd6/action-send-mail` release `v3` action with certain input parameters (`subject`, `to`, `from`, and `body`).

The aim here is to introduce a solution for creating actions using Python and have the ability to call it with the desired input parameters.

Worth noting that the `action-send-email` is written in JavaScript and we're talking snakes here. [🐍](https://emojipedia.org/snake)

### Creating an Action

Technically, GitHub offers three ways to develop custom actions.

* JavaScript actions
    
* Docker container actions
    
* Composite actions
    

Let's focus on the Docker container and Composite options. Composite actions are actions created using only bash scripts. Essentially, you have the freedom to perform various tasks within a Composite action. You can compile and execute C programs, install tools based on the optionally-limited `runs-on` image, make API calls, and more. In essence, Composite actions offer flexibility.

On the other hand, Docker container actions are restricted to the base image specified in the `Dockerfile`. You can then add additional layers. PyAction follows the Docker container approach and runs your action within a `python:3-slim` environment. This is what PyAction uses to run your Python actions.

### Using PyAction

PyAction is delivered as a third-party package needed for your action to function. Despite this, it is very stable in the local environment for testing. Therefore, you can use it on your local machine easily and even test your action before deploying it.

#### Installation

Make sure you have `pip` and `python>=3.8` available on your machine and run the following command to install `pyaction`.

```bash
pip install -U "pyaction[cli]"
```

#### Creating a base template

It is highly recommended to use the `init` command to generate a base template for your action. You can then build your action on top of this structure by answering some questions.

```bash
pyaction init
```

| **Question** | **Description** | **Example** |
| --- | --- | --- |
| Action name | Action name | SMS Action |
| Action's slug | Slugged version of the `Action name` (better left with the default value) | sms-action |
| Short description | Short description about the action | Sending SMS Messages |
| Author's name | Author's name | John Doe |
| Include workflow testing pipeline | Creates a `.github/workflows/test.yml` for self-testing the action | `y` |

This prompting would give us the following action tree.

```bash
sms-action/
├── Dockerfile
├── README.md
├── action.yml
├── main.py
└── requirements.txt

1 directory, 5 files
```

#### Hello world example

Let's take a look at a simple `hello-world` example created with PyAction. The goal is to set up an input parameter for users to send their names, and then we will greet them!

After you've initialized the template using the `init` command, it's time to define the input/output parameters. Open the `action.yml` file to declare them.

```yaml
...
inputs:
  name:
    description: user's name
    default: World

outputs:
  phrase:
    description: greeting message
```

Open the `main.py` file. And create the very basic `greeting_action` inside it.

```python
from pyaction import PyAction


workflow = PyAction()

@workflow.action()
def greeting_action(name: str) -> None:
    workflow.write(
        {
            "phrase": f"Hello {name}!"
        }
    )
```

As you can see, the `greeting_action` takes one parameter called `name` which is a string. It also writes to the workflow the variable `phrase`. We've defined them both in the `action.yml` file.

#### Testing

To test if the action works as expected, there is a `run` command that does the job for us. However, before we proceed with the execution, we need to simulate how action runners invoke the actions with the defined input parameters.

Create a `.env` file inside the action to simulate the input parameters of the action.

```bash
INPUT_NAME=Sadra
```

Now, by running the `run` command, you'll see the variables that the `workflow.write()` method writes to the workflow.

```bash
pyaction run
phrase=Hello Sadra!
```

The `phrase` variable is accessible in other steps of the user's workflow.

```yaml
    ...
    steps:
    - name: Greeting action
      id: greeting
      uses: you/greeting-action@main
 
   steps:
    - name: Showing the message
      run: echo ${{ steps.greeting.outputs.phrase }}
```

#### Publishing

To publish the action on the marketplace, you need to consider certain things during the development process. After developing your action, there are some post-development tasks to complete before delivering it to the GitHub Marketplace, such as tagging and releasing it. If you wish to proceed, refer to the [**publishing in the marketplace**](https://pyaction.imsadra.me/tutorial/#publishing-in-the-marketplace) section in the documentation.

This `hello-world` action is also available on [https://github.com/lnxpy/pyaction-hello-world](https://github.com/lnxpy/pyaction-hello-world). Feel free to check it out! ✨

### New Features in v0.6

In the new v0.6 release, a few major features were announced.

#### Issue Form feature

As GitHub describes the issue forms..

> You can define different input types, validations, default assignees, and default labels for your issue forms.

It's a reliable solution for controlling users' input when they open issues on your repositories. By using this feature in PyAction, you can allow users to interact with your actions through the issues tab by filling out the designed form.

For example, take a look at the following repository. It uses the Issue Form feature to serialize the details within the opened issue. It then utilizes this information to invoke MindsDB's [mdb.ai](https://mdb.ai) service and obtain the output from ChatGPT. Lastly, it comments on the result.

%[https://github.com/lnxpy/mdb-ai-prompted-text] 

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1715446091005/11a2b4f7-943d-48f1-8691-4182c67be7be.png align="center")

Check out [this page](https://pyaction.imsadra.me/tutorial/#issueform) for more information about how this feature works.

#### Running additional bash scripts before invoking the action

If the action requires some additional system dependencies or you want to run some additional commands before the action starts running, you can put all the commands inside a `script.sh` file inside the action directory. It'll be executed even before your action's Pythonic dependencies installation.

Check out [this page](https://pyaction.imsadra.me/tutorial/#running-additional-commands) for more information.

#### Local testing

With the `run` command, test the action locally before publishing your action.

### Composite Actions vs PyAction

PyAction uses the Docker container convention to create an isolated environment using DockerHub-hosted images. On the other hand, with a composite approach, you have to go through several steps to set up a Python-friendly environment before implementing your idea.

In a composite action, you often make many external API calls. In contrast, PyAction relies on internal API calls, which are quicker and more secure.

Ultimately, PyAction simplifies local action testing by simulating inputs and outputs.

### Useful Links

* PyAction Repository: https://github.com/lnxpy/pyaction
    
* PyAction Docs: https://pyaction.imsadra.me
    
* mdb.ai Action (that uses Issue Forms): [https://github.com/lnxpy/mdb-ai-prompted-text](https://github.com/lnxpy/mdb-ai-prompted-text)
    

### Conclusion

GitHub Actions is a platform commonly used for performing CI tasks on projects hosted on GitHub. I developed a tool called PyAction to allow users to create custom actions using Python. PyAction includes a range of features such as local testing.