---
title: 'Preparing and validating your lab'
session: LTRCCT-2004
speaker: Kevin Simpson
---

## Table of Contents
- [Introduction](#introduction)
    - [Lab Objective](#lab-objective)
    - [Pre-requisites](#pre-requisites)
- [Lab Section](#lab-section)
    - [Log in](#log-in)
    - [Bulk import audio files](#bulk-import-audio-files)
    - [Launch the Contact Center Portal](#launch-the-contact-center-portal)
    - [Configure your teams](#configure-your-teams)
    - [Configure your users](#configure-your-users)
    - [Create a queues](#create-a-queues)
    - [Create your first flow](#create-your-first-flow)
    - [Create your Entry Point](#create-your-entry-point)
    - [Create your Entry Point mapping](#create-your-entry-point-mapping)
    - [Test your configuration](#test-your-configuration)


# Introduction
 In this lab we be be ensuring that we are set for success by configuring our testing agents, setting up our queues and teams as well as validating our testing numbers with a testing flow.

### Lab Objective

### Pre-requisites


# Lab Section

### Log in 
1. Open the [Control Hub](https://admin.webex.com/){:target="\_blank"} in your browser
2. Click Contact Center in the left frame
3. Click settings in the top ribbon
   
<img src="images/CH_Settings.jpg">

4. Click Synchronize Users

### Bulk import audio files

1. Download the lab audio file using this link [Audio Files](files/CL_Audio1.zip){:target="\_blank"}
2. Click Bulk Operations in the top ribbon 
3. Click Create Bulk Operation
4. Select Audio Files from the drop down
5. Drag the zip file to the import box or brows for the zip file
6. Click Next

### Launch the Contact Center Portal
1. Click Settings in the top ribbon
2. Click the Go to Webex Contact Center Management Portal link at the bottom of the page

### Configure your teams
1. Navigate to **_Provisioning_** and select **_Team_**.
2. Click on `+ New Team`.
3. Select you site from the _Site_ drop-down.
4. Input _Name_ as **<w class = "attendee-class">your_attendee_ID</w>\_Team1**.
5. Use the default **_Type_** `Agent Based`.
6. Select your MMP in the _Multimedia Profile_ drop-down.
7. Left as a default value **_Global Layout_** in the **_Desktop Layout_** drop-down and **_Save_** the configuration.


### Configure your users
1. Click on Provisioning and select Users.
2. Click on ... for the agent, to launch the Edit view for a particular User configuration.

3. Click on Contact Center Enabled toggle to move it to On.

4. In the Agent Settings section, select your site in the Site drop-down.

5. Click the Teams area and select your team1

6. Select the default Agent-Profile in the Agent Profile drop-down list.

7. Choose the Multimedia Profile and hit Save.







### Create a queues
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
   > <details> <summary>If using Firefox, Select the save option.</summary>
   >
   > <img src="images/saveJson.gif">
   >
   > </details>
   >
   > <details> <summary>If using Chrome or Edge, right click and select save.</summary>
   >
   ><img src="images/saveJsonChrome.gif" width="243">
   >
   > </details>
      ---
2. <details> <summary>Click Routing Strategy</summary>
    
   <img src="images/rsToFlow.gif" height="200">

   </details>

3. Click on Flows in the top ribbon 
4. Click Import
5. Select flow_template
6. <details> <summary>Click the ellipsis next to the newly imported flow_template and select Open </summary>
    <img src="images/openFlow.JPG" height="40">
    
    </details>
   

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

1. Click on Provisioning > Entry Points/Queues > Entry point [Show Me](images/openEP.gif){:target="_blank"}
2. Click Create new Entry point 
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



1. Click on Provisioning > Entry Point Mapping [Show Me](images/openEPmap.gif){:target="\_blank"}
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


<script>
function mainPage() {window.location.href = "Home";}
function nextLab() 
 {
 window.location.href = "Lab_1";
 }
</script>

<div id="button-row">
<button onclick="mainPage()" style="
  border-radius: 5px;
  background-color: rgb(116,191,75);
  padding: 10px;">Go To Previous Lab</button>

<button onclick="nextLab()" style="
  position: absolute;
  right: 200px;
  border-radius: 5px;
  background-color: rgb(116,191,75);
  padding: 10px;">Go to the Next Lab</button>

</div>