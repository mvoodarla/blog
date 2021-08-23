---
layout: post
title:  "The Future of Computer Vision"
date:   2021-08-21 00:00:00 -0700
categories: tech
---

## Introduction

Computer vision has the potential to impact so much of our world but little has actually come to fruition. If you think about it, the only wide-spread use of computer vision has been with selfie filters, Amazon product recommendations, Facebook feed tagging, and a select few others. There's the applications in robotics and self-driving which we've been working on for 10+ years but with no wide-spread use as of yet, along with all the other small solutions in security cameras, etc. My view is that computer vision can become "Google Analytics but for the real world". Google Analytics made it really easy for companies to manage and track site traffic to then make changes / optimizations to the way your site works. In the same way, computer vision will enable this in factories, malls, town centers, traffic-ridden streets, shipping docs, and almost any other physical place you can think of.

This changes the way our global supply chain works and can create a lot of value through simple collection of these insights.

## What's Wrong?

What's wrong though? Why hasn't computer vision been able to be deployed in most of these scenarios? It comes to down to the way these algorithms work today, how they're built, and how quickly they can break down.

Most of the recent success of computer vision algorithms has come from [deep learning][dl] and the ability to fit more and more complex functions. Deep learning is what most self-driving cars use today to detect objects of interest while driving. Turns out however that these algorithms aren't really generalizable. François Chollet, the creator of Keras, exemplifies this perfectly with the following tweet:

