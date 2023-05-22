---
title: 'Customizing the wait treatment by business unit'
session: LTRCCT-2004
speaker: Kevin Simpson
---

## Table of Contents

# Introduction
### Lab Objective

### Pre-requisites


# Lab Section


1. Create a new flow variables
   > Name: treatment
    >
    >> Type: JSON
    >>
    >> Default Value: \{"bUnit":"comfort","mCount":4\}
    >
    > ---
    
2. Delete the connection between salesService and Q_Sales
3. Delete the connection between salesService and QueueContact_ys9
4. Add a Set Variable node
   > Activity Name: salesTreat
   >
   > Variable Name: treatment
   >
   > Value: \{"bUnit":"sales","mCount":5\}
   >
5. Add a Set Variable node
   > Activity Name: serviceTreat
   >
   > Variable Name: treatment
   >
   > Value: \{"bUnit":"service","mCount":4\}
   >
6. Connect the Sales node edge from the salesService to salesTreat
7. Connect salesTreat to Q_Sales
8. Connect the Service node edge from the salesService to serviceTreat
9. Connect serviceTreat to QueueContact_ys9

10. Publish your flow [Compare](images/CL_1_salesService_lang_treatment.jpg){:target="\_blank"}
11. Point your Entry Point to this new flow
12. Open the flow debugger and place a test call to <w class= "DN_out" >Your EP DN</w>
    > Test the flow in both Sales and Service (you don't need to test the callback portion).
    >
    >> Did you observe how the variables allowed the proper language files to be played?
    >>
    >> How would adjust this flow if you wanted to add more Sales or Service messages?
    >>
    >> Could you edit this flow to use a single Queue Contact node?

















<script>
function mainPage() {window.location.href = "Lab_4";}
function nextLab() 
 {
 window.location.href = "Lab_6";
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