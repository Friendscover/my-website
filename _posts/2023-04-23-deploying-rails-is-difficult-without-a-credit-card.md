---
layout: post
author: Tobias Klöpper
---
Recently I have been building a small Rails app for me and my significant other. This website just lists our boardgames and tracks the winner of each game. It is just a small project but I had fun coding it. Currently it has been deployed to [render.com](https://render.com). But the free plan database is limited to just 90 days of activity. The database gets destroyed after this time if there is no credit card provided. And I would like to keep this winning data. 

At this point you have been wondering: “Just provide a credit card, Toby!”. I would like to provide a card but I currently don’t own a single (credit) card. In Germany it is not so common to own a credit card. We mostly use the [debits cards](https://en.wikipedia.org/wiki/Debit_card) of our local bank. And these cards work different than credit cards. Because I did not travel internationally, there was no need for a credit card.

Without a card I am now currently unable to deploy my app to a service host. But why?

### Why do I need a card for the deployment
At first it seemed weird that every service needs to validate a card to potentially charge money. But looking into that dilemma (aka searching online for reasons) it suddenly made a whole lot sense.

Previously I have been using heroku as the go to host for rails applications. But heroku changed [their pricing model](https://help.heroku.com/RSBRUH58/removal-of-heroku-free-product-plans-faq). Therefore the free plan does not exist anymore. Their reasoning:
> “...to manage fraud and abuse from free resources on Heroku, we have made the choice to end these free product plan offerings that will allow Heroku to focus on customers of all sizes.”.

Basically their free plan was too good to be true and was probably abused for fraudelent activities (my guess would be crypto mining). Other free online service provider also face the [same issues](https://sysdig.com/blog/massive-cryptomining-operation-github-actions/).

So to use the heroku services you have to pay and conveniently this is done via credit card. One the one hand it is effective action against misuse of the service. On the other hand it moves all students and new learners to the side. And people without credit cards.

### Different hosts I looked into
There are alternatives to heroku. But because all of them require a credit card (expect render.com), I was not able to deploy on these services. Most people recommend the following services: 1. [Fly.io](https://fly.io/), 2.[Render.com](https://render.com/). 3. [Railway]().
I event tried [Google Cloud](). After skimming the docs it seemed more difficult to setup the deployment. But after the initial login prompt, I had to provide a credit card number again.

### How should I deploy now?
After all I did not find a single host with a free tier, that does not require a credit card. There are now only four possible solutions left:
1. Find a free host (unlikely, but I have to look into Railway.app. Their free plan seems to be promising).
2. Host the rails app myself (less likely. I do not have the hardware to host the app on demand)
3. Prepaid credit card (possible)
4. Just getting a normal credit card.

In the end I just have to accept that providing a credit card number should fix all my current issues with my preferred deployment. 

If you know about any good alternative to deploy a rails app, feel free to contact me via email or via [mastodon](https://mastodon.social/@friendscover).



