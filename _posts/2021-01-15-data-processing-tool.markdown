---
layout: post
title:  "Formatting Data is Hard"
date:   2021-01-15 00:00:00 -0700
categories: tech
---

I'm in Hawaii right now and I woke up early so I decided to write this.

There are so many tools that are making the development of ML models easier. This starts from the data collection step in which there are services that can both help with the collection and the labelling of data (Appen, Scale, and Labelbox). Tools like PyTorch and TensorFlow then make it easy for us to both train and deploy our ML models. However, my two main observations in painpoints come in the data processing step as well as the model deployment step.

I want to talk more about the data processing step in this post so I'll describe the model deployment issue quickly. When deploying models, there are many situations when we don't want to also deploy the models in Python due to the slow runtime. For this reason, we require an ML/data engineer to take the trained model file and write separate inference code in PyTorch or TensorFlow which can be run in C++ but are harder to write and less experimentable in a quick and dirty way. It would be interesting to create a tool here.

But, the main issue is the data processing step. What this step entails is taking the labelled data and formatting it in the right way to train the model. For example, with image data we tend to have to do things like batch resizing (via some interpolation) so it fits the models input dimensions. Most data engineers just resize their input image and save the interpolated version on disk to then access. They then also have to save variations based on the augmentations they decide to perform and what ablation study they're running if there are different formats they're trying, etc. This stays the same with text data or any other data where similar/parallel operations tend to need to be performed. It just gets too messy too quickly.

I'm thinking of a tool that makes the ability to use a generator to pass data in through batches easy. It could be an API that has access to a base dataset that has been uploaded to some S3 bucket. Within the online tool, you then have the ability to not only organize all your data (view it, query through it, etc) but also add things like augmentations, specific subsets, etc which can then be called via a generator which has a single line of code to an Python API calling for the next batch of data from the server.

I don't see any tools trying to do this and I think it would be an important problem to solve that saves times for all them ML engineers out there.