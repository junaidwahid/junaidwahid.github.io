---
layout: post
title: You're up and running!
published: true
---

It seems that the word "ChatGpt" is on everyone's lips these days, no matter where you go or who you talk to. But before we get carried away with all the hype, let's take a closer look at some of the challenges that come with these fancy language models. Don't worry if none of this makes sense at first - I'll be your trusty navigator and guide you through the murky waters of machine learning.

Today, we will start a journey towards a difficult type of learning called "few-shot learning". It's like an island that most people avoid because it's very challenging. However, I will lead the way and guide us through the obstacles.

### Few Shot learning
Traditional machine learning models often require large amounts of labeled data to achieve high performance on a given task, such as sentiment analysis or named entity recognition. However, collecting such large amounts of labeled data can be difficult or even impossible, especially for low-resource languages or domains.

This is where few-shot learning comes into play. Few-shot learning is a machine learning paradigm that aims to train models that can learn from just a few examples, hence the name "few-shot". The goal is to enable models to perform various tasks with only a small amount of labeled data, such as sentiment analysis with only a few examples of positive and negative reviews.

Let's look at some examples to understand the concept better. Imagine you want to train a model to generate responses to customer support inquiries. In traditional machine learning, you would need thousands of labeled examples of customer support conversations to train the model. However, in few-shot learning, you can train the model on a few examples of different types of customer support inquiries, and then test it on new types of inquiries that it hasn't seen before.

In more technical terms, few-shot learning involves training a model on a small number of labeled examples (or "shots") of each task or class. The model is then tested on a set of novel tasks or classes, each with only a few examples, to evaluate its ability to generalize.

### Language models and Prompt engineering
Have you ever talked to a computer? You might be thinking, "Wait, computers can't talk, can they?" But what if I told you that there are machines out there that can communicate with humans just like we do with each other? These machines are called language models, and they are taking the world by storm and one of the example is indeed ChatGPT.

Language models are trained on vast amounts of text data, such as books, articles, and websites. They learn the rules of grammar, syntax, and semantics from this data and use it to generate human-like text. It's like teaching a machine how to speak our language by exposing it to millions of examples of how we use words and sentences.

One of the most famous language models out there is called GPT-3. It's like a super-smart computer that can write essays, answer questions, and even write code. But here's the catch: it needs to be told what to write about. That's where prompt engineering comes in.

Prompt engineering is like giving GPT-3 a topic to write about and some examples to learn from. For example, if we want GPT-3 to write a recipe for chocolate cake, we might give it some examples of other chocolate cake recipes, along with some keywords and phrases like "mix the flour and sugar" or "bake at 350 degrees." GPT-3 can then use this information to generate its own unique recipe for chocolate cake.

Here is one example of few shot learning, where we have given task description, some examples and finally a prompt the model needs to complete.

![Few shot learning]({{site.baseurl}}/_posts/fewshot.png)


### True Few shot learning
Now that we've covered the basics of language models, let's dive into what true few-shot learning really means. Previous research has classified few-shot learning into three different categories (see Table 3). The first is the Data-Rich setting, which is essentially a supervised learning pipeline where we have access to a large amount of training and validation examples. The second is the Multi-Distribution setting, where we have access to a small dataset of many similar distributions. The last category is the Tuned Few-shot setting, where we have access to a large validation set that we can use to fine-tune our task.

But, wait a minute... if we go back to our earlier definition of few-shot learning, can we really call these methods "few-shot learning"? The answer is no. That's where true few-shot learning comes in! We don't need many similar small datasets from other distributions, nor do we need a large training or validation set. All we need are just a few examples to perform your desired task, my friend!
![true]({{site.baseurl}}/_posts/true.png)


Well you might be thinking, that you came here find out about problems few shot learning and I am just strecthing the topic without going discussion about the problem. Well, Similar to “Attention is all you need” ,I would just say “More readind is what you need right now 🙂” .
Before discussing the problems, we have to formalize few shot learning and the method to select models . Lets first describe how we actually formaizlie the model selection in the few shot learning setting. As usual , we split out dataset into training and validation set. We used our training dataset to train a Algorithm “A”  and we also consider other random factors like network initialization or order of training example, we covered these factors under the umbrella of random factors “R”. To achieve generalization or better performance, we want the validation loss to be which is a expecte(mean) loss on many folds, similarly to k-fold. 

![mode selection ]({{site.baseurl}}/_posts/model_selection.png)

We can perform this experiment with two model selection criteria: cross validation and minimum description length. The former is known to many people so i will spare the detail while later is commonly used for model selection but still less known. Minimum Description length, MDL is a criterion used for model selection based on the trade-off between the model's complexity and its ability to fit the data. The goal of MDL is to find the simplest model that can effectively represent the data.
In the MDL formula you provided, the expectation is taken over the possible values of k, which determines the split between the training and validation sets.Lets understand the MDL using this pseudo code.
Divide the dataset into k folds.
Used 1-k for training and kth fold for testing
Repeat the process for all k

In order words, we want to encode the information with less number of bits as possible so more compress models actually leads to better generalization and hence a better model.






