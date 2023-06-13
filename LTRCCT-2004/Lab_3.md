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

### Configure the BRE

1. Navigate to the [BRE Configuration Tool](Configuring_The_BRE.md){:target="_blank"}
2. Use the following information to create the BRE rules
   > Your table name is states
   >
   > Your key is st

3. Download [this CSV](files/statelookup.csv){:target="_blank"} and upload it to the BRE

### Create the flow
1.  In Routing Strategy > Flows
    > Click New
    >
    >> Flow name: CL_States
    >> 
    >> ---
2. Create New Flow Variables
    > Name: count
    >
    >> Type: Integer
    >>
    >> Default Value: 0
    >
    > ---
    >
    > Name: counter
    >
    >> Type: Integer
    >>
    >> Default Value: 0
    >
    > ---
    >
    > Name: selectInt
    > 
    >> Type: Integer
    >>
    >> Default Value: 0
    >
    > ---
    >
    > Name: list
    >
    >> Type: String
    >>
    >
    > ---
    >
    > Name: state
    >
    >> Type: String
    >>
    >
    > ---

3. Add a Collect Digits node
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

4. Connect NewPhoneContact to CollectStateDigits
5. Add a BRE Request node
    > Activity Label: getStates
    >
    >> Use the instructions from the BRE Configuration Tool to configure this node
    >>
    >> Substitute "your lookup value" with  \{\{CollectStateDigits.DigitsEntered\}\}
    >>
    >> Substitute "YourVariable" with list
    >>
    >
    > ---

6. Connect CollectStateDigits to getStates
7. Add a Set Variable node
    > Activity name listCount
    >
    > Variable: count
    >
    > Set to Value: \{\{list \| split(",") \|length\}\}
    >
    > ---

8. Connect getStates to listCount
9.  Add a Condition node
    > Activity Name: singleMatchCheck
    >
    > Expression: \{\{count < 2\}\}
    >
    > ---

10. Connect listCount to singleMatch

11. Add a Set Variable node
    > Activity Name: singleState
    >
    > Variable: state
    >
    > Set to Value: \{\{list\}\}
    >
    > ---


12. Connect the True node edge of singleMatchCheck to singleState

13.  Add a Set Variable node
    > Activity Name: incrementCounter
    >
    > Variable: count
    >
    > Set to Value: \{\{counter + 1\}\}
    >
    > --- 

14. Connect the False node edge of singleMatchCheck to incrementCounter

15. Add a Set Variable node
    > Activity name: stateName
    >
    > Variable: state
    >
    > Set to Value: \{\{list \| split(",",list \| split(",") \| length-(list \| split(",") \| length-counter)) \|last \| split(",") \| first\}\}
    >
    > ---

16. Connect incrementCounter to stateName

16. Add a Menu node
    > Activity Label: selectState
    >
    > Audio File: Press.wav
    >
    > Audio Prompt Variable: \{\{counter\}\}.wav
    >
    > Audio File: for.wav
    >
    > Audio Prompt Variable: \{\{state\}\}.wav
    > 
    > Make Prompt Interruptible: True
    >
    > Digit Number: 1 Link Description: 1
    >
    > Digit Number: 2 Link Description: 2
    >
    > Digit Number: 3 Link Description: 3
    >
    > Digit Number: 4 Link Description: 4
    >
    > ---
   
17. Connect stateName to selectState
    

19. Add a Condition node
    > Activity Name: listComplete
    >
    > Expression: \{\{counter < count\}\}
    >
    > ---

20. Add a Set Variable node
    > Activity Name: resetCounter
    >
    > Variable: counter
    >
    > Set to Value: 0
    >
    > ---

21. Connect the True node edge of listComplete to the incrementCounter node
22. Connect the False node edge of listComplete to resetCounter node
23. Connect resetCounter to incrementCounter ⚠️ In a production environment you would want to limit the number of times you let this menu loop.
24. Connect No-Input Timeout node edge to the listComplete node
25. Connect Unmatched Entry node edge to the listComplete node    
26. Add a Set Variable node
    > Activity Name: stateFromListPos
    >
    > Variable: selectInt
    >
    > Set to Value: \{\{selectState.OptionEntered\}\}
    >
    > ---
27. Connect Node edges 1, 2, 3, and 4 from selectState to stateFromListPos

28. Add a Set Variable node
    > Activity Name: stateFromList
    >
    > Variable: state
    >
    > Set to Value: \{\{list \| split(",",list \| split(",") \| length-(list \| split(",") \| length-selectInt)) \| last \| split(",") \| first\}\}
    >
    > ---
29. Connect stateFromListPos to stateFromList

30. Add a Queue Contact node
    > Activity Name: queueCaller
    >
    > Static Queue
    >
    > Queue: Service
    >
    > ---
31. Connect stateFromList to queueCaller node
32. Connect singleState to queueCaller node
33. Add a Play Music node
    > Activity Name: PlayMusic
    >
    > Static Audio File
    >
    > Music File: defaultmusic_on_hold.wav
    >
    > ---
34. Connect queueCaller to PlayMusic
35. Loop the output of PlayMusic to the input of PlayMusic
36. Publish your flow [Compare](images/CL_1_salesService.jpg){:target="\_blank"}
37. Point your Entry Point to this new flow
38. Open the flow debugger and place a test call to <w class= "EPDN" >Your EP DN</w>
    > What happens when you enter 63?
    >
    > What happens if you enter 43?



<script>
if(localStorage.getItem("EPDN")){ Array.from(document.getElementsByClassName("EPDN")).forEach((index)=> {index.innerHTML = localStorage.getItem("EPDN")})} 

if(localStorage.getItem("agent1")){ Array.from(document.getElementsByClassName("agent1")).forEach((index)=> {index.innerHTML = localStorage.getItem("agent1")})} 

if(localStorage.getItem("agent2")){ Array.from(document.getElementsByClassName("agent2")).forEach((index)=> {index.innerHTML = localStorage.getItem("agent2")})} 

if(localStorage.getItem("PW")){ Array.from(document.getElementsByClassName("PW")).forEach((index)=> {index.innerHTML = localStorage.getItem("PW")})} 

if(localStorage.getItem("admin")){ Array.from(document.getElementsByClassName("admin")).forEach((index)=> {index.innerHTML = localStorage.getItem("admin")})} 
function mainPage() {window.location.href = "Lab_2";}
function nextLab() 
 {
 window.location.href = "Pause_2";
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