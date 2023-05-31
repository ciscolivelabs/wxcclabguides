---
title: 'Targeted Agent Routing'
session: LTRCCT-2004
speaker: Kevin Simpson
---

## Table of Contents

# Introduction
### Lab Objective
In this lab we will add the ability for a caller to queue to an exiting agent if they provide a valid ticket ID.  We will also allow them to receive a callback from their agent or opt-out to the main queue.
### Pre-requisites


# Lab Section
1. Create a new queue for reporting
   > Name: service_direct
   >
   > Call Distribution: Group1: CLTeam
   >
   > Service Level Threshold: 60
   >
   > Maximum Time in Queue: 600
   >
   > Default Music in Queue: defaultmusic_on_hold.wav
   >
   > ---

2. Create a new flow variables
   > Name: agentEmail
   >
   >> Type: String
   > 
   > Name: ticketID
   >
   >> Type: String
   >>
   >> Make Agent Viewable: True
   >>
   >> Desktop Label: Ticket ID
   >
   > Name: true
   >
   >> Type: String
   >>
   >> Value: true
   >
   > Name: toService
   >
   >> Type: Boolean
   >>
   >> Value = False
   >
   > ---

3. Delete the connection between serviceTreat and QueueContact_ys9 
4. Add a Collect Digits node
   > Activity Label: collectTicket
   >
   > Audio Prompt Variable: existing_ticket_\{\{lang\}\}.wav
   >
   > Make Prompt Interruptible: True
   >
   > Minimum Digits: 5
   >
   > Maximum Digits: 5
   >
   > Connect No-Input Timeout to QueueContact_ys9
   >
   > Connect Unmatched Entry to QueueContact_ys9
   >
   > ---

5. Connect serviceTreat to collectTicket
6. Add an HTTP Request node
   > Activity Label: getTicketInfo
   >
   > Use Authenticated Endpoint: False
   >
   > request URL: https://63f62bf859c944921f6e89de.mockapi.io/account
   > 
   > Method: GET
   >
   > Query Parameters:
   >
   >> KEY: ticketID VALUE: \{\{collectTicket.DigitsEntered\}\}
   >
   > Content Type: Application/JSON
   >
   > Parse Settings:
   >
   >> Content Type: JSON
   >>
   >> Output Variable: agentEmail
   >>
   >>> Path Expression: $[0].agentEmail
   >>
   >> Click Add New (under Output Variable)
   >>
   >> Output Variable: ticketID
   >>
   >>> Path Expression: $[0].ticketID
   >>
   >> ---

7. Connect collectTicket to getTicketInfo
8. Add a Queue To Agent node
   > Activity Label: QueueToOwner
   >
   > Agent Variable: agentEmail
   >
   > Agent Lookup Type: Email
   >
   > Set Contact Priority: True
   >
   > Static Priority: P5 (Priority 5)
   > 
   > Reporting Queue: direct_service
   >
   > Park Contact if Agent Unavailable: True
   >
   > Recovery Queue: Service
   >
   > ---

9. Connect getTicketInfo to QueueToOwner
10. Connect QueueToOwner to PlayMusic_b9x
11. Delete the Every_other
12. Select opt_out and click the copy button at the bottom of the canvas
    > Change Activity Label: opt_out_direct
    >
    > Change Audio Prompt Variable: opt_out_agent_\{\{lang\}\}.wav
    >
    > Digit Number 2: to service queue
    >
    > Connect Digit Number 1 node edge to SetVariable_07n
    >
    > Connect No-Input node edge to PlayMusic_b9x
    >
    > Connect Unmatched Entry node edge to PlayMusic_b9x
    >
    > ---

14. Add a Set Variable node
    > Activity Label: set_toService
    >
    > Variable: toService
    >
    > Value: True
    >
    > ---

15. Connect Digit Number 2 node edge from opt_out_direct to set_toService
16. Connect the error node edge from QueueToOwner to set_toService
17. Connect set_toService to QueueContact_ys9
18. Add a new Case node
    > Activity Name: cbTreat
    >
    > Build Expression: true
    >
    > Link Description:
    >>
    >> \{\{count is even and toService\}\}
    >>
    >>> Connect node edge to SetVariable_07n
    >>
    >> \{\{count is even and ticketID.length == 5\}\}
    >>
    >>> Connect node edge to opt_out_direct
    >>
    >> \{\{count is even\}\}
    >>
    >>> Connect node edge to SetVariable_07n
    >> 
    >> Connect Default node edge to PlayMusic_b9x
    >
    > ---
19. Publish your flow [Compare](images/CL_1_salesService_lang_treatment_agentRouting.jpg){:target="\_blank"}

### Test Your Flow
1. Call <w class="EPDN">your EP DN</w> and select Service
2. When prompted enter <w class="TicketID">your ticket ID<w/>
3. Select call back from agent.
   - Did the callback get queued to the agent?
  
4. Repeat steps 1 and 2, but this time drop to the queue
   - How did the opt-out menu change?
  
5. What happens if you enter in a non matching Ticket ID?

6. Try with the different language option.
















<script>
if(localStorage.getItem("EPDN")){ Array.from(document.getElementsByClassName("EPDN")).forEach((index)=> {index.innerHTML = localStorage.getItem("EPDN")})} 

if(localStorage.getItem("TicketID")){ Array.from(document.getElementsByClassName("TicketID")).forEach((index)=> {index.innerHTML = localStorage.getItem("TicketID")})} 

function mainPage() {window.location.href = "Lab_5";}
function nextLab() 
 {
 window.location.href = "Pause_5";
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