---
title: 'Adding Callback Number Read Back'
session: LTRCCT-2004
speaker: Kevin Simpson
---

## Table of Contents
- [Introduction](#introduction)
    - [Lab Objective](#lab-objective)
    - [Pre-requisites](#pre-requisites)
- [Lab Section](#lab-section)
  - [Import the starter flow](#import-the-starter-flow)
  - [Creating an opt-out option with ANI readout](#creating-an-opt-out-option-with-ani-readout)
  - [Adding the ability to receive a callback at a different number](#adding-the-ability-to-receive-a-callback-at-a-different-number)

# Introduction


### Lab Objective
In this lab we will be taking a starter flow and adding a callback number read back to confirm to the caller which number we should be calling them back at.

Feel free to reference the [Cheat Sheet](cheatSheet.md){:target="_blank"} along the way if you are not sure of how to navigate a step.


### Pre-requisites
- Complete Lab0

# Lab Section

## Import the starter flow

1. Download the [CL_1_start Flow Template](flows/CL_1_start.json){:target="_blank"}
2. Import the flow
3. Click the ellipsis next to the newly imported flow_template and select Open 
   > 
   >
   > Click on the Play Message node
   >> Audio File: welcome.wav 
   >>
   >>---
   > 
   > Click on the Queue Contact node
   >> Select Static Queue
   >>
   >> Queue: Service
   >>
   >> ---
   >
   > Click on the Play Music node
   >> Select Static Audio File
   >>
   >> Music File: defaultmusic_on_hold.wav
   >>
   >> Music Duration: 2 seconds
   >
   > Click on the Variable Message node
   >
   >> Click the Add Audio prompt Variable button
   >>
   >> Delete the Audio File drop down
   >>
   >> Audio prompt Variable: comfort_\{\{(count % 4) + 1\}\}.wav
   >>
   >>> Click the blue Test Expression button in the lower right corner of the Audio Prompt Variable box
   >>>
   >>> Put 0 in the count box
   >>>
   >>> Do you see the result of "comfort_1.wav"?
   >>>
   >>> What happens when you put other numbers in the count box?  Try 4 and 5...
   >>>
   >>> Click Close
   >>
   > Click the opt_out node
   >
   >> Audio File: opt_out.wav
   >>
   >> Select Make Prompt Interruptible
   >>
   >> Connect the Unmatched Entry node edge to the front of the PlayMusic node
   >>
   > Click PlayMessage_s4p node
   >>
   >> Audio File: callback_confirm
   >>
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
   > Edit your Entrypoint to point to CL_1_start
   >
   > Call your EP DN and test the flow
   >
   > ---




## Creating an opt-out option with ANI readout
1. Create new flow variables:
   > Name: callbackANI
   >> Type: String
   >>
   >> No default value
   >
   > ---
   >
   > Name: rDigit
   >> Type: string
   >>
   >> No default value
   >
   > ---
   >
   > Name: sPosition
   >> Type: Integer
   >>
   >> Default Value: 0
   >>
   ---
2. Delete the connection from the websiteMessage node to Play Music
3. Drag a Menu node onto the canvas
   > Activity Label: callback_opt
   >
   > Audio File: opt_out.wav
   >
   > Make Prompt Interruptible: True
   >
   > Digit Number: 1 Link Description: optOut 
   >
   > Connect the No-Input Timeout node edge to Play Music
   >
   > Connect the Unmatched Entry node edge to Play Music
   >
   > ---
4. Connect the websiteMessage to the callback_opt node
5. Add a Set Variable node
   > Activity Label: callbackANI_set
   >
   > Select Variable: callbackANI
   >
   > Set to Value: \{\{NewPhoneContact.ANI \| slice (NewPhoneContact.ANI.length -10,NewPhoneContact.ANI.length)\}\}
   >
   ---
6. Connect the callback_opt optOut node edge to callbackANI_set 
7. Add a Play Message Node
   > Activity Label: cfrom
   >
   > Audio File: calling_from_English.wav
   >
   > ---
8. Connect callbackANI_set to cfrom
9. Add a Set Variable node
   > Activity Label: rDigit_set
   >
   > Select Variable: rDigit
   >
   > Set to Value: \{\{callbackANI \| slice (sPosition,sPosition+1)\}\}
   >
   ---

10. Connect cfrom to rDigit_set
11. Add a Play Message node
   > Activity Label: playDigit 
   >
   > Click Add Audio Prompt Variable
   >> Audio Prompt Variable: \{\{rDigit\}\}_English.wav
   >>
   >> Delete the Audio File Drop Down
   >> 
   >> ---
12. Connect rDigit_set to playDigit
13. Add a Set Variable node
    > Activity Label: advance
    >
    > Select Variable: sPosition
    >
    > Set to Value: \{\{sPosition+1\}\}
    >
   ---
14. Connect playDigit to advance
15. Add a Condition node
    > Activity Label: positionCheck
    > 
    > Condition: \{\{sPosition <= (callbackANI.length -1) \}\}
    >
    > True: Connect to rDigit_set 
    >
    > False: Add a new Disconnect Contact node and connect it here
    >
   ---
16. Connect advance to positionCheck  
17. Publish your flow [Compare](https://webexcc.github.io/../../../assets/images/IVR/aniRead.JPG){:target="\_blank"}
18. Place a test call to <w class= "DN_out" >Your EP DN</w>
    > When you are given the option for a callback, press 1.
    >> Did you hear your 10 digit callback number being read back?

    ---



## Adding the ability to receive a callback at a different number
1. Add a new Menu node
    > Activity Label: confirmNumber
    >
    > Prompt: number_confirm.wav
    >
    > Make Prompt Interruptible: True
    >
    > Digit Number: 1 Link Description: confirm number
    >
    > Digit Number: 2 Link Description: change number
    >
    > Connect No-Input Timeout to the front of the confirmNumber node
    >
    > Connect Unmatched Entry to the front of the confirmNumber node
    >
    > ---
2. Delete the False node edge from positionCheck to Disconnect Contact
3. Connect the False node edge from positionCheck to confirmNumber
4. Connect the confirm number node edge to Disconnect Contact
5. Add a Collect Digits node
   > Activity Label: newNumber 
   >
   > Audio File: new_number.wav
   >
   > Make Prompt Interruptible: True
   >
   > Minimum Digits: 10
   >
   > Maximum Digits: 10
   >
   > Connect No-Input Timeout to the front of the newNumber node
   >
   > Connect Unmatched Entry to the front of the newNumber node
   >
   > ---
6. Connect the change number node edge to newNumber
7. Add a Set Variable Node
   > Activity Label: newCB
   >
   > Variable: callbackANI
   >
   > Set Value: \{\{newNumber.DigitsEntered\}\}
   >
   > ---
8. Connect newNumber to newCB
9.  Add a Set Variable Node
    > Activity Label:resetPosition
    >
    > Variable: sPosition
    >
    > Set Value: 0
    >
    > ---
10. Connect newCB to resetPosition
11. Add a Play message node
    > Activity Label: rcontext
    > 
    > Audio File: entered_English.wav
    >
    > ---
12. Connect resetPosition to rcontext
13. Connect rcontext to rDigit_set
14. Publish your flow [Compare](https://webexcc.github.io/../../../assets/images/IVR/changeNumber.JPG){:target="\_blank"}
15. Place a test call to <w class= "DN_out" >Your EP DN</w>
    > When you are given the option for a callback, press 1.
    >
    > Press 2 to enter a different number.
    >> Did you hear your 10 digit callback number being read back?
    >>
    >> Did you hear the number you entered read back?

    ---




<script>
function mainPage() {window.location.href = "Lab_0";}
function nextLab() 
 {
 window.location.href = "Lab_2";
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