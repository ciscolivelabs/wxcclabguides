---
title: 'Menu to Select from 50 States'
session: LTRCCT-2004
speaker: Kevin Simpson
---

## Table of Contents
- [Introduction](#introduction)
    - [Lab Objective](#lab-objective)
    - [Pre-requisites](#pre-requisites)
- [Lab Section](#lab-section)
  - [Configure the BRE](#configure-the-bre)
  - [Create the flow](#create-the-flow)


# Introduction
### Lab Objective
In this lab we will be creating a new flow with an extensible menu to allow the caller to use their phones keypad to enter in a two digit state code and then pick from a list of states if there is are multiple matches.

### Pre-requisites
- Have a BRE table created for your tenant
- Import Audio Files from Lab 0

# Lab Section

## Configure the BRE

1. Navigate to the [BRE Configuration Tool](Configuring_The_BRE.md){:target="_blank"}
2. Use the following information to create the BRE rules
   > Your table name is states
   > Your key is st
3. Download this CSV and upload it to the BRE

## Create the flow
1.  In Routing Strategy > Flows
    > Click New
    >
    >> Flow name: CL_States
    >> 
    >> ---
2. Create New Flow Variables
    > Count
    >
    > Counter
    >
    > 
    >
    >
4. Add a Collect Digits node
    > 
    > Activity Name: CollectStateDigits
    >
    > Audio File: enter_state.wav
    >
    > Make the prompt interruptible 
    >
    > Minimum Digits: 2
    >
    > Maximum Digits: 2
    >
    > Connect Unmatched Entry to the front of CollectStateDigits
    >
    > Connect No-Input Timeout to the front of CollectStateDigits
    >
    > ---
5. Connect NewPhoneContact to CollectStateDigits
6. Add a BRE Request node
    > Activity Label: getStates
    >
    >> Use the instructions from the BRE Configuration Tool to configure this node
    >
    > ---
7. Connect CollectStateDigits to getStates
8. 






<script>
function mainPage() {window.location.href = "Lab_2";}
function nextLab() 
 {
 window.location.href = "Lab_4";
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