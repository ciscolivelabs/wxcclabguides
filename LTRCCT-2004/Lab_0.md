---
title: 'Preparing and validating your lab'
session: LTRCCT-2004
speaker: Kevin Simpson
---

## Table of Contents

# Introduction
 In this lab we be be ensuring that we are set for success by configuring our testing agents, setting up our queues and teams as well as validating our testing numbers with a testing flow.

### Lab Objective

### Pre-requisites


# Lab Section

### Configure your users



### Bulk import audio files

1. Download the lab audio file using this link [Audio Files](https://webexcc.github.io/assets/files/lab_wav.zip){:target="\_blank"}
2.  


### Create a queue
1. Click on Provisioning > Entry Points/Queues > Queue
    > <img src="images/openQueue.gif">
    ---
2. Click New Queue
    > Name your queue Q_<w class="attendee_out">AttendeeID</w>
    >
    > Description: optional
    >
    > Channel Type: Telephony
    >
    > Queue Routing Type: Longest Available Agent
    > 
    > Call Distribution:
    >> Click Add Group
    >>
    >> Select <w class="attendee_out">Your_Attendee_ID</w>_Team1
    >>
    >> Save Group
    >>
    >> Create second group
    >>
    >> Select <w class="attendee_out">Your_Attendee_ID</w>_Team2
    >>
    >> After: 60 Seconds in queue
    >>
    >> Add Group as: Last
    >>
    >> Save Group
    >>
    >> Click Close
    >
    > ---
    >
    > Service Level Threshold: 60
    >
    > Maximum Time in Queue: 600
    >
    > Default Music in Queue: defaultmusic_on_hold.wav
    >
    > Save

    ---

### Create your first flow
1. Download the [Flow Template](flows/flow_template.json){:target="\_blank"}
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

6. Click the ellipsis next to the newly imported flow_template and select Open 
   > <img src="images/openFlow.JPG" height="40">
   > 
   > Rename the flow to <w class="attendee_out">AttendeeID</w>_TechSummit by clicking on the pencil icon at the top of the screen, next to the flow name
   >
   > Click on the Play Message node
   >> Audio File: welcome.wav 
   >
   > ---
   > Click on the Queue Contact node
   >> Select Static Queue
   >>
   >> Queue: Q_<w class="attendee_out">AttendeeID</w>
   >>
   > ---
   >
   > Click on the Play Music node
   >> Select Static Audio File
   >>
   >> Music File: defaultmusic_on_hold.wav
   >>
   >  ---
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

    ---



### Create your Entry Point

1. Click on Provisioning > Entry Points/Queues > Entry point
2. Click Create new Entry point [Show Me](https://webexcc.github.io/../../../assets/images/IVR/openEP.gif){:target="\_blank"}
    > Name your Entry Point EP_<w class="attendee_out">AttendeeID</w>
    >
    > Description: optional
    >
    > Channel Type: telephony
    >
    > Service Level Threshold: 60
    >
    > Flow: <w class="attendee_out">AttendeeID</w>_TechSummit
    >
    > Music on Hold: defaultmusic_on_hold.wav
    >
    > Click Save
    >
    > ---

### Create your Entry Point mapping



1. Click on Provisioning > Entry Point Mapping [Show Me](https://webexcc.github.io/../../../assets/images/IVR/openEPmap.gif){:target="\_blank"}
2. Click new mapping
    > In location, select "Office"
    >
    > In Available Numbers select <w class= "DN_out" >Your EP DN</w>
    >
    > In Entry point select EP_<w class="attendee_out">AttendeeID
    >
    > Click Save
    >
    > ---


### Test your configuration
1. Call <w class= "DN_out" >Your EP DN</w> from your supervisor extension
    > You should hear the greeting message and then the music in queue
    >
    > Go available in the agent desktop
    >> The call should be delivered to your agent extension
    >
    > End the call, Wrap-up, and Go unavailable
    >
    > ---
