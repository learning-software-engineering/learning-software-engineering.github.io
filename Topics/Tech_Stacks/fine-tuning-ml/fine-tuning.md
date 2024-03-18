# Fine-tuning an ML model in Pytorch tutorial

## Table of Contents
1. [Introduction](#introduction)
2. [Setting Up the Problem](#setting-up-the-problem)
3. [Finding a Pretrained Model](#finding-a-pretrained-model)
4. [Finding a Dataset](#finding-a-dataset)
5. [Setting Up Training](#setting-up-training)
7. [Conclusions](#conclusions)

## Introduction
This tutorial is meant as a brief guide to fine-tuning a pre-trained machine learning model using Pytorch.

This tutorial assumes basic knowledge and familiarity of machine learning basics and PyTorch like what a model is, how training works, and other requisite topics.
If needed, an online PyTorch tutorial is available online at [this link](https://pytorch.org/tutorials/beginner/deep_learning_60min_blitz.html). 
Additionally, if needed, there are various machine learning materials online for self learning, such as [this](https://alexjungaalto.github.io/MLBasicsBook.pdf).

## Setting Up
Suppose there is some task for which machine learning approaches may be effective. 
Before looking into model fine-tuning, however, one must consider the what fine-tuning is and the advantages and disadvantages of model fine-tuning.

Fine-tuning a machine learning model can be described as the process of using a machine learning model that has already been trained on some task and further training that model to a similar task. 
For instance, one could fine-tune a model that has been pretrained on general image recognition tasks and further train it to recognize different breeds of dogs.
This works because a pre trained model that may have been trained to a high accuracy on a large dataset can be thought of a form of feature extraction; the weights of the pre-trained model has likely been trained to recognize various features of the dataset, and using that pre-trained model as a starting set may yield better results than just training a model from scratch.

This may yield several advantages: 
- Fine-tuning leverages the learning other parties have trained the model to recognize, often taking advantage of learning from larger, more optimized datasets.
- Fine-tuning may take significantly less time to train, as the process of fine-tuning often involves 'freezing' most of the weights of the model.
- Fine-tuning a model may be resistant to overfitting to training data, as most of the weights of the model have been 'frozen' at training time.
- Fine-tuning enables models trained on general, large-scoped tasks to be adapted to smaller-scale or similar tasks without starting from scratch.

However, this could come with some downsides.
- Fine-tuning may cause the model to forget previously learned features or tasks if the new task is substantially different from the original task the model was trained on.
- Fine-tuning requires a sufficient amount of data from the target domain to avoid overfitting. In cases of extremely limited data, fine-tuning may not be effective.
- If the pre-trained model is significantly different from the target domain, fine-tuning may not yield significant improvements, and in some cases, it may even degrade performance.
- Because the process of fine tuning often involves 'freezing' most of the weights of the model during the training process, fine-tuning such a model may limit how flexible such a model is during training.

If a user believes that model fine-tuning is the right choice for their particular task, they can get started on finding a dataset and pretrained model pair that fits their task.

## Finding a Pretrained Model

Generally, when finding a pretrained model, a model that 
- Has been trained on a similar dataset/task
- Has achieved high accuracy
- Is accessible
is desired.

A good place to look for pretrained models is [Hugging Face](https://huggingface.co/models).

For example, using the Hugging face Transformers library, it is possible to import a BERT model from Hugging face using the following pieces of code:

![Importing the transformers library](./transformerslib.png)
![Importing a pre trained BERT model](./Screenshot%202024-03-17%20224606.png)

Because different machine learning models and different pretrained models are distributed differently, more work may be needed for each individual task.

## Finding a Dataset

A good place to look for datasets is [Hugging Face](https://huggingface.co/datasets).

When looking for a dataset, find a dataset that is a similar to the task at hand as possible. It is possible to import the dataset directly from hugging face by directly downloading it.

## Setting up Training

Before training, it is important to note that if a GPU is available, using it would speed up training time significantly.
![GPU testing](./Screenshot%202024-03-17%20225750.png)

Fine-tuning involves 'freezing' the weights of the pretrained model. 

![Freezing and Overwriting](./overwrite.png)

The first chunk of code freezes the weights of the entire pretrained model. This is important to preserve feature extraction capabilities from the pretrained model throughout fine tuning.

The second chunk of code creates a PyTorch Module for which to replace the final layer of the pretrained model. This is important to adapt to the new task; the shape of the last layer must be changed to match with the new task. For instance, here, we are training the model to recognize 4 as opposed to 2 classes, so the output of this layer must have size 4. This newly initialized final layer will not have its weights frozen. 

The next chunk of code sets the model's classifier to the new module we have initialized. The name of the last layer of the ML model is entirely arbitrary, so in many cases, instead of model.classifier, one would write model.last_layer or something along those lines.

The last chunk of code sends the model to the GPU for accelerated training and prints details about the model for the purpose of checking the validity and behavior of the code. 

Once this is done, one can train the model as one normally would. 

## Conclusions 

Having learned what model fine-tuning is and its applications, I hope any reader of this can add this useful skill to their arsenal of software engineering/machine learning skills.