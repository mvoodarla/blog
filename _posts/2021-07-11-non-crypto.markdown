---
layout: post
title:  "Abstracting Away Crypto"
date:   2021-07-11 00:00:00 -0700
categories: tech
---
This post was written after reading the recent post on [1729][1729].

## Introduction

The crypto space has reached new heights in 2021 with Bitcoin reaching [all-time heights][60k], [Coinbase going public][coinbase], a hot [digital art market][beeple], and more institutional adoption. So many people are drinking the crypto Kool-Aid: social media influencers [promoting shitcoins][influencer], and [46 million Americans][46mil] holding Bitcoin as of mid-May. There has been so much market-value created in a much shorter time relative to other types of technologies like the internet. The weird thing though when comparing crypto with other technologies like the computer or the internet is that the technology was created before the application. There is very little practical use of crypto right now. This however does not mean the shortage in projects like [Ethereum][ethereum], [Uniswap][uniswap], and [Solana][solana] which are helping build the infrastructure needed for more applications.

This is why I want to dedicate this post to the applications of this basic blockchain technology and how it might replace so much of the tech we're used to today. Let's abstract away smart-contracts and the blockchain. Assume a decentralized database that anyone can write to, that is extremely difficult to modify or delete. Also assume a simple way to execute code on this database that modifies certain values when different requirements are met.

### Online Social Identity

Right now, most of us use Twitter, Instagram, Facebook, LinkedIn, or some other form of social networking. We have a set of friends, a group of followers, or follow different topics ourselves on these sites. These sites are great ways for us to share and consume content posted by others.

However, there are some big problems with most of these sites. First is that they're insecure. Many top figures have been [hacked on Twitter][twitter-security] for example. Another is censorship and de-platforming where the company behind the site can remove your account or prevent you from posting, one of the most famous incidents being with [President Donald Trump][trump]. The biggest problem by far however is the fact that if you do get de-platformed or feel like posting somewhere else that isn't one of those sites, going to an alternative or preserving that free-speech you want to exercise is difficult. You can't take a following from Twitter for example and move it to your own personal domain.

Imagine however if things like posts and a public profile are all stored on-chain with other private information only being accessible via a private key. This is what [bitclout][bitclout] is trying to build as an alternative to Twitter. There is a bitclout chain and using the network isn't restricted to using bitclout.com. Anyone can build their own clients with different algorithms for recomendation, etc. where people use the one they like the most. This prevents being hacked or any form of de-platforming.

### App Stores

The ongoing case between [Epic Games and Apple][appstore] related to Apple's restrictions on having other in-app purchasing methods outside Apple's payment system which takes a 30% cut has gotten a lot of press coverage. Epic's argument with regards to the fact that as people grow large mobile app businesses, Apple will always be able to take a significant cut of business, decreasing margins and making it harder to compete. Apple's side of the argument is that they've built an amazing phone and OS which gave these companies access to millions of consumers and thus deserves this cut. Apple also has it's own arbitrary safeguards as to which apps it accepts onto the store, etc. The case is complex and it's hard to side with one or the other.

Another story is one where [Google paid billions][12bil] to Apple so it could keep Google search on iPhones.

Let's imagine an alternative however. What if we had a decentralized store with some type of voting process when it comes to adding or removing apps from the store, which still takes a cut but a much smaller one? This cut however doesn't go to a single business and rather goes to the computer which are hosting apps for download and putting more effort into quality reviews for acceptance vs rejection decisions for apps. This makes it easier for companies to compete and makes it impossible for a singal entity to prevent an app from existing on a store.

### AWS S3

Right now, AWS is the most dominant cloud provider out there. Unless you're a giant company, you're not building your own secure infrastructure to host your site or other operations it provides. You're most likely using AWS products like S3, Compute, and Databases. There are some potential issues with this however. What if AWS goes down? There's nothing you can do about it. What if Amazon chooses to up prices? There are a few other competitors right now with GCP and Azure so it's unlikely but it would be a pain in the ass to immediately switch over to an alternative. Also do we trust Amazon to never look at our data? Most of these cloud providers ensure secure encryption but most of the time also store the encryption keys themselves. This might ensure no 3rd parties from accessing your data but it still leaves the door open for AWS to access it if it needs to (say maybe the government comes knocking).

Now let's think of an alternative. AWS is of course more than just storage now but at its start, began with just S3. What if there's a way for any person to lease storage space on their personal computers for some price and securely store bits of your information for you? No one computer will store an entire file and will rather store small parts of it, which can only be accessed all together with some private key. This is essentially what [Filecoin][filecoin] is. This prevents the risk of government seizures, unforseen price hikes, or any real downtime given the properties of decentralization and the ability for files to be stores across an entire network.

