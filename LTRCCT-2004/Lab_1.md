---
title: 'Adding Callback Number Read Back'
session: LTRCCT-2004
speaker: Kevin Simpson
---

## Table of Contents

# Introduction
In this lab we will be taking a starter flow and adding a callback number read back to confirm to the caller which number we should be calling them back at.

### Lab Objective



### Pre-requisites


# Lab Section

## Import the starter flow

1. Download the [Flow Template](flows/CL_1_start.json){:target="\_blank"}
   > The file will open in a separate window.  
   >
   > If using Firefox, Select the save option.
   >
   > <img src="images/saveJson.gif">
   >
   > If using Chrome or Edge, right click and select save.
   >
   ><img src="images/saveJsonChrome.gif" width="243">
   
      ---
2. Click Routing Strategy <img src="images/rsToFlow.gif" Align= "right" height="200">
3. Click on Flows in the top ribbon 
4. Click Import
5. Select flow_template
   
<br><br><br><br><br><br><br><br>

---

6. Click the ellipsis next to the newly imported flow_template and select Open 

    > <img src="images/openFlow.JPG" height="40">
    > 
    > Rename the flow to <w class="attendee_out">AttendeeID</w>_TechSummit by clicking on the pencil icon at the top of the screen, next to the flow name
    >
    > Click on the Play Message node
    >> Audio File: welcome.wav 
    >>
    >>---
    > 
    > Click on the Queue Contact node
    >> Select Static Queue
    >>
    >> Queue: Q_<w class="attendee_out">AttendeeID</w>
    >>
    >> ---
    >
    > Click on the Play Music node
    >> Select Static Audio File
    >>
    >> Music File: defaultmusic_on_hold.wav
    >>
    >> ---
    >
    > Click the Validation switch to turn on validation
    >
    > Click Publish Flow
    > 
    > Add a Publish Note of your choosing
    >
    > Click Publish Flow
    >
    > Click Return to Flow
    > 
    > Turn off Validation 
    >
    >   ---
