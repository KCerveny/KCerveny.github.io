---
layout: page
title: The Rickety 3D Printer
description: A 3D printer built from scratch in the labs of Texas Inventionworks.
img: assets/img/3.jpg
importance: 1
category: hardware
giscus_comments: true
images:
  compare: false
  slider: true
toc:
    sidebar: right
    scope: h4
---
{% assign image_path = "assets/img/projects/rickety-3d-printer" %}


The *Rickety 3D Printer* was my final lab submission for EE 445L Embedded Systems Lab, one of my favorite classes at UT. It is result of three months of very dedicated work, lots of support from others, and more than a few mishaps. Ultimately, this project submission came in 2nd for the UT ECE Embedded Systems competition, earning just over half of all possible points and getting me out of taking my final.

## Background
During my last year of my UT undergrad I took EE 445L Embedded Systems Lab, considered by many students to be one of the most challenging undergraduate ECE classes. Throughout the semester we were to complete 11 labs, the final lab being of our own design. Throughout the semester we would begin to design and build our final labs. Each team of students would submit their final project to the competition, and the top three projects would be excempt from taking the final exam. For a class as tough as this, the award was a powerful incentive. 

### Texas Inventionworks
I was fortunate to have a few advantages in this project. First, I was a part-time employee at Texas Inventionworks (TIW), the makerspace for engineering students at UT. This place is *magic*. Chock-full of interesting machines, interesting ideas, and interesting people. And I happened to be familiar with many of these interesting machines, ideas, and people through my time working at TIW. 

When the opportunity arose to come up with our own project, I went straight to my colleages and friends at TIW asking for advice. One of the leaders, Steve, offered a great idea. There were some linear rails, belts, and stepper motors left over from a previous project. He offered to let me use those to build a 3D printer if I would mention TIW and generate some excitement for the space.

Wonderful! A win-win for everyone. I could get some parts and a desk in the electronics lab, and all I had to do was hype my favorite place at UT. Easy. Now the hard part.

<div class="row justify-content-sm-center">
    <div class="col-sm-8 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/projects/rickety-3d-printer/loose_parts.JPG" title="loose parts" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
    <div class="col-sm-4 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/projects/rickety-3d-printer/power_plan.jpg" title="napkin math" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    A scattering of parts and a plan
</div>


## Approach
Turns out, this project was actually three projects in a trenchcoat, each depending on the former. In the stack:

1. **The case**: The case is the part most people imagine when they hear "3D Printer". It is all of the hardware that makes the machine: linear rails, belts, motors, lights, the printing bed, end stops, etc. I needed to turn our loose box of parts into a case.
2. **The control board**: Once the case is complete, we have a fully built box that does not do anything. The control board acts as the orchestrator, converting commands into coordinated movements and actions. Everything from the movement of motors, extrusion of filament, to the heating of the bed and filament heating elements are performed by the control board.
3. **The GCode Sender**: With both a case and a control board, the machine can now take commands and convert them into intricate actions. These commands come from our GCode sender. It is responsible for ensuring commands are recieved and executed in a timely manner, and handles unexpected events. 

If you have never worked with 3D printers before, this may seem confusing. I always love a good analogy, so I will try to devise one for you here. 

Imagine this whole system as a car. The **case** is the visible parts: the wheels, the engine, the frame. Very good, but it won't drive anywhere quite yet. In order to move, it will need a way of converting commands into actions. 

The **control board** is like our steering wheel, pedals, indicator blinker buttons, and windshield wiper stick. Of course, the gas pedal does not make the car move. It just converts a command (depression of the gas pedal) into actions (more engine force). The car is now drivable!

Finally, our **GCode sender** is like the driver. Its job is to interperet the state of the environment and convert its plans into commands. If it wants to reach a higher speed, it will send a command for more gas. 

## The Case
First, we need our case. All the commands in the world will not do us any good if there is nothing to perform them. My job was to take the loose parts and assemble them into a machine. 

Now, although this step involved the least electrical engineering, I think it is still exciting to talk about. Being now several years removed from my undergraduate, I still marvel at the fact that it was possible to *build a machine* using the machines at Texas Inventionworks. I will be forever grateful for that opportunity.

### Cutting the Case
So what's the plan? I measured out the linear rails and base to understand the inside dimensions that I would need for the case. A 3D printer is, in most cases, just a box with mounts for motors and the bed. TIW had multiple Spectrum laser beds, good for quickly cutting thin sheets of wood and acrylic with high precision. I could use these to design and fabricate the exterior of the case quickly. 

So I went to a favorite site of TIW, [boxes.py](https://boxes.boringplace.org/), to build a box to the correct dimensions. If you ever find yourself needing to laser cut a 3D project, you ought to check it out. It will save you an enourmous amount of stress designing your projects, and will even plan your finger joints to boot. 

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/projects/rickety-3d-printer/boxes_py.jpg" title="example image" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/projects/rickety-3d-printer/laser-cut_frame1.jpg" title="case building 1" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/projects/rickety-3d-printer/laser-cut_frame3.jpg" title="Drilling mounting holes" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
<div class="caption">
    Left: Crafting the case components using Boxes.py. <br>
    Center and Right: Drilling mounting holes after laser cutting the parts.
</div>

After cutting the outer case from 1/4 inch plywood, I cut a large window in four of the six faces to access the inside. You can see that our vertical rails fit snugly inside. What a relief! The finger joints holding the faces together were *very* snug, and held together easily. With a little wood glue and some clamps, the case ended up being suprisingly sturdy.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/projects/rickety-3d-printer/gluing_case.jpg" title="Assembling the case after checking the rails." class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/projects/rickety-3d-printer/case_no_internals.jpg" title="Printer case without internals" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
<div class="caption">
    Left to right: Assembling the case after checking the rail heights. Final printer case without internals.
</div>

### Testing the Hardware
Last but not least, we needed some internals. All of the parts *fit* in the case, but do they work? I borrowed a pre-built control board and a power supply to test the hardware.  

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include video.liquid path="assets/video/projects/rickety-3d-printer/check_before_assembly.mp4" class="img-fluid rounded z-depth-1" controls=true %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include video.liquid path="assets/video/projects/rickety-3d-printer/zaxis-working.mp4" class="img-fluid rounded z-depth-1" controls=true %}
    </div>
