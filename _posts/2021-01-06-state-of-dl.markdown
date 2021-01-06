---
layout: post
title:  "State of Deep Learning Workflows"
date:   2021-01-06 00:00:00 -0700
categories: doing
---

Below is a breakdown of the current gaps or inefficiencies in the workflow for deep learning.

Deep learning is a field that has been in great focus for the last 5-7 years now. People are trying to make the tools we use to build deep learning models easier to use (just so you don't need a PhD to actually build something useful with them). There's already been so much progress here with accessible libraries like Keras along with new tools for getting labelled data, etc.

### Workflow Breakdown

I can break down some of the workflow of building ml/deep learning models into the following steps:

<ul>
<li>Understanding the task</li>
<li>Training Data
	<ul>
		<li>Collect + Label</li>
		<li>Create environment + simulate</li>
	</ul>
</li>
<li>Develop model pipeline/architecture</li>
<li>Format data to be fed in properly (preprocessing)</li>
<li>Train model
	<ul>
		<li>Remote Cluster</li>
		<li>Google Cloud/AWS Instance</li>
		<li>Local Machine</li>
		<li>Other Options</li>
	</ul>
</li>
<li>Evaluate model</li>
<li>Deploy model</li>
<li>Monitor failures, then report and fix (edge cases)</li>
</ul>

Training data steps are mostly solved by companies like Scale AI, Appen, Labelbox (only for real-world data though). If we're looking to build realistic simulated environments, there's still a gap to fill (though there are companies like Applied Intuition which focus specifically on self-driving cars).

Building the model has been made easy with PyTorch, TensorFlow, Keras, and other libraries + repos. There may be some gap to fill here to make a lot of code people write in their research projects cleaner, more accesible and easier to deploy in production since most of the time, code from research projects is really messy or not easily adapatable.

Formatting data has been in my experience something that takes so much time to do. Especially when working with multiple data streams (i.e. rgb image, segmentation map, depth map) and trying to combine them all, it becomes really messy to get them in the right format via some batch operation we can perform and then save on disk. There's definitely some though I need to put here in terms of how we can improve current workflows.

Training the model has been made relatively easy with the use of things like Docker along with newer companies like Anyscale which allow for some distributed operation. I don't have deep enough knowledge of this part to assess the current state of tools here.

Evaluating the model can be done right now but there's no tool that makes it easy to organize all results and easily view them over specific pieces of data you want to view them on. Scale AI is building a tool called Nucleus that tries to make this easier though.

Deploying models is still pretty hard. Depending on the use case, you want to do this on-edge, in the cloud via an instance, or in the cloud via some serverless backend. A good amount of the time, it's important that the model trained with some Python package is then easily useable in C++ which allows for faster, more efficient runtimes per inference when deployed. From my knowledge, this is still somewhat tough to do and requires a lot of custom optimization.

Monitoring a model in production is probably to biggest thing we can solve in this workflow. Companies like Tesla have probably perfected this with the pipeline they use for Autopilot but there isn't really any open-source way to effectively monitor when a model fails and then report + iterate on those cases of data.

### Painpoints

There's a few different painpoints we can observe with the overall workflow that exists for deep learning above. Only thing I left out is possible solutions which is the hard part.