### Owning Things

Right now, we carry with us a lot of documentation. This includes things like our passport, driver's license, birth certificate, property documents, etc. This even includes smaller things like a ticket to a concern or a movie. Most of these things are stored physically on paper or on some PDF. There is however a blossoming market of creating fake IDs and in places like India, cases where people [make up property documents][india-prop] and claim they own a piece of property when they actually don't. This is because the entities which issue these documents aren't transperant and nobody can publicly access information to this regard which should be atleast semi-accessible.

Now imagine if these agencies which issued some credential, document, or proof of ownership did it on-chain? Then a person can always prove that they're the real owner of something or verify their identity without the burden of carrying physical documents which can be faked. That would be so much more convenient and also just pretty cool.

### Fake News

We are all probably too familar with the issue of fake news and spread of mis-information. I wrote a [different post][capitol-post] about this when the famous capitol riot happened in January of 2021. Events like that highlight the importance of ensuring that there's some way of fact-checking information. We don't have good ways of doing this right now, and so social media sites have their own private team of people or set of models that manually do this. This has however led to many cases where something false spreads like wildfire or something true is de-platformed.

Now imagine if there was a way to give badges to any piece of content online that communicated some sense of whether a thing is true or not. This could be a system where given organizations or groups which could be represented as [DAOs][dao] are given a certain amount of credibility over certain topics. These organizations can then give certain badges to content they support or disagree with, at which point a decision can be made about whether it can cause harm and should be removed. Obviously, I don't have the perfect idea here of how this would work exactly but it just comes to show how diverse the applications of this blockchain database are.

### Paywalls

Right now, I can't read any content I want on sites like the Wall Street Journal or the New York Times. I need to pay. This is the same for many top scientific journals like Nature or IEEE. Why does knowledge sometimes have a monetary barrier? This definitely shouldn't be the case. The reason these journals or sites exist is because they've all formed a notion of credibility around their name. This is really powerful for good but also allows for these centralized organizations to slowly sneak in opinion or accept papers which don't deserve to be accepted based on the personal motives of a few.

Imagine an on-chain way of sharing papers and giving them some sense of credibility through systems of upvotes, which are weighted based on the readers credentials, which are also stored on-chain. Imagine if rather than journalist working for a bigger organization, they just work for themselves and publish freely on their own sites, which become popular based on the value of their journalism. People can then support these people through donations or by buying some ownership into the journalist's token which increases in value depending on the value of the content they produce.


## Conclusion

I've listed a few applications of blockchain technology but there are a lot more that I haven't mentioned including everything happening in DeFi which will enable a lot more financial freedom. However, it just comes to show how many applications of this technology there are and how it can rewrite almost everything we've build on the web already, and digitize some other things that hadn't yet made it there (like our passports).

[1729]: https://1729.com/crypto-for-people-who-dont-follow-crypto
[60k]: https://cointelegraph.com/news/bitcoin-suddenly-hits-60k-as-a-new-resistance-battle-liquidates-850m
[coinbase]: https://www.theverge.com/2021/2/25/22300835/coinbase-s1-bitcoin-going-public-profit-revenue-invest-crypto
[beeple]: https://www.theverge.com/2021/3/11/22325054/beeple-christies-nft-sale-cost-everydays-69-million
[influencer]: https://mashable.com/article/influencers-altcoin-scams
[46mil]: https://www.nasdaq.com/articles/about-46-million-americans-now-own-bitcoin-2021-05-14
[ethereum]: https://ethereum.org/
[uniswap]: https://uniswap.org/
[solana]: https://solana.com/
[twitter-security]: https://twitter.com/TwitterSupport/status/1283591848729219073
[trump]: https://en.wikipedia.org/wiki/Social_media_use_by_Donald_Trump
[bitclout]: http://bitclout.com/
[appstore]: https://en.wikipedia.org/wiki/Epic_Games_v._Apple
[12bil]: https://www.npr.org/2020/10/22/926290942/google-paid-apple-billions-to-dominate-search-on-iphones-justice-department-says
[filecoin]: https://filecoin.io/
[india-prop]: https://www.bbc.com/news/world-asia-india-20457766
[capitol-post]: https://blog.mokshith.xyz/tech/2021/01/07/state-of-privacy.html
[dao]: https://ethereum.org/en/dao/