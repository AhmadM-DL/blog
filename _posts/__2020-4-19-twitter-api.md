---
layout: post
title: Data Enrichment and Twitter Api
---

**Objective**: Hands-on Twitter Api

In a previous post we showed an example of web scraping using Python and we targeted [Al-Akhbar]() website. We collected a bunch of articles. For each article we collected the following information: {Title, Content, URL, Author, Class and Date}. This type of data can be useful for many goals. for example, we can train a model to automatically classify articles. We might be trying this later. But now we want to *enrich* our data and add value to it. We do this by crossing the data we collected by a related data from another domains. How much it would be great if we have associated with each article how much people engaged with it?
{: .justify-text}

Before going more into the details of enriching our data with users engagements using Twitter API, I would like to talk more about data enrichment and its importance.
{: .justify-text}

### Data vs. Data Products

The rise of Data Science in our days is related to different factors. Factors like cheaper computing power, online and offline datafication of human aspects (social media, e-shopping, e-governance, e-health, web browsing, ...), the 4 V's characterizing big data ( Volume, Velocity, Value, Variety), etc. However, it is not only about the massiveness of the data. The Data value plays an important role.  
{: .justify-text}

Business have been the reason behind the advancement of different technologies, and is also  a factor behind the Data Science rise. When businessmen and entrepreneurs see value in something, money pours in. Big Tech companies have started to see value in their massive amount of data and started to gain money from them by building *Data Products*.
{: .justify-text}

Rachel Schutt and Cathy O’Neil in their O'reilly book "Doing Data Science" put it this way: "But it’s not only the massiveness that makes all this new data interesting(or poses challenges). It’s that the data itself, often in real time, becomes the building blocks of data products. On the Internet, this means Amazon recommendation systems, friend recommendations on Facebook, film and music recommendations, and so on. In finance, this means credit ratings, trading algorithms, and models. In education,this is starting to mean dynamic personalized learning and assessments coming out of places like Knewton and Khan Academy. In government, this means policies based on data."
{: .justify-text}

That is why Data Enrichment plays an important role in the Data Science Process (it is also important in academia, though this is out of the scope of this post). Data Enrichment transforms huge and seemingly invaluable data into valuable data that drives decisions and generates money. For example in our case, collecting Al-Akbar news articles only might be of minimal value for the newspaper. But when we associate the articles with users engagements, we can start to smell value. The newspaper then can see what articles interests more it's audience, what articles are controversial, who are the writers that writes engagefull articles, does the time of publishing on the social media affects engagement, etc.
{: .justify-text}

I will end this section by pointing out to the privacy problem associated with data aggregation ( merging data from different sources ). Data aggregation can be considered as a breach for end users privacy. Services users hoping from one online platform to another providing complementary data, are unaware of the possible negative consequences resulting from aggregating their own data by companies. Consider a users who uses Facebook, and Linked-In simultaneously. He have given both platforms access to his data. He usually use facebook for his social life and Linked-In for his professional life. One each platform he conceals some information about himself. Say, on facebook he don't mention his professional achievements. By combining the data from both platforms new information is revealed about him that have been concealed previous to the merge of data. What is worse is that there is a business model built over the idea of aggregating data. Data Brokers companies sells users data to other companies to better optimize their Ad campaigns.
{: .justify-text}

Fortunately, we won't be breaching any user privacy as we are centering our data around articles not users. And users engagements is being anonymized and aggregated. When you center your data around individual users then you should start to worry about their privacy. I can went on and write more about privacy in the age of data aggregation, but that is out of the scope of this article.
{: .justify-text}

### Twitter API

#### Developer Account

[Twitter API](https://developer.twitter.com/en/docs/basics/getting-started) is part of Twitter's Developer Platform. It enables developers to harness the power of Twitter communication network. The API is divided into different groups, the standard includes endpoints that will let you perform the following:
{: .justify-text}

- Post, retrieve, and engage with Tweets and timelines
- Post and receive direct messages
- Manage and pull public account information
- Create and manage lists
- Follow, search and get users
- Retrieve trends

In order to have access to Twitter API you have to have a Twitter Developer account. To have one you have to [apply](https://developer.twitter.com/en/apply-for-access) and fill a form. Go on!
{: .justify-text}

#### Twitter app

The second requirement to access Twitter API is to have a [Twitter App](https://developer.twitter.com/en/docs/basics/apps/overview). Accessing API requires a set of credentials (api key, secret, access tokens, ...) to be sent with each request. One can generate those by creating Twitter apps. 
