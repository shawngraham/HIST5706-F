---
layout: post
title:  "Topic Models"
date:   2024-09-26 10:36:30 +0100
tags:   topicModels, data, scripts
---

Yay topic models! Yay text analysis!

Let's have a look at [Voyant Tools](https://voyant-tools.org/). (Fun fact: this was originally branded _Voyeur_.). Voyant works primarily as a web-based GUI, though you can install it on your own machine (where it runs as a server, but serving Voyant _just_ to your own browser at the address https://localhost:8080) (or maybe 8000; I forget). Voyant does a whole suite of text analysis which fundamentally come down to counting words and their collocates and their proximity to other words. AND it can do topic modeling, too!

Just like Python and R though Voyant has the capability to work with notebooks. These are called 'Spyral' and they combine text with a modified form of Javascript. See [Getting Started with Spyral Notebooks](https://voyant-tools.org/spyral/alta-start/) and have a look at the [Spyral Tutorials](https://voyant-tools.org/spyral/learnspyral@gh/Tutorials/).

Some more things to explore:

[A topic model of 75 years of Archaeological Scholarship](https://shawngraham.github.io/archae-topic-models/20000/#) which uses Andrew Goldstone's [DfR Browser](http://agoldst.github.io/dfr-browser/). This approach to topic modeling is largely out of date now (I do like the stream graph [visualization](https://shawngraham.github.io/archae-topic-models/20000/#/model/yearly/raw).

Here's a complete script to topic model John Adams' diaries written in R [link: gist](https://gist.github.com/shawngraham/fefbeb06deb5ed786f41a6aba72da530). You _could_ run the whole damn thing in one go, but it's better to go one little section at a time, to see what's happening and also to trouble shoot because _there will_ be issues; I haven't run this script in a number of years.

[JSTOR's Constellate service](https://constellate.org/builder?unigrams=indigenous,%20indigenous%20peoples,%20residential%20schools) lets you search jstor and create collections; these collections can then be fed into a wide variety of text analysis tools; [see this collection] and here's the [topic modeling notebook](https://github.com/ithaka/constellate-notebooks/blob/master/Topic-modeling/topic-modeling.ipynb). NB you can import that notebook into Google Colab (or [launch it within Constellate itself](https://constellate.org/lab?repo=https%3A%2F%2Fgithub.com%2Fithaka%2Fconstellate-notebooks)).

Here's a version of the LDA approach to topic modeling (via the gensim package) that runs in python and uses the LDAvis package to visualize results: [which you can run in Google Colab](https://colab.research.google.com/drive/1aOq0E1vGFWfu8t5bjpv-kNV5wx0qCWw6?usp=sharing).

And here's an approach to topic modeling that depends on word embeddings [which you can run in Google Colab](https://colab.research.google.com/drive/1FieRA9fLdkQEGDIMYl0I3MCjSUKVF8C-)