![fchollet tweet](https://drive.google.com/uc?id=1sabYomoqRX59VsvuoSxMtRDE07xDkl-H)

We haven't been working on self-driving for 10+ years because we feel like it. It's because we're trying to collect as many "edge cases" as we can in our datasets until we feel comfortable enough leaving it up to the cars.

<div class='jekyll-twitter-plugin' align="center">
    {% twitter https://twitter.com/FSD_in_6m/status/1400207129479352323 %}
</div>

While this is best exemplified with self-driving cars, this limitation exists with virtually every application of computer vision. Teams across industry sometimes assume some of these algorithms to be magic and automatically generalize. This is a myth and it's a dangerous one. Self-driving car companies are some of the most [well-funded companies][well] and still have these issues. Imagine the mistakes a smaller, scrapier team might make.

There are two important takeways from the above.

1. Computer vision models aren't generalizable.
2. Few teams have the resources necessary to follow best-practices when building these models.

##### Computer vision models aren't generalizable

Earlier in this post, we've seen examples of how computer vision algorithms break down, even when built by the most qualified and well-equipped teams. This is an artifact of model performance which can be attributed to the following two factors:

1. Building the right datasets to train models on
2. Properly evaluating real-world performance of models

Building the right datasets to train models on involves [amazing label quality][scale] in the case the problem is supervised and a way to pick which data to actually label and then train the model on. Models can struggle from things like [data drift][drift] and [catastrophic forgetting][catas]. Given that our datasets are always a different distribution from the real-world who's distribution constantly changes and may under-represent certain scenarios / edge-cases which may be important to our use-case, we must be wary of these issues. Methods such as [active learning][al] are being more widely used by teams like [Autopilot at Tesla][autopilot] and are being integrated into services like [Scale][nucleus] and [Aquarium Learning][aq] to make it easier for other teams to do the same.  

There is still a lot of active work happening in this space however with some contreversy around whether active learning works better than random sampling and figuring out at which point we can say these models are actually ready.

Then comes the problem of actually evaluating models properly after they're trained. Most of the time, teams will take a single aggregate metric like accuracy on a test set as their north-star metric and compare different models they train solely off of that.

This methodology is wrong however because it faces the issue of [hidden statification][hs]. Take the example of two models we train to detect people. Say one has an accuracy of 90% and the other has an accuracy of 95%. Say however that model 1 performs at 95% in night-time and model 2 performs at 90% at night-time. If you're deploying this model in a room that tends to stay dark, model 1 is better even though it has a lower overall accuracy. Another reason the methodology doesn't work is because of the way a test set might be sourced. If a team takes a random sample, it already faces the issue that the distribution of the dataset is not the same as the real-world and thus isn't representative of real-world performance.

A better way to break this problem down is in the sense of unit tests or scenarios that are conceptually important to wherever you might be deploying a model. Taking the example of a people detection model again, we might want to build different sets based on the following to ensure we perform at a similar level regardless of the factors:

1. Lighting
2. Gender
3. Type of clothing
4. Race
5. Scene layout type
6. more...

These factors help us decide which scenarios our model performs better in and make deployment decisions comparing models using this context. The issue right now is that these sets are really hard to build because most teams tend not to actually get these other types of metadata labeled as a part of each sample ([unless they have a lot of budget][well]) which makes building these subsets a manual process which engineers would have to go through.

##### Few teams have the resources necessary to follow best-practices when building these models

Companies like Google, Facebook, Tesla, Amazon, Snap, etc are the only ones who've been able to successfully deploy computer vision at a larger scale. It isn't a coincidence that all these companies are valued over $100B. They all...

1. have order of magnitude larger budgets for CV projects
2. are talent aggregators
3. have more people working on these problems
4. have built a lot of internal tooling to help themselves

Smaller teams will constantly take shortucts like the ones below just to name a few:

1. Less rigorous hyper-parameter tuning
2. Random sample / manual test set curation rather than metadata tagging to build better test subsets
3. Non-implementation of active learning (hard to implement internally)

This makes models produced by these smaller teams objectively worse. It also seems inneficient that every small company is trying to attract talent to work on their specific computer vision problem when in reality most of these companies work with similar paradigms with substitution of the type of thing they're predicting and the scenario they're deploying in.

## Scaling Computer Vision

My view here is that it's infeasible to continue with the development of computer vision in the way it's going now. There are so many applications of the technology in our supply chain that it requires smaller teams and startups to tackle them. However, these teams should not keep taking shortcuts and should not have to build computer vision teams and infrastructure from the ground up.

Why not build a talent aggregator that's specifically equipped to build computer vision for everyone, and serve it as models-as-a-service? This seems so much more efficient. This talent aggregator would build a team and all the internal infrastructure necessary to quickly and reliably ship computer vision models to companies that need to apply them to a specific task. The goal of other companies would then be to collect as much data as they can and build the other software and insights around the model's results. We're already seeing this with teams like [Scale Document][doc]. Abstract away the model development lifecycle.

The way to build a successful business here is to find the right attack vector to then scale to a talent aggregator that builds all the relevant infrastructure to quickly ship good computer vision.

This is what I think makes sense to dedicate the next decade of my life to given past failed ventures like [Placeware][placeware] and the constant pains I've seen working at [Ford][ford], [Scale][doc], and [NVIDIA][emb]. It's the single greatest thing I can do with the priors of my past experiences, current interests, and current timing of problems.

[dl]: https://en.wikipedia.org/wiki/Deep_learning
[scale]: https://scale.com/
[drift]: https://en.wikipedia.org/wiki/Concept_drift
[catas]: https://en.wikipedia.org/wiki/Catastrophic_interference
[al]: https://en.wikipedia.org/wiki/Active_learning_(machine_learning)
[autopilot]: https://www.tesla.com/autopilot
[nucleus]: https://scale.com/nucleus
[aq]: https://www.aquariumlearning.com/
[hs]: https://arxiv.org/abs/1909.12475
[well]: https://www.marketplace.org/shows/marketplace-tech/funding-is-pouring-in-to-companies-trying-to-crack-self-driving-tech/
[doc]: https://scale.com/blog/scale-document-ai
[placeware]: https://placeware.io/
[emb]: https://www.nvidia.com/en-us/autonomous-machines/embedded-systems/
[ford]: https://corporate.ford.com/operations/autonomous-vehicles.html