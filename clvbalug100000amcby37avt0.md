---
title: "Next-Gen Databases: AI meets SQL"
datePublished: Mon Apr 22 2024 18:30:41 GMT+0000 (Coordinated Universal Time)
cuid: clvbalug100000amcby37avt0
slug: next-gen-databases-ai-meets-sql
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1710439622304/5868de87-7a18-447a-87f4-bcaf7921c1fd.png
tags: ai, artificial-intelligence, machine-learning, databases, chatgpt, vector-database

---

As developers, we have experience with various database management systems (DBMS), including SQL and NoSQL. The database platforms we work with can range from advanced ones like SQL Server and PostgreSQL to simpler options like SQLite, which can be a smart choice in certain situations.

By the term "advanced," I am referring to the features and functionalities of the database that users can access, like setting up scheduled jobs, auto-indexing, and creating functions/macros and procedures when needed.

We have entered a new era where databases are no longer just for storing data. Developers are utilizing AI-friendly programming languages like Python to build database engines. This method has enabled them to merge AI models with DBMSs.

This article explains some basic concepts about the revolution happening in databases. We won't delve into very deep AI concepts. Providing a brief overview of each topic should suffice to lead us to the main subject: integrating AI and databases, the process involved, and the benefits companies and teams are reaping from it.

This article is based on my research on related concepts, a few months of working as an open-source contributor at MindsDB, and the paper [EVA: A Symbolic Approach to Accelerating Exploratory Video Analytics with Materialized Views](https://dl.acm.org/doi/pdf/10.1145/3514221.3526142).

## Supervised Learning

In every real-world machine learning scenario, we design a system using a data set. We always have a data source available to us. This data might come from an external stream (like CCTVs, real-time API calls, or pub-sub systems) or be stored in a local database within the same infrastructure.b

Normally, in an AI project, especially in machine learning, we go through three phases. We begin with gathering the necessary data. After accumulating a sufficient amount of data for our model, we proceed to the first phase, which is pre-processing.

> **Pre-processing:** This step initially covers all the necessary operations that need to be done on our essential data to reduce the outliers, scale them, replace the missing records, data correction, and so on.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1712541572956/13ab3cff-3e8b-4953-876c-0863a8ea9013.png align="center")

Now that we have our data prepared, we would typically proceed to the next phase and train a model using this data. When we talk about **"training a model based on data"**, we are referring to developing a mathematical function that takes inputs and provides an output.

$$Predictor(x_1, x_2, x_3,\cdots) = y$$

As a developer, consider this explanation as a function named `predict` that takes a value and returns the corresponding value from a dictionary for now.

```python
data = {
    10: 3_000,
    15: 5_000,
    20: 10_000,
    25: 15_000,
    30: 20_000
}

def predict(x: int) -> int:
    return data[x]
```

There is a difference between a mathematical function and a programming function. A function in mathematics provides a result (whether accurate or not) for any input, while in programming, a function might raise an exception during runtime or return nothing (`None` or `null)`.

We'll see various results if we call this function with different inputs.

```python
predict(20) # 10_000
predict(25) # 15_000
predict(22) # ERROR <KeyError>
```

Notice how we got an error attempting to call the function with a value that's missing from the `data` dictionary. The goal is to implement a functionality for the `predict()` function to predict any value as the key `x`. Following an approach to convert this programming function works just like a mathematical one. If a 20-square-foot room costs $10,000, then probably a 22-square-foot should cost $11,000.

<details data-node-type="hn-details-summary"><summary>How is this Predictor function made?!</summary><div data-type="detailsContent">The data we stored can assist us in this phase. Using algorithms like <strong>Regression</strong>, we can create the most accurate <strong>y</strong> expression. This is achieved by minimizing errors and developing a function that encompasses as many data points as possible.</div></details>

So far, we've seen a brief preview of how supervised Machine Learning models work. This method is used in lots of forecasting solutions in AI databases.

In the example that we practiced, we were dealing with pure numeric data. In some cases, we might be working with media-typed data such as photos, video tapes, audio, etc.

How does a machine distinguish an apple from a banana? How does a machine classify SUVs out of a road full of taxis? This is where the importance of databases shines and comes in handy in terms of storing vectors and classification.

## Integration with Databases

The entire process of reading, restructuring, and purifying the data used to occur on our machine, requiring us to write Python code for these tasks. We needed to assign a table column for our vectors, store the precise parameter values in variables, and so forth. This process could be tedious, particularly in production from a DevOps perspective. That's when we asked: Why not do it in databases?!

In most SQL databases, we have a wide range of options for creating custom macros, functions, and reusable SQL code snippets. That's where we can put our training steps; scientists thought!

Of course, it will make AI more accessible to developers and those interested in integrating AI into their products. However, there is another important reason behind this. In the old classic way, we had to establish the connection between our models and datasets by writing codes. This has changed now, as our models reside within our database tables.

This game-changing solution has two major benefits.

* Easy access to AI models from anywhere.
    
* Models can reach out to data columns even faster.
    

With that said, there is also a possibility to use a model based on hand-picket data from the entire dataset using SQL commands and clauses. This feature enables you to quickly evaluate your model's accuracy and tune it in the finest possible way.

## How Fast Are They

Technically, when we're talking about numbers and our data is also in numerical form, training a model with this kind of dataset shouldn't be difficult. However, we live in a world where data is diverse. Many things can't be quantified. Can you measure how kind your parents are with a number? Can you express your current mood with a numeric value?

Well, in the sense of numerical values, it's so easy to find a value among all the data. A quick indexing would do the job for you, but how can you find a movie scene among all the movies produced by the industries?!

Imagine you have a table full of photos. Records contain hard-coded URLs that redirect to photos. How can you find the photos that contain an apple in the scene?

We use a method called **Vectorizing** to create a column that contains the vectorized form of each photo.

Well, mathematically, each photo is a matrice and each cell of that matrice is a vector showcasing the RGB values of that point.

<details data-node-type="hn-details-summary"><summary>Why Vectorizing?!</summary><div data-type="detailsContent">That's a good question. That's because machines don't understand any other data like how we do except numbers. Machines try to find patterns between numbers.</div></details>

Any type of data can be transformed into numbers (vectors). Your voice consists of frequency pulses, often represented by decibels for loudness and hertz for frequency wave height. Videos are composed of frames, with each frame being a matrix. Texts can also be represented as numbers. The real question is, where do we store the numeric form of our data?!

We used to define a data structure for this, but now, with the assistance of AI databases, we store everything our models require directly within the database that runs our model.

## Classification

To find the photos that represent the figure of an apple, we can go on with two solutions.

* Parametrizing
    
* Vectorizing
    

**Parametrizing:** It means we have to tag each photo based on different attributes like color, size, weight, shape, etc, and do the queries based on these values.

**Vectorizing:** It helps you to define those patterns that we talked about. Their accuracy mainly depends on the quality of the photo.

### Conclusion

Hopefully, this article has provided you with a brief overview of the functioning of AI databases, focusing on two key aspects: Parametrizing and Vectorizing.

In essence, understanding the roles of parametrizing and vectorizing is crucial in comprehending how AI databases operate and optimize data processing tasks.