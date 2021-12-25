---
layout: post
title:  "Solving Computer Vision: Applying First Principles"
date:   2021-12-25 00:00:00 -0700
categories: tech
---

## Introduction

In my last post from a few months ago, I wrote my view on the future of computer vision. I suggest you read that first, to see how my perspective has changed.

The biggest change in perspective comes from a practice I've been using for some time now. I only realized recently that such practice is called [First Principles Thinking][first-principles]. It's the idea that you condense a complicated problem down to the fewest facts you know to be true about it, and then try to extrapolate everything else you can from those simple facts.

## Is it really a problem with computer vision?

Our claim is that computer vision has many issues today, preventing it from becoming ubiquitous. More specifically but still pretty generally, we claim that the bottleneck has to do with the data we use to train computer vision models. Let's take a step back though and understand what go us to this stage, and how computer vision fits into a more general class of data analysis problems. To do that, let's start with the history of storing data on computers.

### History of Data Storage and Processing
The database was pioneered in the 1960/70s. From [DBMS][dbms] to [RDBMS][rdbms] which led to more efficient ways of storing, processing, and later querying data using languages like SQL - the database has constantly improved. Sometime later came along [MySQL][mysql] which open-sourced RDBMS.

In the late 90s and early 2000s, NoSQL became a lot more popular. The internet needed faster processing of unstructured data and NoSQL could handle both structured and unstructed data while helping scale some of the internets most well-known services like Google, Facebook, and Twitter. The main theme was scalability (large datasets) and flexibility (many schemas).

At some point down the line, these services were scaling really well but become really messy in the sense of different devices or clients writing to different databases or different modes of information being stored in different places. The buzz-phrase here was that data got really siloed - which made it hard for business to make data-driven decisions easily. This is what led to the creation of services like [Snowflake][snowflake] which provide what we call [data warehousing][data-warehousing]. Other companies like [Segment][segment] made a living within this problem of siloed data, but in their own niches like the consolidation of customer data into a single API. A whole separate set of services grew out of this with companies like [Fivetran][fivetran] and [Airbyte][airbyte] which act as easy plug-and-play connectors that update your data warehouse periodically from hundreds of different sources.

All things considered, the ecosystem is large and prosperous today. However, a key thing to note is that this large ecosystem is only limited to the most primitive data-types like text and numbers. Sure, we can store and retrieve other types of raw data like audio, images, etc but nothing at the level of operations we can perform on text and numbers such aggregation, counts, transformations, etc.

### New Types of Data
There is already so much attention put forth to companies solving these traditional data problems and don't get me wrong, there's still so much to solve there. From [better internal data search tools][secoda] to [open-source database alternatives][supabase], there is still so much going on. But, I think we're set for a larger revolution within the niche of non-traditional data types. Think images, videos, LiDAR, RADAR, audio, and more.

Think about robotics for example. At the end of 2019, there were about 2.7 million operational industrial robots and the projection for the end of 2021 is close to 3.8 million (source: [IFR][ifr]). A growing number of these robots will have all types of sensors, either for the purpose of controlling the robot or the for the purpose of collecting data for later analysis.

Imagine parallel applications in factories that can monitor for worker safety using cameras, or detect defective parts. Or other applications in city streets and store for security, shopper / traffic analysis, etc. We are in an age where our ability to work with these more complex data types has increased multiple orders of magnitude due to different types of analytic techniques like deep learning. This will only accelerate the number of applications we come up with for this kind of technology.

### What's actually going wrong
In my last post, I wrote about the ML-specific issues with computer vision today and why we're struggling from that perspective. We struggle with building good computer vision models because it's really hard to build good datasets, and building good datasets is really hard because of poor tooling. But I'd now argue that such a statement doesn't do a good job of getting to the root cause of why we have poor tooling. Analyzing the history of databse I'd now argue the following:

**Our databases weren't designed for handling more than simple text and numbers.**

There is a lot of work happening focused on building ML-specific tools for this but I'm not sure whether that's the best mindset to have as we build these things. The problems we're talking about are first being experienced in communities like computer vision and ML because that's where these new types of data are being most quickly aggregated today. They're not the only industries though that can benefit from storage more purpose-built for richer data types. How do e-commerce stores manage their visual assets? Or gaming / animation studios?

## Pondering a Solution
The biggest difference between traditional data like numbers and text versus newer types of data like images, videos, audio, 3D scans, and more are that these new types of data have greater semantic meaning. They're however still stored solely as their individual bytes rather than with a stronger connection to what they actually represent. There's a few reasons for this involving lack of robust all-purpose models and high compute-costs. Imagine being able to perform operations like equality, difference, grouping, counting, and more with these non-traditional data types in ways as trivial as it is with text and numbers.

I think we have the necessary tech today to build such a solution. Questions still lie who wants this right now, how would they use it, and how much would they pay for it.

Answering those questions is still WIP. Keep following these posts because I guarantee to post clear answers to those questions in 3 months time.

[first-principles]: https://fs.blog/first-principles/
[dbms]: https://www.geeksforgeeks.org/history-of-dbms/
[rdbms]: https://en.wikipedia.org/wiki/Relational_database
[mysql]: https://www.mysql.com/
[snowflake]: https://www.snowflake.com/
[data-warehousing]: https://aws.amazon.com/data-warehouse/
[segment]: https://segment.com/
[fivetran]: https://www.fivetran.com/
[airbyte]: https://airbyte.io/
[secoda]: https://www.secoda.co/
[supabase]: https://supabase.com/
[ifr]: https://ifr.org/ifr-press-releases/news/record-2.7-million-robots-work-in-factories-around-the-globe
