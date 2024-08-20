---
layout: page
title: Follow-me Lights
description: Writeup coming soon!
img: assets/img/projects/electronics/follow-me-lights/lights-thumb.jpg
permalink: /projects/follow-me-lights/
importance: 3
category: electronics
related_publications: true
toc:
  sidebar: right
  scope: h4
images:
  slider: false
  compare: false
---

## COVID Blues

## Trial and Error

## The First PCB

### Baby's First Schematic

Sorry in advance for this first schematic. In my defense, this really was the first one I ever made. At the time, I did not know you could label your nets, so I made sure that **every** ground and power wire were connected, leaving a tangled mess. Pretty impressive, considering that the whole board only had five total components, and over two thirds of those wires are just for power.

For your amusement, I included my first draft. To the right is one easier to understand. This board is mostly used to transfer power between our components, and some signals too. The `POWER IN` powers the full board. The two 15 pin headers attach to an Arduino nano clone, which accepts the motion signal from the RCWL-0516 motion sensor, and drives the attached LEDs. If the `VERT` switch is off, the LEDs will not illuminate.

<div class="row justify-content-sm-center">
    <div class="col-sm-5 mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/projects/electronics/follow-me-lights/v1/v1-schematic.png" title="Light PCB v1 schematic" alt="Light PCB v1 schematic" class="img-fluid rounded z-depth-1" zoomable="true" %}
    </div>
    <div class="col-sm-5 mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/projects/electronics/follow-me-lights/v1/v1-schematic-fix.png" title="Light PCB v1 better schematic" alt="Light PCB v1 better schematic" class="img-fluid rounded z-depth-1" zoomable="true" %}
    </div>
</div>
<div class="caption">
    Left: First attempt at making a schematic. Right: a much clearer attempt.
</div>

### v1 PCB Design

Much like the schematic tomfoolery above, this PCB demonstrates a few rookie mistakes. The prospect of making a two sided PCB with vias was intimidating to me at the time, so I routed every wire across the top. Honestly the auto-router may have done a better job. My biggest concern with this board looking back is the fact that the power traces are just _so_ skinny. For the amount of amperage the LEDs demanded, I am shocked this even worked.

<div class="row justify-content-sm-center">
    <div class="col-sm-5 mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/projects/electronics/follow-me-lights/v1/PCB_Screenshot.jpg" title="Light PCB v1 layout" alt="Light PCB v1 layout" class="img-fluid rounded z-depth-1" zoomable="true" %}
    </div>
    <div class="col-sm-5 mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/projects/electronics/follow-me-lights/v1/pcb-design.jpg" title="Light PCB v1 rendered design" alt="Light PCB v1 rendered design" class="img-fluid rounded z-depth-1" zoomable="true" %}
    </div>
</div>
<div class="caption">
    Left to right: Light PCB v1 layout, PCB rendered design.
</div>

<div class="row justify-content-sm-center">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/projects/electronics/follow-me-lights/v1/single-board.jpg" title="Light PCB illuminated single board" alt="Light PCB illuminated single board" class="img-fluid rounded z-depth-1" zoomable="true" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/projects/electronics/follow-me-lights/v1/board-panel.jpg" title="Light PCB illuminated single panel" alt="Light PCB illuminated panel" class="img-fluid rounded z-depth-1" zoomable="true" %}
    </div>
</div>
<div class="caption">
    PCB held up to light, both individual board and panel.
</div>

Fortunately, these boards actually worked exactly as intended. Not only did these save an immense amount of time on assembly, they were also smaller, more rugged, and less prone to shorts. Those reasons were all why PCBs were invented in the first place, but I really earned an appreciation for them after struggling against the perfboards for so long. Below you can see the huge difference the new PCB made on the size of the LED driver.

<div class="row justify-content-sm-center">
    <div class="col-sm-8 mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/projects/electronics/follow-me-lights/v1/v1-assembled.PNG" title="Comparisson of perfboard to V1" alt="Comparisson of perfboard to V1" class="img-fluid rounded z-depth-1" zoomable="true" %}
    </div>
</div>
<div class="caption">
    First PCB assembled (left), compared to the perfboard prototype. 
</div>

## Scaling Hardware

So we had a huge improvement in the size and assembly of the LED driver, but it was not yet ready to be a real project. Mainly, this design was using a full Arduino Nano clone development board, soldered directly to the PCB to save space. Although we could get them cheaper in bulk, the product was still going to be too large and too expensive to take to market. We needed to skinny this down further.

### V2 Design

<div class="row justify-content-sm-center">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/projects/electronics/follow-me-lights/v2/v2-layout.JPG" title="PCB Layout of light controller v2" alt="PCB Layout of light controller v2" class="img-fluid rounded z-depth-1" zoomable="true" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/projects/electronics/follow-me-lights/v2/v2-render.JPG" title="PCB render of light controller v2" alt="PCB render of light controller v2" class="img-fluid rounded z-depth-1" zoomable="true" %}
    </div>
</div>
<div class="caption">
    PCB layout and render of light controller v2
</div>

<div class="row justify-content-sm-center">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/projects/electronics/follow-me-lights/v2/v2-board.JPG" title="Fabricated light controller v2 PCB" alt="Fabricated light controller v2 PCB" class="img-fluid rounded z-depth-1" zoomable="true" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/projects/electronics/follow-me-lights/v2/v2-panel-size.jpg" title="v2 PCB panel" alt="v2 PCB panel" class="img-fluid rounded z-depth-1" zoomable="true" %}
    </div>
</div>
<div class="caption">
    Fabricated PCB, as a single unit and in assembly panel.
</div>

## Results and Reflections