</div>
<div class="caption">
    A simple, elegant caption looks good between video rows, after each row, or doesn't have to be there at all.
</div>

## The Control Board
This component is what made this an *embedded systems* project, and was the heart of the lab. The control board receives signals from a gcode sender and maps those to discrete actions. For this project the control board managed:
- 6 motor drivers
    - 3 for moving in the X,Y, and Z axes
    - 3 for filament extrusion
- 4 fans
    - 3 for cooling print heads
    - 1 fan for cooling the case
- 3 endstops for calibrating the position of the print head
- 1 heated print bed
- 3 thermistors for measuring the temperature of the heated bed and print head
- 1 strip of case LEDs

That turns out to be a lot of parts, and a precarious mix of high power lines and low power signals all on one board. 

### System Design
Before designing a control board, I needed to decide which components the board needed to control. The first few decisions are relatively easy. We will need it to move in three axes. The extruder will need to be hot so that it can melt the filamtent before depositing it on the print bed. The print bed ought to be hot, but not too hot, to prevent the print from warping as it cooled. 

But then there are some unexpected parts that you might only recognize if you are familiar with 3D printers. Or, more precisely, if you are familiar with the many, many ways in which they can go wrong. With enough failed prints, you would ask:
- How can I ensure the motor that is driving the filament through the heated tip does not itself overheat?
    - A: An extruder fan
- How can I shut this down **immediately** if something goes bad?
    - A: Emergency power switch
- How does a 3D printer "know" where the print head is?
    - A: Using endstops to calibrate for the origin
- How can I see my cool print better while it is printing?
    - A: LEDs in your case
- Who is in charge of commands for our actuators?
    - A: The MCU, with control firmware

The firmware in this last point has a huge job. It turns out, almost all of our devices required different protocols to get them to work as intended, and many at different frequencies. In addition, there were lots of possible safety concerns for this project, from thermal runaway to power loss recovery. Not surprisingly, the firmware to manage all of these parts in near realtime is *very* complex, and I was not going to have time to write this by the end of the semester.

After reading around I found [Marlin](https://marlinfw.org/), an open-source firmware suite that was designed for running on 3D printer control boards. Even better, it was compatible with my favorite microcontroller board at the time, the NodeMCU ESP32. 

### Schematic Design
S

<swiper-container keyboard="true" navigation="true" pagination="true" pagination-clickable="true" pagination-dynamic-bullets="true" rewind="true">

  <swiper-slide>{% include figure.liquid loading="eager" path="assets/img/projects/rickety-3d-printer/control-board/Sheet_1.png" title="MCU schematic" class="img-fluid rounded z-depth-1" zoomable=true %}</swiper-slide>
  <swiper-slide>{% include figure.liquid loading="eager" path="assets/img/projects/rickety-3d-printer/control-board/Sheet_2 copy.png" title="Motor drivers schematic" class="img-fluid rounded z-depth-1" zoomable=true %}</swiper-slide>
  <swiper-slide>{% include figure.liquid loading="eager" path="assets/img/projects/rickety-3d-printer/control-board/Sheet_3 copy.png" title="Extruder drivers schematic" class="img-fluid rounded z-depth-1" zoomable=true %}</swiper-slide>
  <swiper-slide>{% include figure.liquid loading="eager" path="assets/img/projects/rickety-3d-printer/control-board/Sheet_4 copy.png" title="Thermistor and fans schematic" class="img-fluid rounded z-depth-1" zoomable=true %}</swiper-slide>
  <swiper-slide>{% include figure.liquid loading="eager" path="assets/img/projects/rickety-3d-printer/control-board/Sheet_5 copy.png" title="High power devices schematic" class="img-fluid rounded z-depth-1" zoomable=true %}</swiper-slide>
  <swiper-slide>{% include figure.liquid loading="eager" path="assets/img/projects/rickety-3d-printer/control-board/Sheet_6 copy.png" title="Signal input schematic" class="img-fluid rounded z-depth-1" zoomable=true %}</swiper-slide>

</swiper-container>
<div class="caption">
    A series of six schematics, together forming the full control board.
</div>



### PCB Design

#### PCB Testing

## The GCode Sender

You can also put regular text between your rows of images.
Say you wanted to write a little bit about your project before you posted the rest of the images.
You describe how you toiled, sweated, _bled_ for your project, and then... you reveal its glory in the next row of images.

<div class="row justify-content-sm-center">
    <div class="col-sm-8 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/projects/rickety-3d-printer/laser-cut_frame1.HEIC" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm-4 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/11.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    You can also have artistically styled 2/3 + 1/3 images, like these.
</div>

The code is simple.
Just wrap your images with `<div class="col-sm">` and place them inside `<div class="row">` (read more about the <a href="https://getbootstrap.com/docs/4.4/layout/grid/">Bootstrap Grid</a> system).
To make images responsive, add `img-fluid` class to each; for rounded corners and shadows use `rounded` and `z-depth-1` classes.
Here's the code for the last row of images above:

{% raw %}

```html
<div class="row justify-content-sm-center">
  <div class="col-sm-8 mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/6.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
  </div>
  <div class="col-sm-4 mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/11.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
  </div>
</div>
```

{% endraw %}
