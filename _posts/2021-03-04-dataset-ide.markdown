---
layout: post
title:  "An IDE for Datasets?"
date:   2021-03-04 00:00:00 -0700
categories: tech
---
### Introduction
ML systems. A whole practice that has come out of trying to take these amazing algorithms out of research and bring them to the forefront of core technologies we all use today. ML systems is all about building tools around ML which make it easier to work with and deploy. There's a few different categories that we can put these tools into.

1. Data collection + labelling
2. Data management + storage
3. Scaled training (distributed, on AWS, etc)
4. Experiment management (keep track of models, accuracies, etc)
5. Easy model deployment

The left of the image below is a cool summary of some of the companies in this space (peep Scale).

![ml systems diagram](https://s3.amazonaws.com/basecase.vc/defensible-ml-market-map.png)

### Intro to Data Management for Computer Vision
I'm super interested in the data management + storage part, and it's what I'll talk about in this post. I think I had a different post on a related topic but now I'm less of a noob since I've been super into all of this stuff for the past month and a half now. Also, disclaimer: I'll be mostly talking about all of this in the frame of computer vision.

The big problem ML teams experience with data isn't necessarily the ability to collect a lot of it. It is rather the ability to take all that collected data, and understand what's important, what's not, and where bias may exist. After all, the model is directly learning from the data and any bias or uneven spread will be learned by the model as the truth. This is why finding bias within data is important.

Now, are there tools that help us solve this problem? Well, yes and no. Most ML teams tend to calculate many statistics about their data to make sure that they are balanced across various types of metadata (class, timestamp, etc). However, the more complicated the data gets (especially with many images), the easier it is to miss bias that exists in non-metadata form. For example, what are the general colors of the image? How is the lighting like? Are there always exactly 5 cars there? What type of camera took the picture? This is why they then try to visualize their data in an [embedding space][embeddings]. An embedding space is essentially a higher dimensional space that is calculated by running images a few layers through some model. In reference to CNNs, this gives you a representation that the rest of the network is going to use to decide on some sort of classification, detection, etc. Algorithms like [T-SNE][tsne] help us take that embedding and bring it down to a lower dimensional space we're able to then view and explore.

So, I've now named two main things: dataset statistics/summarization and embedding space view. These two things should be something every ML team does when working with image data but most of the time they tend to move forward with one or none. What's the main reason for this? Well, even though at face value these two things are pretty easy to write custom scripts for, those scripts need to be maintained to work with small new variations to the data and also need to be more specific based on use-case (types of scores used to evaluate spread, what's relevant). They also aren't always optimized or the easiest to open up and use (because the main job of an ML team is to build model, not to build tooling). Companies like Google, Facebook, Apple, and self-driving car companies like Cruise, Tesla, Waymo, etc all have built redundant tooling out of their needs.

### Current Tools and Their Problems
The closest thing to what I've described above is [Aquarium][aquarium]. Aquarium offers a webgui for exploring the samples in a dataset while also being able to see various statistics about it along with a nice embedding view. This enables ML teams to select parts of their dataset where they see issues (based on misclassifications, high concentrations of similar images, etc). They also have a pretty intuitive GUI with some nice settings.

But, why might a platform like this be limited? Well, I guess a good way to think about this is through the lens of IDEs we use to write code. There's Atom, PyCharm, VSCode, Sublime, Vim, etc. All great options for Python and many other languages. They come will nice plugins and a place to write and compile code. What if we frame these data management platforms in the same sense we've done for code? After all, we are talking about a tool to build good datasets from mounds of data that have been collected. In an IDE for code, I'm in control of what code is written, when I want to compile it, custom unit tests, and other plugins based on my specific use case. It all changes based on what I want. However, with something like Aquarium, you are limited to the set of tools Aquarium has built to be available. You can only view a specific set of statistics, you can only filter or select in ways the Aquarium GUI defines and allows. You can't evaluate model performance on something as custom as detecting transforming many camera views into a birds-eye view and the metrics related to that, for example.

### Building On Top of Current Tools
This is why my take on data management tools is a little different than what we see exists today with Aquarium or [Scale Nucleus][nucleus]. I think that there should be a platform that allows the exploration of data in embedding spaces, as well as a view to understand various statistics, histograms about the spread of the data. However, I think there should be two main changes to what is being built right now.

1. We should build a platform catered to specific modes of data (i.e. images with computer vision). There are so many processes that have to do with images and not other forms of data like text or sound. This includes for example, things like mean subtraction, blurring, edge enhancing, contour detection, specific data augmentation, etc. All possible things we might want to do before sending the data through a model. There are also more specific forms of images we may input (birds-eye view, selfie, professional camera, RAW, fish-eye). There's all these small things we can build features around to make the life of someone who works with this data easier. For example, why not offer automated ways to [rectify stereo pairs, or undistort a set of images based on camera parameters][https://github.com/ethz-asl/image_undistort]? If we're able to build a tool that uploads raw data at which point it can all be processed and analyzed here, we've built the ideal tool.

2. Engineers like custom plugins and tools. They like to write code. Give them what they want. Implement specific ways engineers can programatically specify certain splices or filters to a set of data, specific comparators to sort the data in a specific manner or to cluster into gorups. We could also build the ability to programatically specify specific [augmentations][https://github.com/aleju/imgaug] and pre-processing to the data. These are all things that become endless in options when applied in the real world. The platform should thus not constrain this need, it should embrace it.

While my thoughts may not be perfect here, I genuinly believe that these are a few of the things we need in order to build the ideal tool for computer vision/ML engineers. How cool would it be if I didn't have to download my data locally anywhere in order to analyze it and curate the perfect dataset to train my model on. It would be crazy if it was a matter of a few different types of pre-written inspections and clicks at which point it was ready and packaged for training. Right now, tools exists but they're all fragmented and separate. Maybe this is starting to sound like Palantir since they build tools that make it easier for humans to make decisions on unorganized data coming from many sources. But, I think that whoever builds this tool for ML engineers will have solved a great problem. One that hasn't yet been solved.

[nucleus]: https://scale.com/nucleus
[aquarium]: https://www.aquariumlearning.com/
[tsne]: https://distill.pub/2016/misread-tsne/
[embeddings]: https://cs.stanford.edu/people/karpathy/cnnembed/
[undistort]: https://github.com/ethz-asl/image_undistort