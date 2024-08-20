---
layout: page
title: Drone Power Distribution Board
description: Writeup coming soon!
img: assets/img/projects/electronics/follow-me-lights/lights-thumb.jpg
# permalink: /projects/follow-me-lights/
importance: 3
category: electronics
related_publications: true
toc:
  sidebar: right
  scope: h4
images:
  slider: false
  compare: true
---

## Problem

## Circuit Design

## Hardware Design

### The World's Easiest Schematic?

This board is going to solve an admittedly simple problem. We wanted to remove the extra cables and harnessing from the test bed drone and replace it with a single PCB. If done properly, this should reduce the weight of the payload and simplify troubleshooting in the future. If possible, I should also allow for this PDB to used on future designs even if the drone's design changes.

The power input comes directly from the drone's battery through an XT-90 connector. This power is then routed to four motor electronic speed controllers (ESCs), with the possibility of introducing two more in the future. I also recommended that we offer a power output to the drone's control board, which we could choose to use in the future.

<div class="row justify-content-sm-center">
    <div class="col-sm-6 mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/projects/electronics/feather-pdb/pdb-schematic.png" title="Test Bed PDB schematic" alt="Test Bed PDB schematic" class="img-fluid rounded z-depth-1" zoomable="true" %}
    </div>
</div>
<div class="caption">
    Power in from battery, out to motor ESCs and optionally the drone control board.
</div>

<img-comparison-slider>
  {% include figure.liquid path="assets/img/projects/electronics/feather-pdb/pdb-pcb-top.png" alt="PDB PCB topside" class="img-fluid rounded z-depth-1" slot="first" %}
  {% include figure.liquid path="assets/img/projects/electronics/feather-pdb/pdb-pcb-bottom.png" alt="PDB PCB bottom" class="img-fluid rounded z-depth-1" slot="second" %}
</img-comparison-slider>
<div class="caption">
    Power Distribution Board PCB layout. Left image is top side. Slide to compare.
</div>

As an aside, I find documentation on group projects to be really important. When I design my PCBs I always make an effort to include information that might be important for other engineers. Here I included silkscreen labels for the center-to-center distance between the mounting holes, and those holes' diameters. They may go unused, but the information needed is always packaged with the board.

## Results and Reflections
