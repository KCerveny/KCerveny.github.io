---
layout: post
title: Python Product Image Segmentation
date: 2024-08-29 08:00:00-0400
description: Removing an product's background using image segmentation
tags: code computer-vision jupyter
categories: coding
giscus_comments: false
related_posts: true
# toc:
#   sidebar: right
#   scope: h4
---

## Context

This post is part of an ongoing series discussing the [product color analysis tool](/projects/color-detection) I designed while working at Furnisearch. That project writeup was beginning to get too long, so I split the technical discussion into a series of blog posts.

If you are interested in the high-level details of the project, you can go directly to the [project writeup](/projects/color-detection). I recommend you start there, at least to read the background and motivations of the problem this tool solves.

If you want to see how it works under the hood, you are in the right place. This post will assume a very small level of programming knowledge, and should be accessible to most readers.

## Image Segmentation Breakdown

{::nomarkdown}
{% assign jupyter_path = "assets/jupyter/projects/software/color-detection/image-segmentation.ipynb" | relative_url %}
{% capture notebook_exists %}{% file_exists assets/jupyter/projects/software/color-detection/image-segmentation.ipynb %}{% endcapture %}
{% if notebook_exists == "true" %}

{% jupyter_notebook jupyter_path %}

{% else %}

<p>Sorry, the notebook you are looking for does not exist.</p>

{% endif %}
{:/nomarkdown}
