---
title: 'Making the flow multilingual'
session: LTRCCT-2004
speaker: Kevin Simpson
---

## Table of Contents

# Introduction
### Lab Objective

### Pre-requisites
- Complete Lab 0
- Complete Lab 1
- Complete Lab 2

# Lab Section
### Bulk import audio files

1. Download the lab audio file using this link [Audio Files](files/CL_Audio2.zip){:target="\_blank"}
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
    > ---

2. Delete the connection between 
3. Add a Menu node
   >
   >
   >
4. Connect
5. Connect
6. Edit 
7. Edit
8. Edit



31. Publish your flow [Compare](images/CL_1_salesService.jpg){:target="\_blank"}
32. Point your Entry Point to this new flow
33. Open the flow debugger and place a test call to <w class= "DN_out" >Your EP DN</w>
    > What happens when you enter 63?
    >
    > What happens if you enter 43?


<script>
function mainPage() {window.location.href = "Lab_3";}
function nextLab() 
 {
 window.location.href = "Lab_5";
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