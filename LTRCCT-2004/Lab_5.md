---
title: 'Customizing the Wait Treatment by Business Unit'
session: LTRCCT-2004
speaker: Kevin Simpson
---

## Table of Contents

# Introduction
### Lab Objective
In this labe we will customize the number and content of wait treatment messages based on the business unit selection menu.


### Pre-requisites
- Complete Lab 0
- Complete Lab 1
- Complete Lab 2
- Complete Lab 4

# Lab Section


1. Create a new flow variables
   > Name: treatment
    >
    >> Type: JSON
    >>
    >> Default Value: \{"bUnit":"comfort","mCount":4\}
    >
    > ---
2. Edit Variable_Message
   > Audio Prompt Variable: \{\{treatment.bUnit\}\}\_{\{(count % treatment.mCount) + 1\}\}\_\{\{lang\}\}.wav
   >
   >
3. Delete the connection between salesService and Q_Sales
4. Delete the connection between salesService and QueueContact_ys9
5. Add a Set Variable node
   > Activity Name: salesTreat
   >
   > Variable Name: treatment
   >
   > Value: \{"bUnit":"sales","mCount":5\}
   >
6. Add a Set Variable node
   > Activity Name: serviceTreat
   >
   > Variable Name: treatment
   >
   > Value: \{"bUnit":"service","mCount":4\}
   >
7. Connect the Sales node edge from the salesService to salesTreat
8. Connect salesTreat to Q_Sales
9.  Connect the Service node edge from the salesService to serviceTreat
10. Connect serviceTreat to QueueContact_ys9

11. Publish your flow [Compare](images/CL_1_salesService_lang_treatment.jpg){:target="\_blank"}
12. Point your Entry Point to this new flow
13. Open the flow debugger and place a test call to <w class= "EPDN" >Your EP DN</w>
    > Test the flow in both Sales and Service (you don't need to test the callback portion).
    >
    >> Did you observe how the variables allowed the proper language files to be played?
    >>
    >> How would adjust this flow if you wanted to add more Sales or Service messages?
    >>
    >> Could you edit this flow to use a single Queue Contact node?
    >>
    >> Could you edit this flow to only allow callbacks for a specific business unit?
    >>

















<script>

if(localStorage.getItem("EPDN")){ Array.from(document.getElementsByClassName("EPDN")).forEach((index)=> {index.innerHTML = localStorage.getItem("EPDN")})} 

if(localStorage.getItem("agent1")){ Array.from(document.getElementsByClassName("agent1")).forEach((index)=> {index.innerHTML = localStorage.getItem("agent1")})} 

if(localStorage.getItem("agent2")){ Array.from(document.getElementsByClassName("agent2")).forEach((index)=> {index.innerHTML = localStorage.getItem("agent2")})} 

if(localStorage.getItem("PW")){ Array.from(document.getElementsByClassName("PW")).forEach((index)=> {index.innerHTML = localStorage.getItem("PW")})} 

if(localStorage.getItem("admin")){ Array.from(document.getElementsByClassName("admin")).forEach((index)=> {index.innerHTML = localStorage.getItem("admin")})} 

function mainPage() {window.location.href = "Lab_4";}
function nextLab() 
 {
 window.location.href = "Pause_4";
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