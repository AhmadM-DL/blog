---
layout: post
title: Web Scraping Tutorial
date: 2020-03-13 13:32:20 +0200
description: Hands-on web scraping with Python
img: web_scraping.jpg 
fig-caption: <span>Photo by <a href="https://unsplash.com/@markusspiske?utm_source=unsplash&amp;utm_medium=referral&amp;utm_content=creditCopyText">Markus Spiske</a> on <a href="https://unsplash.com/s/photos/web?utm_source=unsplash&amp;utm_medium=referral&amp;utm_content=creditCopyText">Unsplash</a></span>
tags: [Web Scraping, Beautiful Soup, Python]
---

This post is about Web Scraping. Despite the important role web scraping plays in real-world data science process, many academia oriented data science courses neglect it. A couple of days ago I passed by an interesting data science piece from EliteDataScience in which they wrote: “To succeed in data science, it’s more important to understand the end-to-end framework —plus the practical tools used in each step— than to obsess over the math and theory behind each algorithm”. I believe this makes sense.
{: .text-justify}

>To succeed in data science, it's more important to understand the end-to-end framework — plus the practical tools used in each step — than to obsess over the math and theory behind each algorithm. *EliteDataScience*

In this lengthy tutorial I will by using Python and Beautiful Soup Library. There is plenty of resources online on the topic, though my tutorial will be more project-oriented than a toy example. In this tutorial we will be scraping **[Al-Akhbar](https://www.al-akhbar.com/)** newspaper website.
{: .text-justify}

#### On Web Pages

This section explains the nature of web pages and the interaction between the user browser and the server [skip if you are familiar with those concepts].
{: .text-justify}

![al_akhbar_dns_request]({{site.baseurl}}/assets/img//al_akhbar_dns_request.png)
{: .text-center}

*Web Request*
{: .text-center}

Every content provider on the internet host their data on server machines [ specialized computing devices - some on the cloud]. Those machines are associated with IP addresses [ similar to your home address ] and a domain name. For example when you ask your browser to get al-akhbar.com, al-akhbar.com is a domain name. The browser sends your request to a special server called Domain Name Server (DNS) [ it behaves as your mobile contacts list, though it associates domain names with IP addresses] that get the IP address associated with al-akhbar.com and send it back to the browser. Now that the browser has the IP address it sends a request to Al-Akhbar server to send back it’s main page.
{: .text-justify}

![Al-Akhbar Front Page]({{site.baseurl}}/assets/img//al_akhbar_front_page_html_css_js.png)
{: .text-center}

*Files to Page*
{: .text-center}

What does the server returns back? What we see is an aesthetically pleasing front page. But how this end up in our browser? The server sends 3 main files (HTML, CSS, JS, …). The HTML file is a textual file that contains the document structure as in the below over-simplified example:
{: .text-justify}

```html
<html>
    <head>
        <title>الأخبار</title>
    </head>
    <body>
        <article>
            <article-title>كورونا</article-title>
            <article-body>ألخ، ألخ، ألخ</article-body>
        </article>
    </body>
</html>
```

In the previous HTML code the stuff between <> are called *tags*. Those are the basic building blocks for structure in HTML. A tag has a name, attributes, and children.
{: .text-justify}

For example ```<p class="x" > Hello </p>``` is a tag of name ```p```, it have an attribute named ```class``` of value ```x```, and it has a text ```Hello```. Tag names denote some semantics. For example ```<p>``` tag signifies a paragraph while an ```<a>``` tag signifies a hyperlink and so on. Children of a tag are the tags that fall inside it. For example the ```<article>``` tag in the previous code has two children tags ```<article-title>``` and ```<article-body>```.
{: .text-justify}

The CSS files contain how the parts of the HTML are aesthetically displayed (margin, bg-color, padding, …). The JS file contains some code to manipulate the page (click this -> do this) [ This may end up being very complex ].  Hence your browser is the software responsible for compiling those three files [and many other files actually] into the pleasing web pages you see online. That is why the same website could have different representations if you used different browsers (firefox, chrome, explorer, …).
In web scraping we are *mostly* concerned with HTML and CSS files [ In this tutorial we will depend only on HTML ].
{: .text-justify}

#### Web Scraping

Now that we are more familiar with web pages we can get into web scraping. As we will get to know, the data science process is composed of several parts. The first would be data collection. Web scraping is one way to collect data. It is simply the act of programmatically browsing the internet and getting data, whether the data is textual or visual.
{: .text-justify}

WebHarvy - a visual web scraper - introduce web scraping as following: “Data displayed by most websites can only be viewed using a web browser. They do not offer the functionality to save a copy of this data for personal use. The only option then is to manually copy and paste the data - a very tedious job which can take many hours or sometimes days to complete. Web Scraping is the technique of automating this process, so that instead of manually copying the data from websites, the Web Scraping software will perform the same task within a fraction of the time.”
{: .text-justify}

In our case we want to scrape the HTML file send by Al-Akhbar website and extract the articles from it. To do this we have to parse the HTML files using some Python libraries and extract text from selected tags. We select tags using their names, attributes, and order.
{: .text-justify}

In the following section we will get into the coding part. As aforementioned we will be using Python. This tutorial assumes a basic knowledge of programming, setting the Python environment, installing libraries. If you are unfamiliar with Python environment then you can use an already set up online Python environment at [Google Colab](https://colab.research.google.com/) which I recommend for every data scientist.
{: .text-justify}

#### Get Into Coding

##### Explore the target website(s)

The first step in web scraping is to explore the target website(s) and explore the tags that hold the data you are searching for. In some cases tags that hold the data are obscured in a way or another that prevents scraping. Have you ever passed by an “I am not a robot” captcha? One goal of this captcha is to prevent *programmatic* access to the corresponding website. Other times the data you are searching for can easily be found and extracted through the selection of well-structured tags.
{: .text-justify}

>N.B.: The following code is dependent on Al-Akhbar HTML file structure. If Al-Akhbar changed their HTML structure, the code has to be tweaked to adapt to changes.

In our case we need to collect a dataset of Al-Akhbar news articles. The first thing we will do is to check the HTML structure of a news article and formulate a way to get the article text. To do so we will be using the built-in developer tools in Google Chrome [also available on other browsers]. After opening the target website, right-click on the element you want to check it's HTML structure and click inspect. As in the below image.
{: .text-justify}

![Inspect Element](./{{site.baseurl}}/assets/img//inspect-element.gif)
{: .text-center}

*Inspect Element*
{: .text-center}

As you can see, given an article link it is easy to get the article text by selecting the ```<div>``` tag that has an attribute ```class``` of value ```content```.
{: .text-justify}

```html
<div class="content">
        <p></p>
        <div class="articlebody">
        ... التقرير ...
        </div>
        <p></p>
</div>
```

Though we don’t want to scrape one article, we want hundreds of articles from multiple news editions. Does the website list all editions and their corresponding articles? We need to explore the site more. If we do, we will find a link that lists different editions. The link exists on the site’s menu bar under the tab “الأرشيف”. The link is [https://www.al-akhbar.com/Editions](https://www.al-akhbar.com/Editions).
{: .text-justify}

The page lists links to editions back to the year 2006. And if we inspect those links they are all of the following form  ```al-akhbar.com/Editions/{year}/{month}/{day}```. For example [www.al-akhbar.com/Editions/2020/1/21](www.al-akhbar.com/Editions/2020/1/21). And each one of these pages presents a list of articles titles under different headlines.
{: .text-justify}

![Edition Page]({{site.baseurl}}/assets/img//al_akhbar_edition_page.png)
{: .text-center}

*Edition Page*
{: .text-center}

If we checked the headline HTML element and articles titles elements we can see a structure that we can use.
{: .text-justify}

```html
#Headline
<div class="section">
    <h2 class="section-title">
        <a href="/Lebanon">
            لبنان
        </a>
    </h2>
    <div class="section-content">
    ...
    </div>
</div>
```

So we have a ```section``` that has a ```section-title``` and a ```section-content```.
{: .text-justify}

```html
#Article Title
<ul class="articles list">
    <li class="article">
        <a href="/Lebanon/282867/" class="title">
            ... عنوان ...
        </a>
        <span class="section">سياسة</span>
        <span class="author">الأخبار</span>
    </li>
    ...
</ul>
```

 The ```section-content``` in turn have an ```articles list``` of ```article```. An ```article``` has a link ```a```, a ```section```, and an ```author```.
{: .text-justify}

Now that we explored the website enough we can formulate a *pseudo* code to get our data.
{: .text-justify}

```
sections = ["لبنان", "رياضة"] # Or designated sections
# loop over editions
for year in [2006-2020]: # Or designated years
 for month in [1-12]: # Or designated months
  for day in [1-31]: # Or designated days

   # get edition html file
   edition_page = get_page("www.al-akhbar.com/Editions/{year}/{month}/{day}")

   if page doesn't exist:
    continue

   # an edition have a list of sections
   # loop on sections
   for section in sections:
    section_element = get_section(section)

    if section_element doesn't exist:
     continue

    # a section have a list of articles info.
    articles_list_element = get_articles(section_element)

    # loop on articles info.
    for article_element in articles_list_element:

     # for each article get title, author, link
     article_title = get_title(article_element)
     article_author = get_author(article_element)
     article_link = get_link(article_element)

     # get article html page through link
     article_page = get_page(article_link)
     article_content = get_content(article_page)

     # store the article
     store(article_title,
           article_link,
           article_author,
           article_content,
           article_date,
           article_section)
```

##### Actual Code - Finally

A final version of the code is available [here](https://github.com/AhmadM-DL/AhmadM-DL.github.io/blob/master/code/Web_Scraping.ipynb).

First we have to import the main libraries we will be using.
{: .text-justify}

```python
# A library to get web pages
import requests

# A library to parse html using it we can get particular tags from an html file
from bs4 import BeautifulSoup

# An essential library in data science that allows tabular data manipulation
import pandas as pd
```

Then we initialize our targeted articles.
{: .text-justify}

```python
root_url = "https://www.al-akhbar.com/Editions"
targeted_sections = ["لبنان", "رياضة", "ثقافة وناس"]
targeted_years = ["2018", "2019", "2020"]
targeted_months = ["1", "2", "3", "4", "5", "6", "7", "8", "9"]
```

Then we define the object that will hold our data. We will initialize an empty Pandas DataFrame.
{: .text-justify}

```python
al_akhbar = pd.DataFrame(columns=["year", "month", "day", "section", "article_title", "article_author", "article_url", "article_sub_section", "article_intro", "article_body"])
```

Now we visit the pages of the edition and get the targeted article news. We do this by looping over each edition doing the following for each edition:
{: .text-justify}

- get page
- get articles info. [title, author, URL, sub-section, …] from targeted sections
- for each article visit URL and get [intro and content

```python
for year in targeted_years:
  for month in targeted_months:

    # loop over all days
    for day in range(1,32):

      # formulate the edition url
      # e.g. https://www.al-akhbar.com/Editions/{year}/{month}/{day}
      edition_headlines_url = "/".join([root_url, year, month, str(day)])

      print("Processing %s"%(edition_headlines_url))
      # get the html file using requests
      edition_headlines_html = requests.get(edition_headlines_url).content

      # load the html file into BeautifulSoup to be parsed
      edition_headlines = BeautifulSoup(edition_headlines_html)

      # get edition title
      # the title is represented in the html file as an h1 tag with class page-title
      edition_title = edition_headlines.find("h1", class_="page-title")

      # at some days an edition was not published
      # in this case the page-title tag contains the below phrase
      # or it doesn't contain a page_title tag
      # if so continue skip this edition
      if not edition_title or edition_title.text.strip() == 'عذرا لا يوجد عدد':
        # no edition during this date
        continue

      edition_title = edition_title.text.strip()

      # we still need to get articles in the targeted sections

      # get all edition sections
      # sections are represented by a div tag with class section
      # they contain the corresponding articles as children tags
      edition_sections = edition_headlines.find_all("div", class_="section")

      for section_title in targeted_sections:

        # Get section
        # we select sections from their section-title tag
        section_html = [section for section in edition_sections if section.find("h2", class_="section-title").text.strip() == section_title ][0]

        # get all section articles
        # articles are represented as li tags with class article
        articles = section_html.find_all("li", class_="article")

        # loop on the articles
        for article_info_html in articles:

            # get article title
            article_title = article_info_html.find("a", class_="title").get_text(strip=True)

            # get article url
            article_url = "https://www.al-akhbar.com"+article_info_html.find("a", class_="title").get("href", "")

            # get article author
            article_author = article_info_html.find("span", class_="author").get_text(strip=True)

            # get article sub-section
            # after a trail and error I found that some articles doesn't contain a sub-section
            # get the subsection only if it have one
            article_sub_section = article_info_html.find("span", class_="section")

            # if article have a subsection
            if article_sub_section:
                article_sub_section = article_sub_section.get_text(strip=True)
            else:
                article_sub_section = "NA"

            # now we have to visit the actual article page and get intro and content
            # request and parse as in edition
            article_html = requests.get(article_url).content
            article_html = BeautifulSoup(article_html)

            # check if it has an article tag
            # after a trail and error I found that some edition headlines corresponds to dossiers and not articles
            # if that the case ignore and go to next article
            article = article_html.find("article")

            if not article:
                continue

            # get article intro. it is represented with a div tag with class intro
            article_intro = article.find("div", class_="intro").get_text(strip=True)

            # get article body
            # article body is represented by a div tag with class content
            article_body = article.find("div", class_="content")

            # after trail and error I found that the article body contains some scripts tags that will eventually appear in the text
            # to remove them we will remove the tags before getting the text
            for script in article_body("script"):
                script.decompose()
            article_body = article_body.get_text( " ", strip=True)

            # now we will store that article info in the DataFrame
            al_akhbar = al_akhbar.append({"year": year,
                                          "month": month,
                                          "day": day,
                                          "section": section_title,
                                          "article_title": article_title,
                                          "article_author": article_author,
                                          "article_url": article_url,
                                          "article_sub_section": article_sub_section,
                                          "article_intro": article_intro,
                                          "article_body": article_body}, ignore_index=True)
```

That's it all!

![Al_Akhbar DataFrame]({{site.baseurl}}/assets/img//al_akhbar_output.png)
{: .text-center}

*Collected Data DataFrame*
{: .text-center}

We still need to save the data as a [CSV](https://en.wikipedia.org/wiki/Comma-separated_values) [comma separated vector] file.
{: .text-justify}

```python
al_akhbar.to_csv("al_akhbar.csv")
```

 A CSV file is a wildly known file format for data exchange where values are delimited with a comma as in below:
{: .text-justify}

```csv
id, sex, age
1232, M, 33
5432, F, 32
9172, F, 23
...
```

Note that running the script will take some time depending on the targeted years and months.
{: .text-justify}

### Conclusion

In this post we went through the web scraping workflow. Although the workflow was relatively smooth in this tutorial that is not always the case. And as you can see from the code part, there will always be some web pages exceptions that will be concealed until you do some trial and error cycles. However, what is great about web scripting is that once you have the script done, you can collect as much data as you want.
{: .text-justify}

As aforementioned, web scraping falls in the first part of the data science process which is data collection. In the following posts I might propagate the data collected here to the next parts of the data science process i.e. Exploratory Data Analysis (EDA) or complement the data collection part with data enrichment which is equally important.
{: .text-justify}
