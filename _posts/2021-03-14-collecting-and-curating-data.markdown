---
layout: post
title:  "Going from Collected Data to Curated Datasets"
date:   2021-03-14 00:00:00 -0700
categories: tech
---
For every ML project that is worked on in industry, there exists the process of going from collected data to curated datasets. We will go over the current workflow for doing this and problems that exist within it. We'll take the example of Zillow possibly wanting to automatically label the part of the house each of the listing images are from on their site. My thoughts below have been compiled after talking to 50+ ML engineers and researchers in industry.

### Current Workflow
##### 1. Figure out how you're getting the data
If you're a drone company or a self-driving car company, this might be going out to take the vehicle for a spin either in the real-world or in simulation. But, if you're a company like Zillow, you'll have access to all these images in a database. The team first begins by querying their database for a set of listing image samples along with relevant metadata (house address, timestamps, etc). There are 100M+ listings on Zillow with about say ~10 images per listing which amounts to about 1B images. The team however, is looking for a dataset which is probably around ~100K images.

##### 2. Curate the data
Since the team at Zillow is smart, they'll want to diversify their dataset based on a few factors which could include an even distribution of timestamps, housing prices, housing locations, year built, etc. Writing a query for this though is pretty tough because it's over many axes. So, what the team might do is first sample ~10M images randomly into each of multiple buckets of timestamp ranges. Then, the team may look at each bucket and recursively create new buckets for each of these buckets based on say housing prices until they reach a threshold of about ~5M. They do this for all axes and eventually land on a finite set of buckets of about ~500K images each which fall into each combination of the metadata properties. They can then randomly toss out a fraction of the images from each bucket and have a dataset that's curated according to these 5-6 axes. Systems like [Michelangelo][mich] help with this stuff.

##### 3. Augment the data
Though the team went through the due diligence of trying to create an evenly distributed dataset, chances are that they didn't really. This is mainly because even though they curated over ~5 axes, there are probably hundreds of relevant ones across the dataset. Some of these might not even lie directly within the metadata and could be things such as image lighting, camera focal length, average distance from subjects, moving objects in images, etc. All of these things have the ability to bias the dataset in some way. So, what they decide is that they'll try using some augmentation to de-bias the dataset a little more. This could be with things like vertical/horizontal flips and artificially changing the lighting within the images. We now ideally have a dataset which is completely "de-biased" and gives us a good representation of the houses we'll see in the real world or in the future on the site.

##### 4. Pre-process the data
Now, it's the job of the team to figure out the best way to feed these images into the model. Much of the time, it's a matter of simply resizing the image to the fixed dimensions expected by the model and then one-hot encoding the classification labels. However, there are possiblities of trying to do other things like "un-distorting" the images based on camera parameters one may know depending on what phone the image was taken on or purposefully blacking out all non-static objects within the image (people, animals, cars, etc). The motivation of things like this are rooted in the task you're trying to perform and what it depends on.

##### 5. Train on the data
Now you can just send this data off to some AWS instance that loads up a training script and ingests all this data.

##### 6. Diagnose model failures and restart
At this stage, your model probably isn't perfoming well on some subset of your test set. You have to go through these failure cases and figure out why this is. You then either choose to change something about the model architecture, model hyperparameters, or the dataset itself and run a new job.

### Problems with Current Workflow
Now we try to analyze what's wrong with this workflow and list potential problems below.

##### 1. Manual axis picking for data curation
The first red flag one might see is within the "curating" step. The team hand-picked a certain set of axes that they thought might me relevant to the task at hand and tried to balance the data according to these metrics. However, it must be noted that these aren't ever the only axes that matter. Against our intuition, they may even be axes that barely matter to the task for the reason that deep learning models are black boxes that we don't understand.

##### 2. The movement of data
Though it may not be immediately obvious, there is a tedious process of having download the data to even view it as an ML practitioner. This is what allows you to make decisions on which metadata you should use to balance your dataset or to figure out which types of pre-processing and augmentation might help. The first time you do this is in the data curation step where you might download a portion of the dataset to some local work station to view. The next time data moves is when you run the task of recursively bucketing your data to curate on some remote machine because this is presumably a compute intensive task. The next time it moves is when we pre-process the data because we may require specialized GPU hardware to possibly do deep-learning based pre-processing (i.e. removing people from images). We then move it a final time to an AWS bucket which the training script accesses.

##### 3. Augmentation + pre-processing is messy and annoying
Sometimes when dealing with data samples that might contain RGB images along with LiDAR scans, depth maps, bounding boxes, etc, it gets tough to manage. When doing deep-learning based pre-processing, this may happen because you're trying multiple off-the-shelf models on a set of data and seeing which one gives the best pre-processed results. The takeaway here is that augmentation and pre-processing can be annoying both because of how messy it is to manage multiple experiments in pre-processing procedures and because of how long it may take to run on an entire dataset.

##### 4. Diagnosing issues with the model and improving the dataset
These days, model architectures have been standardized by companies like Google, Microsoft, and OpenAI to the point at which it makes no sense to experiment with it yourself. The only real way to improve your model is to figure out how to improve your data. This involves sourcing samples that are similar to our failure cases to include in our next training run or seeing if a pre-processing technique negatively affected the model's performance for some reason.

### Solving the Problems
In my last post, I wrote about an IDE for datasets. I think that some of my unorganized ideas from there are part of the solution but since that post, I've further organized my ideas on solutions and am trying to build some of them out myself. Will keep the blog posted...

[black-box]: https://stats.stackexchange.com/questions/93705/why-are-neural-networks-described-as-black-box-models#:~:text=A%20neural%20network%20is%20a,of%20the%20function%20being%20approximated.&text=Then%20you%20use%20the%20Neural,is%20acceptable%20to%20your%20application.
[mich]: https://eng.uber.com/michelangelo-machine-learning-platform/
