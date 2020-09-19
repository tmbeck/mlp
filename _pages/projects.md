---
title: "Projects"
description: "Documentation on some of my projects and ideas."
layout: page
toc: true
permalink: /projects/
comments: false
hide: false
search_exclude: false
categories: [ml, jupyter]
---

*Where failure isn't just an option, it's expected.*

# Projects in progress

## Fossil Identification

[Reddit](https://www.reddit.com) is a popular social media website with user submitted content. Subreddit `r/fossils` frequently has posts such as [this one](https://www.reddit.com/r/fossils/comments/int102/my_grandma_found_this_on_a_lake_erie_beach_any/?utm_source=share&utm_medium=web2x&context=3), asking for identification (there is another subreddit, `r/fossilid`, for this purpose). Could we train a model to classify such images?

Hypothesis: A machine learning model could ultimately be used by the scientific community to identify species, provided a sufficiently large dataset.

Objective: Train a model that can recognize fossils. Create a reddit bot that can reply to posts with classifications, allowing for replies on various subreddits that can help train the model.

Background: For obvious reasons, idenification and taxonomy are important topics for paleontologists. Here, I will train a model using labels that provide as much or more detail as `class`, as per [modern taxonomic classification](https://en.wikipedia.org/wiki/Taxonomy_(biology)#Kingdoms_and_domains), with the ultimate goal that a model can identify a specific species (or conversely, identify a species it does not recognise). 

See [Trilobite evolutionary rates constrain the duration of the Cambrian explosion](https://www.pnas.org/content/116/10/4394) for how trilobites are classified. A model trained on sufficiently large data set should be able to identify an entire class (e.g. it can identify a fossil's species if that fossil is known in class trilobita).

Methodology: To do this, I use the same subreddits as a source for material in order to build a dataset. The model will use `resnet34` as its `architecture`. I build upon my growing knowledge from the fastai courses to achieve this.

### Exploration

Based on the experience creating a model that can identify teddies (fastai course v3), then cats vs. dogs (course v4), this is plausible but we will need to build a dataset.

Began by investigating solutions for scraping images. Initially considered using reddit.

1. Initial solution: use [ParseHub](https://www.parsehub.com/) to scrape reddit and download images.
    * Pros
        * Low code, visually build scraping logic
        * Output can be automated and available in CSV via API
    * Cons
        * Eventually, not free
        * Results inconsistent, particularly with the "new" reddit site layout
        * Slow (unless you pay for it)
        * Costs $$$

    Tried this solution. Limited success, thanks to a number of tutorials out there showing how to scrape [old.reddit.com](https://old.reddit.com). This is a no go.

2. Better solution: use [praw](https://praw.readthedocs.io/en/latest/getting_started/quick_start.html), [tutorial here](https://www.storybench.org/how-to-scrape-reddit-with-python/) and [here on towardsdatascience](https://towardsdatascience.com/scraping-reddit-data-1c0af3040768). Obtain API creds, write own scraping logic. Build into a notebook.

### Dataset Construction

1. [Scrape images off of reddit](jupyter/2020/09/06/fossil-dataset.html)
2. [Bing image search](/fossils/jupyter/2020/09/18/Fossils-Production.html)

# Ideas for new projects

## Optical character recognition (OCR) of historical documents

There are a lot of documents (such as the image below) that are difficult to read. Can a model learn to read the image?

![Old English Document]({{site.baseurl}}/images/olde_english_small.jpg "Sample document candidate")

### Research

Looks like this is already being done to varying degrees:

* [pytessaract](https://github.com/madmaze/pytesseract)
* [An example of using tesseract](https://stackabuse.com/pytesseract-simple-python-optical-character-recognition/)
* [NanoNets Tutorial OCR with tesseract](https://nanonets.com/blog/ocr-with-tesseract/#trainingtesseractoncustomdata)

Looks like we'd need to either cut the image up into single images (similar to the MNIST dataset) or use image segmentation. Looks like the OCR examples do some image segmentation, especially for some of the documents.
