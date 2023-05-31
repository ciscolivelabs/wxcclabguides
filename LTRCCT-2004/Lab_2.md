---
title: 'Reusing Our Existing Wait Treatment and Opt-out'
session: LTRCCT-2004
speaker: Kevin Simpson
---

## Table of Contents
- [Introduction](#introduction)
    - [Lab Objective](#lab-objective)
    - [Pre-requisites](#pre-requisites)
- [Lab Section](#lab-section)
    - [Add an additional queue](#add-an-additional-queue)
    - [Add Functionality to Flow](#add-functionality-to-flow)


# Introduction

### Lab Objective
In this lab you will be adding a menu to select different business units which will utilize different queues but will reuse the same wait treatment.

Feel free to reference the [Cheat Sheet](cheatSheet.md){:target="_blank"} along the way if you are not sure of how to navigate a step.

### Pre-requisites
- Complete Lab 0
- Complete Lab 1

# Lab Section

### Add an additional queue

1. Create a queue  
    >Name: Sales
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
    >> Select CLTeam
    >>
    >> Save Group
    >>
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
    >
    > ---

### Add Functionality to Flow

1. Add a new Menu node
    > Activity Label: salesService
    >
    > Audio File: salesServiceMenu.wav
    >
    > Make Prompt Interruptible: True
    >
    > Digit Number: 1 Link Description: Sales
    >
    > Digit Number: 2 Link Description: Service
    >
    > Connect No-Input Timeout to the front of the salesService node
    >
    > Connect Unmatched Entry to the front of the salesService node


2. Delete the connection from PlayMessage_oc2 to QueueContact_ys9
3. Connect PlayMessage_oc2 to salesService
4. Add a new Queue Contact node
    > Activity Name: Q_Sales
    >
    > Static Queue
    >
    > Queue: Sales
    >
    > ---
5. Connect the Sales node edge of salesService to the Q_Sales node
6. Connect the Service node edge of salesService to the QueueContact_ys9 node
7. Connect the Q_Sales node to the PlayMusic_b9x node
   
    ---
8. Publish your flow [Compare](images/CL_1_salesService.jpg){:target="\_blank"}
9. Place a test call to <w class= "EPDN" >Your EP DN</w>
    > Test the flow
    >> Were you able to set a callback for the queue which was chosen in the menu?

    ---



<script>
if(localStorage.getItem("EPDN")){ Array.from(document.getElementsByClassName("EPDN")).forEach((index)=> {index.innerHTML = localStorage.getItem("EPDN")})} 

if(localStorage.getItem("agent1")){ Array.from(document.getElementsByClassName("agent1")).forEach((index)=> {index.innerHTML = localStorage.getItem("agent1")})} 

if(localStorage.getItem("agent2")){ Array.from(document.getElementsByClassName("agent2")).forEach((index)=> {index.innerHTML = localStorage.getItem("agent2")})} 

if(localStorage.getItem("PW")){ Array.from(document.getElementsByClassName("PW")).forEach((index)=> {index.innerHTML = localStorage.getItem("PW")})} 

if(localStorage.getItem("admin")){ Array.from(document.getElementsByClassName("admin")).forEach((index)=> {index.innerHTML = localStorage.getItem("admin")})} 
function mainPage() {window.location.href = "Lab_1";}
function nextLab() 
 {
 window.location.href = "Pause_1";
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