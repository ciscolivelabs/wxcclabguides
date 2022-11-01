---
title: 'Lab Pre-requisites'
---

# Table of Contents

- [Lab Topology](#lab-topology)
- [Access URLs](#access-urls) 
- [Before starting the labs](#before-starting-the-labs)
- [Lab Support](#lab-support)

# Introduction
Digital channels are now more impactful than ever. 
These labs are specially designed for the Cisco Live session. The primary purpose of the labs is to give a clear understanding of New Digital Channels functionality. You will learn how to create and configure Webchat and SMS. Using the debug console, you will also get a clear understanding of troubleshooting issues.


## Lab Topology
<img align="middle" src="images/topology.png" width="1000" />

## Access URLs

| Component     | URL                     | Login                                                       |
| --------------- | ----------------------------------------- | -------------------------------------------------------------           |
| Webex CC Control Hub | [https://admin.webex.com](https://admin.webex.com){:target="_blank"} | cladmin**\<ID\>**@email.carehybrid.com |
| Management Portal | [https://portal.wxcc-anz1.cisco.com/portal](https://portal.wxcc-anz1.cisco.com/portal){:target="_blank"} | cladmin**\<ID\>**@email.carehybrid.com |
| Webex Connect | https://auclpod**\<ID\>**.au.webexconnect.io/ | cladmin**\<ID\>**@email.carehybrid.com |
| Agent Desktop | [https://desktop.wxcc-anz1.cisco.com](https://desktop.wxcc-anz1.cisco.com){:target="_blank"} | clagent**\<ID\>**@email.carehybrid.com |

> **NOTE:**  
> **\<ID\>** – is your unique POD ID listed on the card. \
> The lab POD is the same as the production tenant which is located in the ANZ Datacenter. These labs are for instructional purposes only but the configuration can be reused for the real deployment.
> The telephony service is not activated. This pod is used only for digital channels.

## Before starting the labs

1. Please confirm that you can login to WxCC Admin portal and Agent desktop by using the links above.

2. Use the admin account to access **Control Hub** and **Administration/Management** portal. 

3. To log in to the agent desktop, use either a separate web browser or a new incognito web page. This will prevent any browser caching issues with admin and agent credentials.

    - Navigate to **[https://desktop.wxcc-anz1.cisco.com/](https://desktop.wxcc-anz1.cisco.com/){:target="_blank"}** in a new browser or in incognito mode.

    - Enter the agent’s **email ID** `clagent**\<ID\>**@email.carehybrid.com`.

    - Enter the **Password** for the appropriate Username.

    - In the **_Station Login_** pane, select **"Extension"** and put any number, for instance 1000. 

      > **Note:**  The Webex Calling service is not activated at this tenant we need to set a dummy extension only once during the login.

    - Select the `Team1` and click **_Submit_**. Make sure that you are successfully logged in to the Agent Desktop. Now you can continue with the Next Lab.

      <img align="middle" src="images/Lab1_Login.gif" width="1000" />
      <br/>
      <br/>

4. Please follow the labs in the same order as they are provided.

### **Users**

Users are already configured for you with following user settings in the Webex CC admin portal.

| **User Role** | **User email**                       |
| ------------- | ------------------------------------ | 
| Agent         | clagent**\<ID\>**@email.carehybrid.com   | 
| Supervisor    | clsup**\<ID\>**@email.carehybrid.com     | 

### **User Settings**

| **Entity**          | **Name** |
| ------------------- | -------- |
| Multimedia Profiles | MMP   |
| Site                | Site1  |
| Team1               | Team1 |
| Team2               | Team2 |

## **Lab Support**

1. Proctors are your number 1 contact. If you need assistance just raise your hand.

2. All registered participants are also added to the support room where engineering and Product Management team are added. As an alternative way, you can use that space for any questions related to the digital channels.

### May good fortune smile on you as you begin this new adventure :)
 
<script>
function mainPage() {window.location.href = "https://ciscolivelabs.github.io/wxcclabguides/LTRCCT-2336/Home.html";}
function nextLab() 
 {
 window.location.href = "https://ciscolivelabs.github.io/wxcclabguides/LTRCCT-2336/Lab1_Preconfiguration.html";
 }
</script>

<div id="button-row">
<button onclick="mainPage()" style="
  border-radius: 5px;
  background-color: rgb(116,191,75);
  padding: 10px;">Main Page</button>
<button onclick="nextLab()" style="
  position: absolute;
  right: 200px;
  border-radius: 5px;
  background-color: rgb(116,191,75);
  padding: 10px;">Next Lab</button>

</div>
