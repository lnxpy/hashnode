---
title: "Introducing Hey! - Your AI-powered Pair Programming Friend"
datePublished: Wed Apr 26 2023 14:03:43 GMT+0000 (Coordinated Universal Time)
cuid: clgxro5ik000l09kyh9pl5az3
slug: introducing-hey-your-ai-powered-pair-programming-friend
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1681801520684/bb66c4fe-43a8-4246-bf2c-7a72950056ec.png
tags: cli, chatbot, mindsdb, chatgpt, mindsdbhackathon

---

### Introduction

%[https://www.youtube.com/watch?v=fhO34PVa-38] 

**Hey** (/heɪ/) is an AI friend that helps you alongside your coding projects' development. It's powered by the OpenAI's GPT models that MindsDB supports. This command-line tool can easily act like your non-human pair programming partner that's smart enough to clean your codes, refactor them, and give solutions based on different cases.

I named this project "Hey" because I thought that would be a nice sweet way to start a conversation with an AI.

I had been using some free services that used to give me free limited access to OpenAI's services, ChatGPT as such. Since I'm more of a CLI guy, I had to switch back and forth between my terminal and browser just for a quick answer to my question from ChatGPT. With the help of MindsDB, I easily implemented a secure interface and named it Hey, and since then, I can ask the model MindsDB trained for me, whatever I want from wherever I have access to a CLI shell. It could be either a VScode terminal panel, the system's terminal app, or even [TTYs](https://en.wikipedia.org/wiki/TTY).

#### Pair Programming

Pair Programming relates to collaborating (programming) on a project with a human partner. You initially team up with someone, it could be your friend or colleague, and develop the same codebase on a single machine but this time, Hey is meant to be there for the rescue. You can easily develop the codebase solo with the help of this AI tool.

### Installation

This section includes steps you need to take in order to install Hey on your machine.

**Note:** This quick tutorial is designed for Hey version 0.1.0 and this version is *not stable* on Windows machines yet. It's highly recommended to use Hey on Unix-like operating systems like Linux distros or MacOS.

#### Sign up on MindsDB

First thing first, you need a free MindsDB account. Sign up at [https://cloud.mindsdb.com](https://cloud.mindsdb.com/) and keep your credentials (email and password) safe. We'll need them later on.

#### Prepare your GPT model

Once you're logged into your account, open up the editor by heading to [https://cloud.mindsdb.com/editor](https://cloud.mindsdb.com/editor). Now, it's time to prepare your desired version of the ChatGPT model by running the following SQL query.

```sql
CREATE MODEL mindsdb.gpt_model
PREDICT response
USING
engine = 'openai',
model_name = 'gpt-4', -- you can also use 'text-davinci-003' or 'gpt-3.5-turbo'
prompt_template = 'respond to {{text}} by {{author_username}} and act like a pair programming partner.';
```

You can change your `model_name` to other GPT versions as well.

Once you execute the query, you see the following result moments later meaning your `gpt_model` table is ready to use.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682495562826/e9e3d9a3-fa95-435e-8049-0633e683cbab.png align="center")

At this point, we're almost done with the MindsDB dashboard. Let's get Hey installed on our system.

* Check [this](https://docs.mindsdb.com/sql/tutorials/twitter-chatbot#1-create-a-gpt-4-model) quick tutorial for more details and options about creating a GPT model on MindsDB.
    

#### Install Hey

Make sure you have `python>=3.6` and `pip` installed on your computer. Run the following command and it'll install Hey on your system.

```plaintext
$ pip install hey-mindsdb
```

**Optional:** If you can't download from PyPI servers by any chance, you can try GitHub servers via `git`.

```plaintext
$ pip install git+https://github.com/lnxpy/hey.git
```

Just to make sure the installation process was successful, print out Hey's version number as follows.

```plaintext
$ hey --version
  _  _          _
 | || |___ _  _| |
 | __ / -_| || |_|
 |_||_\___|\_, (_)
           |__/ --> v0.1.0
```

#### Authentication and configuration

Create a `MINDSDB_EMAIL_ADDRESS` environment variable filled with your MindsDB account email address. The following command does the trick for you. Just replace `<EMAIL>` with your actual email address.

```plaintext
$ echo "export MINDSDB_EMAIL_ADDRESS=<EMAIL>" >> ~/.bashrc
```

If you're using Zshell (ZSH), run the following command instead.

```plaintext
$ echo "export MINDSDB_EMAIL_ADDRESS=<EMAIL>" >> ~/.zshrc
```

Run `hey --set-password` followed by your MindsDB account password.

```plaintext
$ hey --set-password <PASSWORD>
Password successfully set for your@email.com!
```

Now, you're all good to go.

### Usage

Simply call your friend by typing `hey` followed by your question. You can start by asking simple programming questions about concepts as I've done here.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682429755067/764e76d4-6157-451e-bb10-36a285109037.png align="center")

This time, I ask Hey to help me add proper annotations to my Python function which exists in a file called `code.py`.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682430538130/77b7df21-9588-45b3-acf9-33365eb8b106.png align="center")

This feature (using files' content as input) is not officially supported as you may face issues but that's nice knowing this trick.

Notice that Hey is not returning the full answer. It's because of the limitation over `gpt-4`. You can still prepare your model in different versions as we saw earlier. If you want to re-train your GPT model, make sure to drop `mindsdb.gpt_model` table first.

### Development Process

Well, everything starts with `git init`. So did the whole creation of the world maybe. Just kidding..

Hey uses [mindsdb\_sdk](https://github.com/mindsdb/mindsdb_python_sdk) in order to make connections to the MindsDB cloud dashboard. One of the main goals behind Hey v0.1.0 is to let users get their hands on the MindsDB services by heading through the editor, running some SQL queries, and working with tables and structures.

### Next Steps..

In this section, I'm going to talk about the futuristic ideas and features I have in mind for Hey.

| Features & New Implementations |
| --- |
| Adding function and class as input feature |
| Adding file-as-input feature officially |
| Caching already-answered questions locally |
| Giving ChatGPT permissions to read/write through files |
| No authorization required |

### Tech Stacks

* [Python](https://python.org)
    
* [MindsDB](https://cloud.mindsdb.com) (Infrastructure + SDK)
    
* [PyPI](https://pypi.org)
    

### Useful Links

* [YouTube Introduction Video](https://www.youtube.com/watch?v=fhO34PVa-38&list=LL&index=9)
    
* [GitHub Repository](https://github.com/lnxpy/hey)
    
* [PyPI Page](https://pypi.org/project/hey-mindsdb/)
    

### Special Thanks 🔥

I'm truly happy about the partnership between [Hashnode](https://hashnode.com) and [MindsDB](https://mindsdb.com) that made up this amazing hackathon. Their great services and wholesome support are appreciatable. 🍺