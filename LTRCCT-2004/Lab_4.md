---
title: 'Making the Flow Multilingual'
session: LTRCCT-2004
speaker: Kevin Simpson
---

## Table of Contents

# Introduction
### Lab Objective
In this lab we will enable our flow to be multilingual by using variable audio prompts with structured file names.

### Pre-requisites
- Complete Lab 0
- Complete Lab 1
- Complete Lab 2

# Lab Section
### Bulk import audio files

1. Download the lab audio file using this link [Audio Files](files/CL_Audio2.zip){:target="_blank"}
2. Click Bulk Operations in the top ribbon 
3. Click Create Bulk Operation
4. Select Audio Files from the drop down
5. Drag the zip file to the import box or brows for the zip file
6. Click Next

### Edit CL_1_Start

1. Create a new flow variable
   > Name: lang
    >
    >> Type: string
    >>
    >> Default Value: EN
    >
    > ---

2. Delete the connection between PlayMessage_oc2 and salesService
3. Add a Menu node
   > Activity Name: lang_menu
   >
   > Audio File: 2_for_spanish.wav
   >
   > Make Prompt Interruptible: True
   >
   > Digit Number: 2 Link Description: Spanish
   > 
   > Connect the No-Input Timeout node edge to salesService
   >
   > Connect the Unmatched Entry node edge to salesService
   >
   > ---

4. Add a Set Variable node
   > Activity Name: set_ES
   >
   > Variable: lang
   >
   > Value: ES
   >
   > ---

5. Connect PlayMessage_oc2 to lang_menu
6. Connect the Spanish node edge of lang_menu to set_ES
7. Connect set_ES to salesService
8. Edit salesService
   > Change from Audio File to Audio Prompt Variable
   >
   >> Click Add Audio prompt Variable
   >>
   >> Audio Prompt Variable: salesServiceMenu_\{\{lang\}\}.wav
   >>
   >> Delete Audio File dropdown
   >
   > ---

9.  Edit Variable_Message
    >  
    > Audio Prompt Variable: comfort_\{\{(count % 4) + 1\}\}\_\{\{lang\}\}.wav
    >
    > ---

10. Edit opt_out
    > Change from Audio File to Audio Prompt Variable
    >
    > Audio Prompt Variable: opt_out_\{\{lang\}\}.wav
    >
    > ---

11. Edit cfrom
    > Change from Audio File to Audio Prompt Variable
    >
    > Audio Prompt Variable: calling_from_\{\{lang\}\}.wav
    >
    > ---

12. Edit playDigit
    > Update Audio Prompt Variable
    >
    > Audio Prompt Variable: \{\{rDigit\}\}\_\{\{lang\}\}.wav
    >
    > ---

13. Edit confirmNumber
    > Change from Audio File to Audio Prompt Variable
    >
    > Audio Prompt Variable: number_confirm_\{\{lang\}\}.wav
    >
    > ---
    
14. Edit newNumber
    > Change from Audio File to Audio Prompt Variable
    >
    > Audio Prompt Variable: new_number_\{\{lang\}\}.wav
    >
    > ---
    
15. Edit rcontext
    > Change from Audio File to Audio Prompt Variable
    >
    > Audio Prompt Variable: entered_\{\{lang\}\}.wav
    >
    > ---
    
16. Edit PlayMessage_s4p
    > Change from Audio File to Audio Prompt Variable
    >
    > Audio Prompt Variable: callback_confirm_\{\{lang\}\}.wav
    >
    > ---
    



17. Publish your flow [Compare](images/CL_1_salesService_lang.jpg){:target="\_blank"}
18. Point your Entry Point to this new flow
19. Open the flow debugger and place a test call to <w class= "EPDN" >Your EP DN</w>
    > Test the flow in both languages.
    >
    >> Did you observe how the variables allowed the proper language files to be played?

<script>

if(localStorage.getItem("EPDN")){ Array.from(document.getElementsByClassName("EPDN")).forEach((index)=> {index.innerHTML = localStorage.getItem("EPDN")})} 

if(localStorage.getItem("agent1")){ Array.from(document.getElementsByClassName("agent1")).forEach((index)=> {index.innerHTML = localStorage.getItem("agent1")})} 

if(localStorage.getItem("agent2")){ Array.from(document.getElementsByClassName("agent2")).forEach((index)=> {index.innerHTML = localStorage.getItem("agent2")})} 

if(localStorage.getItem("PW")){ Array.from(document.getElementsByClassName("PW")).forEach((index)=> {index.innerHTML = localStorage.getItem("PW")})} 

if(localStorage.getItem("admin")){ Array.from(document.getElementsByClassName("admin")).forEach((index)=> {index.innerHTML = localStorage.getItem("admin")})} 

function mainPage() {window.location.href = "Lab_3";}
function nextLab() 
 {
 window.location.href = "Pause_3";
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