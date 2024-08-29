---
layout: page
title: Product Color Detection
description: <!> Writeup coming soon!
img: assets/img/publication_preview/wave-mechanics.gif
importance: 1
category: software
images:
  slider: true
  compare: false
toc:
  sidebar: right
  scope: h4
---

## Background

I graduated from UT Austin in 2022 as an electrical and computer engineer. Shortly after my graduation, I teamed up with a friend and former web client to work on a "furniture search engine".

The basic idea was a user could come to our website looking for a specific type of furniture. Once there, they could filter by dimensions, color, material, or other characteristics and filter their search to a few good candidates.

Our site was intended to prevent the normal dragging flow of shopping for furniture. Instead of having to visit a dozen different sites, traverse their menus, and attempt to use what filters they had, a user could instead simply do all the searching from our site. Once they found some items they liked, they would go buy them directly from the retailer.

In short, we were doing product aggregation. Think of Google Shopping, but just for furniture.

## Problem

After some months of development, we actually had began to have some success in collecting product information from multiple data sources. Before this data was to be shown on our website, I needed to standardize the product data to our internal schema.

One of our website's product requirements was that each furniture product should be filterable by color. This immediately posed a huge question.

**What even is color?**

I don't mean that facetiously. What do we _really_ mean by color, and how can we communicate color in a standardized fashion?

### The Limitations of Color Names

Most of the products coming through our data pipeline had no color information presented at all. The few that did would offer color values with names. Terms such as "khaki", "Royal Peacock", and "velvet emerald" were abundant.

But what can we do with those names? A common conundrum is the color olive. Is olive a dark, warm, earthy green or a darker tan?

<div class="row justify-content-sm-center">
    <div class="col-sm-5 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/projects/software/color-detection/olive-colors.jpg" title="Olive colors" alt="Olive colors" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Which of these is the true olive color?
</div>

When I say "Royal Peacock", I'm sure some color comes to your mind. Now tell me if that is closer to "azure" or "turquoise".

You can readily see the issue. Describing these colors with words is going to be a dead end, especially since companies like to invent new terms for colors to make their products seem more luxurious.

### Color by Numbers

To really describe colors effectively, I was going to need a numerical approach. Fortunately, this already exists in abundance.

In computers, most colors are described using an [RGB value](https://en.wikipedia.org/wiki/RGB_color_model). This assigns a number, often from 0 to 255, to the relative red, green, and blue values of a color. Because of the properties of light, we can create any color by combining red, green, and blue in different proportions.

<div class="row justify-content-sm-center">
    <div class="col-sm-8 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/projects/software/color-detection/rgb-colors.png" title="RGB color wheel" alt="RGB color wheel" class="img-fluid rounded z-depth-1" zoomable="true" %}
    </div>
    <div class="col-sm-4 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/11.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    You can also have artistically styled 2/3 + 1/3 images, like these.
</div>

This is a great start to describing our products in an objective, numerical fashion. Instead of using words, we can describe each color as a collection of three numbers, its RGB value.

### Pick a Number, Any Number

Using a color model, we can now describe any color numerically. Unfortunately, an image has a _lot_ of colors. In fact, every single pixel is just a single color value.

For a relatively small image, say 500 pixels by 500 pixels, we end up with 250,000 individual color values. And each of these pixel color values can be unique! If you have a quarter of a million options for the "color" of an image, you end up with a large task trying to pick just one, or even a handful.

We now have a new problem. **How can I pick the color value(s) that best represent the color of a product just from its image?**

## Enter Image Analysis

Like most programming problems, this challenge is best approached by breaking it into smaller problems and solving those in turn. I chose to chop this problem approximately like this:

- Can I "cut out" the product from the image?
- Can I determine the dominant "average" colors of the product?
  - Can I change how many colors I add to this palette?
- Should the colors be sorted by how much of the image they describe?
- Can I group approximate color values to color names?

Many of these questions fall into the domain of computer vision and image analysis. Fortunately for me, many generous scientists have developed really effective python libraries to help engineers solve these problems.

### Image Segmentation

Before we are able to determine the colors of the product, we must first determine what part of the image _is the product_. Most product images come with a standard, all white background. Or, if you are really ~_fancy_~ (looking at you, Crate & Barrel), the product backgrounds might be a slight off-white.

If we were to include the white background of these images, the color palette would be overrun with white. In short, we need to cut out the product from the background such that we only analyze the actual colors of the product.

<!-- <div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="" title="Donkey Kong 3 Arcade Machine" alt="DK3 Arcade Machine" class="img-fluid rounded z-depth-1" zoomable="true" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="" title="Barna playing Donkey Kong 3" alt="Barna playing DK3" class="img-fluid rounded z-depth-1" zoomable="true" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="" title="Austin Cidercade Classic Games" alt="Austin Cidercade Classic Nintendo Arcade Games" class="img-fluid rounded z-depth-1" zoomable="true" %}
    </div>
</div>
<div class="caption">
    Barna and I discovering Donkey Kong 3 at the Austin Cidercade.
</div> -->

<swiper-container keyboard="true" navigation="true" pagination="true" pagination-clickable="true" pagination-dynamic-bullets="true" rewind="true" height="600px">
  <swiper-slide>{% include figure.liquid loading="eager" path="assets/img/projects/floating-arcade/just-assembled.jpg" class="img-fluid rounded z-depth-1" title="Arcade just assembled, checking buttons" alt="freshly assembled" zoomable="true" %}</swiper-slide>
  <swiper-slide>{% include figure.liquid loading="eager" path="assets/img/projects/floating-arcade/paint-prep.jpg" class="img-fluid rounded z-depth-1" title="Wrapping arcade for paint preparation" alt="Arcade paint prep" zoomable="true" %}</swiper-slide>
  <swiper-slide>{% include figure.liquid loading="eager" path="assets/img/projects/floating-arcade/paint-prep2.jpg" class="img-fluid rounded z-depth-1" title="Wrapping arcade top for paint preparation alt" alt="Arcade paint prep 2" zoomable="true" %}</swiper-slide>
  <swiper-slide>{% include figure.liquid loading="eager" path="assets/img/projects/floating-arcade/spraypaint.jpg" class="img-fluid rounded z-depth-1" title="Arcade outside, ready for painting" alt="Arcade spraypaint imminent" zoomable="true" %}</swiper-slide>
  <swiper-slide>{% include figure.liquid loading="eager" path="assets/img/projects/floating-arcade/fully-painted.jpg" class="img-fluid rounded z-depth-1" title="Arcade post painting, awaiting hardware" alt="Arcade post painting" zoomable="true" %}</swiper-slide>
</swiper-container>
<div class="caption">
    Gallery of the arcade frame getting painted.
</div>

## Reflections

<div class="row justify-content-sm-center">
    <div class="col-sm-8 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/6.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm-4 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/11.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    You can also have artistically styled 2/3 + 1/3 images, like these.
</div>
