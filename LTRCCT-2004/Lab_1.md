---
title: 'Adding Callback Number Read Back'
session: LTRCCT-2004
speaker: Kevin Simpson
---

## Table of Contents

# Introduction


### Lab Objective
In this lab we will be taking a starter flow and adding a callback number read back to confirm to the caller which number we should be calling them back at.

Feel free to reference the [Cheat Sheet](cheatSheet.md){:target="\_blank"} along the way if you are not sure of how to navigate a step.


### Pre-requisites
- Complete Lab0

# Lab Section

## Import the starter flow

1. Download the [CL_1_start Flow Template](flows/CL_1_start.json){:target="\_blank"}
2. Click Routing Strategy
3. Click on Flows in the top ribbon 
4. Click Import
5. Select CL_1_start
---

1. Click the ellipsis next to the newly imported flow_template and select Open 
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
   > Audio File: opt_out_English.wav
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
    > Prompt: number_confirm_English.wav
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
   > Audio File: new_number_English.wav
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