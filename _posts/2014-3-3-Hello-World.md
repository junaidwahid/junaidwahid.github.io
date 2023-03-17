---
layout: post
title: ''
published: true
---

It seems that the word "ChatGpt" is on everyone's lips these days, no matter where you go or who you talk to. But before we get carried away with all the hype, let's take a closer look at some of the challenges that come with these fancy language models. Don't worry if none of this makes sense at first - I'll be your trusty navigator and guide you through the murky waters of language model problems

In this article, we will begin by providing a basic understanding of few-shot learning, and explore some of the challenges that arise in this domain. It is important to note that a prerequisite for reading this article is a fundamental understanding of machine learning concepts and a willingness to explore new ideas.

By the end of this article, readers will have a deeper understanding of the unique challenges posed by few-shot learning, and the potential applications of this technology. We hope this article will serve as a useful guide for those interested in exploring this fascinating field.

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

![fewshot](https://raw.githubusercontent.com/junaidwahid/junaidwahid.github.io/master/_posts/fewshot.png)


### True Few shot learning
Now that we've covered the basics of language models, let's dive into what true few-shot learning really means(yes there is difference between few shot learning and "true" few shot learning"). Previous research has classified few-shot learning into three different categories (see Table 3). The first is the Data-Rich setting, which is essentially a supervised learning pipeline where we have access to a large amount of training and validation examples. The second is the Multi-Distribution setting, where we have access to a small dataset of many similar distributions. The last category is the Tuned Few-shot setting, where we have access to a large validation set that we can use to fine-tune our task.

But, wait a minute... if we go back to our earlier definition of few-shot learning, can we really call these methods "few-shot learning"? The answer is no. That's where true few-shot learning comes in! We don't need many similar small datasets from other distributions, nor do we need a large training or validation set. All we need are just a few examples to perform the desired task!
![true](https://raw.githubusercontent.com/junaidwahid/junaidwahid.github.io/master/_posts/true.png)


You might be wondering why I haven't started discussing the problems of few-shot learning yet. Don't worry, I'm not avoiding the topic. Similar to the phrase "Attention is all you need", I would like to say that "More reading is what you need right now".

Before we delve into the issues, let's first define few-shot learning and the method we use to choose models. To do this, we divide our dataset into a training set and a validation set. We use the training set to train an algorithm called "A" while considering random factors like network initialization or the order of training examples. We refer to these factors as "R". In order to achieve better performance, we aim for the validation loss to be low, which is the expected mean loss on multiple folds, similar to k-fold.

![mode selection](https://raw.githubusercontent.com/junaidwahid/junaidwahid.github.io/master/_posts/model_selection.png)

There are two ways to perform few-shot learning: cross-validation and minimum description length. The former is well-known, so I won't go into detail, but the latter is also commonly used for model selection despite being less well-known.

Minimum Description Length, or MDL, is a criterion used for model selection that balances the model's complexity with its ability to fit the data. The aim of MDL is to find the simplest model that can accurately represent the data.

When using MDL, we take an expectation over the possible values of "k", which determines how the dataset is split between the training and validation sets. Here's a pseudo code to understand MDL better:

	1. Divide the dataset into "k" folds.
	2. Use "k"th fold for testing and the rest for training.
	3. Repeat the process for all "k".

In simpler terms, we want to encode information using as few bits as possible. Therefore, models that are more compressible generally lead to better generalization and, in turn, better models.

## Problems with Few Shot Learning

Although models like GPT-3 and other big language models are impressive, every good thing comes with a hidden cost. Few-shot learning seems like the ultimate solution to the problem of limited data in everyday machine learning pipelines, but it has underlying issues that need to be reviewed. Recently, a paper by Nitin published in NeuralIPS has explored the problems of few-shot learning. I highly encourage you to read that paper after this blog to gain a deeper understanding. In the upcoming sections, we will discuss the problems mentioned in the paper and how much they can affect the model's performance. The meme below provides a summary of what we will be discussing!

![problems](https://raw.githubusercontent.com/junaidwahid/junaidwahid.github.io/master/_posts/chopper.png)


### 1. How well does prompt selection do in true few-shot learning?

When it comes to training language models with limited data, prompt selection is a crucial factor for achieving good performance. The right prompt can provide the model with more context and help it generate better results. However, in the case of true few-shot learning, where the amount of data is severely limited, prompt selection becomes even more important.

In the mentioned paper, researchers have explored different techniques to evaluate the effectiveness of prompt selection. They found that, on average, test accuracy of prompts chosen by cross-validation (CV) and minimum description length (MDL) were very far from the best prompt.  Even when comparing the results of a selected prompt to the average of some random prompts, the accuracy was not significant in most cases. This pattern was consistent across all model sizes.

They further studied the accuray of choosing of best prompt. The results were not different and they faced the same fate and number of times models chose the best was significantly low. 

**What does this mean?** First, we should not expect to always get the best prompt or even a prompt that is close to its performance. Second, these results suggest that previous studies may have overestimated the performance of few-shot learning.


### 2. How reliably does prompt selection improve over the average prompt?
One key question that arises is whether it is possible to improve performance with high probability, even if the expected improvement from prompt selection is small. This question is essential because avoiding the selection of the worst prompt, which can result in a low-performance model, is critical to achieving better results. While previous experiment has shown that the expectation of getting better performance over average random prompts is not significant but avoiding the selection of the worst prompt can still result in an improvement. In other words, if we can identify and eliminate the worst-performing prompts, we can increase the likelihood of obtaining a better model performance.

The experiment in the paper revealed that CV/MDL-chosen prompts showed high variance in test accuracy relative to the average prompt, and for most model sizes, the chance of improving over the average, randomly-chosen prompt was only 56% for CV and 55% for MDL. The authors noted that the performance of prompt selection formed a long-tailed distribution, with a 27% chance that prompt selection would cause an accuracy drop of 13% for all model sizes and CV/MDL alike. Additionally, the tails grew heavier as model size increased, indicating that the ability to reliably choose good prompts degraded as models grew bigger and generalized better. The surprising finding was dropping of the model accuracy by 40% with 5% probability. These number disclosed the earlier overestimation in the area of few shot learning thats has been relied blindly over the years with little focus on its performance on actual true few shot learning setting.

**What could be the possible explanation for these results?** One possible explanation for this trend is that larger models have the capacity to draw more complex decision boundaries, requiring more examples to estimate the true expected loss on unseen examples. Therefore, scaling validation sets along with model size may be necessary. Overall, the limited average-case gains from prompt selection could not be expected with any reasonable confidence in the true few-shot setting, and this problem would only become worse with larger models.

### 3. Does prompt selection improve with more labeled examples?
One can argue, that may be increasing the number of data examples may increase the performance and that argument makes sense as it is evident even in case of supervised learning. To test the argument,the paper replicated the experiment with different amount of data in increasing order and examined how well prompt selection methods performs. They also tested whether increasing the amount of compute (i.e., the amount of computational resources used) would improve prompt selection performance.

**So, does it increase the performance?** Surprisingly, even with more labeled examples, prompt selection methods did not consistently perform better than simply choosing examples based on few examples. Additionally, increasing the amount of compute used to estimate the performance of different prompts did not improve the accuracy of prompt selection beyond a certain point.These findings are surprising because prompt design has been thought to be most promising in the true few-shot setting, where there is very little labeled data available. However, these results suggest that prompt selection is still difficult even with more labeled data, greatly undermining the potential value of prompts in the true few-shot setting.

### 3. To what extent are chosen prompts specific to the model?

When it comes to language modeling tasks, one of the most critical things is choosing the right prompts. But how do we know if the prompts we choose are specific to the model we're using, or if they can be used for other models too? That's was one the experiment of the paper.

The researchers used something called prompt transfer to test whether the prompts chosen using cross-validation/minimum description length (CV/MDL) techniques were tailored to specific models or not. Prompt transfer involves using a prompt chosen for one model to make predictions using another model. The accuracy of these predictions is then evaluated to determine whether the prompts are working well or not.

**So what did the study find?** Well, it turns out that prompts chosen based on test accuracy tend to work well for models of similar sizes. However, when using CV and MDL-selected prompts, things can get a little trickier. In fact, the researchers found that these prompts tend to underperform when compared to the best prompts and don't consistently improve accuracy across different tasks and model sizes.

**What does this mean for practitioners?** Essentially, it suggests that prompts selected using CV/MDL techniques may not be tailored to individual models, and may not be the best prompts to use for NLP tasks. Instead, it's important to choose prompts that are specifically designed for the model you're using, or to consider other techniques for prompt selection. By doing so, we can ensure that our  models are as accurate and effective as possible.

### 4. Is prompt selection challenging on other tasks?

Choosing the right prompts is crucial for language modeling tasks, but is it equally challenging for all tasks? The mentioned paper also ought to answer this question by investigating the effectiveness of prompt selection on three different NLP tasks: Recognizing Textual Entailment (RTE), CommitmentBank (CB), and Word-in-Context (WiC). The authors used prompts chosen by cross-validation (CV), minimum description length (MDL), and test accuracy to evaluate the accuracy of the models.

**What did the study find about the effectiveness of prompt selection?** The study found that the results were similar to their findings on the LAMA task, where CV/MDL-chosen prompts tended to obtain lower average accuracy than those chosen based on test accuracy. This trend was consistent across all tasks and model sizes, even when selecting fewer prompts. Additionally, the accuracy of CV/MDL-chosen prompts varied widely across tasks and model sizes, often resulting in worse-than-average prompts. To further examine the variance in chosen prompt accuracy, the authors calculated the chance that prompt selection would obtain various accuracy gains over the average prompt. They found that the accuracy gains were highly dispersed, often negative, and not consistently achieved. Overall, the study concludes that prompt selection is challenging in general, and the earlier findings on LAMA tasks apply to other kinds of tasks as well.

### 5. True Few-Shot Hyperparameter Selection
**Are you ready for a surprising fact?** Even when you choose the best hyperparameters for a model, it may not perform well on tasks that require few-shot learning. In other words, even the best model may not give you the results you want when you have limited data to train it on. This is the conclusion reached by the authors of a recent paper that focused on ADAPET, a few-shot model that was considered one of the top-performing models according to SuperGLUE, a standard benchmark in natural language processing (NLP).

The study evaluated the impact of using validation examples to choose two hyperparameters: the early stopping checkpoint and fraction of words masked for the masked LM objective. The results showed that across all SuperGLUE tasks, cross-validation/minimum description length (CV/MDL) hyperparameter selection performed similarly or worse than average hyperparameters randomly chosen, and several points worse than the best hyperparameters. In the true few-shot setting, the average SuperGLUE performance of ADAPET dropped below that of earlier methods, highlighting how the use of validation examples can give the false appearance of progress in few-shot learning.

**So, what does this mean?** While prompt selection has been shown to be challenging in low data regimes, this study demonstrates that model selection can also be just as challenging. Despite the use of the best hyperparameters, a model may not perform as expected in few-shot learning scenarios. These findings shed light on the need for further research and development in this field to improve few-shot learning performance in the future.

## Takeaways

Here are some takeaways from this blog:

1.Few-shot learning has underlying issues that need to be reviewed, as highlighted in a recent paper by Nitin.

2.Prompt selection is crucial for achieving good performance when training language models with limited data.

3.Researchers found that choosing the best prompt is challenging and previous studies may have overestimated the performance of few-shot learning.

4.Prompt selection showed high variance in test accuracy relative to the average prompt, and the ability to reliably choose good prompts degraded as models grew bigger and generalized better.

5.Prompt selection is still difficult even with more labeled data, greatly undermining the potential value of prompts in the true few-shot setting.

6.The prompts are model-specific, and prompt selection methods did not perform well across models.

7.The findings suggest that prompt selection is a challenging problem that needs more attention and research to improve its performance.
