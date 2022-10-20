---
title: 'Lab 4: Agent Productivity'
---

# Table of Contents
- [Table of Contents](#table-of-contents)
- [Introduction](#introduction)
    - [Lab Objective](#lab-objective)
    - [Pre-requisite](#pre-requisite)
- [Lab Section](#lab-section)
  - [Step 1. Create Inbound Webhook](#step-1-create-inbound-webhook)
  - [Step 2. Create an Event](#step-2-create-an-event)
  - [Step 3. Create Webex room](#step-3-create-webex-room)
  - [Step 4. Fetch Webex access token and RoomId](#step-4-fetch-webex-access-token-and-roomid)
  - [Step 5. OTP Flow configuration](#step-5-otp-flow-configuration)
  - [Step 6. Agent desktop layout update](#step-6-agent-desktop-layout-update)
  - [Step 7. OTP scenario verification](#step-7-otp-scenario-verification)
  - [Back to top](#back-to-top)
    - [Congratulations, you have completed this section!](#congratulations-you-have-completed-this-section)

# Introduction 
### Lab Objective

In this Lab, we will go through the tasks that are required to configure a basic OTP (One Time Passcode) verification scenario in Webex Connect. The OTP generated will be sent to customer's email and also to agents Webex teams, that is accessible in the agent desktop. 

### Pre-requisite

1. You recived an admin credentials to configure in Managment Portal and Webex Connect.
2. You have successfully completed the previous Lab **Preconfiguration**

# Lab Section
## Step 1. Create Inbound Webhook

- Login to your respective Webex Connect UI using the provided URL https://auclpod**X**.au.webexconnect.io (where **X** is your POD number).

- Navigate to Assets > Integrations > Add Integration

<img align="middle" src="images/AU_Lab4_1.png" width="1000" />
<br/>
<br/>

- Click on Add Integration and select Inbound Webhook 

<img align="middle" src="images/AU_Lab4_2.png" width="1000" />
<br/>
<br/>

- Input a desired name in the **Webhook Name** field. Copy the **Webhook URL** for later use. Click **Save**

<img align="middle" src="images/AU_Lab4_3.png" width="1000" />
<br/>
<br/>

## Step 2. Create an Event

- Login to your Webex contact centre portal with your administrator credentials: **[https://portal.wxcc-anz1.cisco.com/portal](https://portal.wxcc-anz1.cisco.com/portal){:target="_blank"}** and navigate to **New Digital Channels**

<img align="middle" src="images/AU_Lab4_4.png" width="1000" />
<br/>
<br/>

- Navigate to Groups > Click 'Default'

<img align="middle" src="images/AU_Lab4_5.png" width="1000" />
<br/>
<br/>

- Click 'Default' Team

<img align="middle" src="images/AU_Lab4_6.png" width="1000" />
<br/>
<br/>

- Navigate to 'Events and Rules' and click 'Add New Event'

<img align="middle" src="images/AU_Lab4_7.png" width="1000" />
<br/>
<br/>

- Input a desired name in the **Name** field 

- Select the **Method** as **POST**

- Input the webhook URL (copied in Step-1) in the **URL** field

- Select the **Expected Response format** as **JSON**

<img align="middle" src="images/Lab8_8.png" width="1000" />
<br/>
<br/>

- Select the **Payload** as **Key Value Pair** and Click on **Add Param**

<img align="middle" src="images/AU_Lab4_9.png" width="1000" />
<br/>
<br/>

- In the **Edit Parameter**: 
  
  -- Type Parameter name - **registeredmobile** (All in small letters)

  -- Select **Request Body** in Pass Through

  -- Select **custom param** in the Value field

  -- select radio button **Allow Agent to enter value manually**

  -- Click on **Update**

<img align="middle" src="images/AU_Lab4_10.png" width="1000" />
<br/>
<br/>


- Click **Save**

<img align="middle" src="images/AU_Lab4_11.png" width="1000" />
<br/>
<br/>


## Step 3. Create Webex room 

- Go to https://web.webex.com/sign-in and login with the administrator credential of your lab pod. 

<img align="middle" src="images/Lab8_10.png" width="1000" />
<br/>
<br/>

<img align="middle" src="images/Lab8_11.png" width="1000" />
<br/>
<br/>

- Click **Create a Space** option

<img align="middle" src="images/Lab8_12.png" width="1000" />
<br/>
<br/>

- Enter a desired **name** for the room, search  for **Agent** and add the Agent user to this room. Click **Create**

<img align="middle" src="images/AU_Lab4_12.png" width="1000" />
<br/>
<br/>

- Verify that the room is created and the agent is part of the newly created room. 

<img align="middle" src="images/AU_Lab4_13.png" width="1000" />
<br/>
<br/>

## Step 4. Fetch Webex access token and RoomId

- Go to https://developer.webex.com/ and login with the administrator credential of your lab pod. 

<img align="middle" src="images/Lab8_15.png" width="1000" />
<br/>
<br/>

- Click **Documentation** . Navigate to Messaging > Reference > Rooms > Select **List Rooms** and copy the access token under **Authorization**

- Click **Run**

<img align="middle" src="images/Lab8_16.png" width="1000" />
<br/>
<br/>

- In the response window, identify the room created in the previous step and copy the value of **id** of that room in a notepad. (This is for later use).

<img align="middle" src="images/Lab8_17.png" width="1000" />  
<br/>
<br/>

## Step 5. OTP Flow configuration 

- Login to your respective Webex Connect UI using the provided URL https://auclpod**X**.au.webexconnect.io/ (where **X** is your POD number).

- Click on **Services** and select the **My First Service**.

- In the service click on **FLOWS** -> **CREATE FLOW** 

- Enter the **FLOW NAME** as **Inbound Webhook Flow**, select the **TYPE** as **Work Flow** and under **METHOD** select **New flow**. Click **Create**

<img align="middle" src="images/AU_Lab4_14.png" width="1000" />
<br/>
<br/>

- Select the trigger event of this flow as **Webhook**

<img align="middle" src="images/AU_Lab4_15.png" width="1000" />
<br/>
<br/>

- In configure webhook window, select the **Webhook Name** as the one created in Step-1

- Input the sample input data as,

`
  {
     "registeredmobile":"042XXXXXXXX"
  }
`

- Click **Parse** and Click **Save**

<img align="middle" src="images/AU_Lab4_16.png" width="1000" />
<br/>
<br/>

- Navigate to settings on the top right corner of the flow builder UI > Custom Variables. 

- Create a new variable and provide a default value. 

- Enter the **Variable Name** as 'getOTP' and the **Default Value** as '123456'. Click **Save**

<img align="middle" src="images/Lab8_22.png" width="1000" />
<br/>
<br/>

- Add **Generate OTP** to the flow builder UI. Connect the trigger event success outcome to the **Generate OTP** node. Double click the node. 

<img align="middle" src="images/Lab8_21.gif" width="1000" />
<br/>
<br/>

- Select **OTP Format** as 'Numeric' and **OTP Validity** as '30' 

<img align="middle" src="images/AU_Lab4_18.png" width="1000" />
<br/>
<br/>

- Select the **getOTP** variable in the **Transaction Reeference** section and click **Save** 

<img align="middle" src="images/Lab8_24.gif" width="1000" />
<br/>
<br/>

- Add **SMS** node to the flow builder UI and connect the success outcome of **Generate OTP** to the **SMS** node. Double click the node. 

<img align="middle" src="images/AU_Lab4_19.gif" width="1000" />
<br/>
<br/>

- Select the **Destination** as the registeredmonile output variable of the trigger (Start) node. Select **CONNECT** in the Form Number. 

<img align="middle" src="images/Au_Lab4_19.png" width="1000" />
<br/>
<br/>

Enter the desired **Message** in the **Message** field and include the **$(n3.generateOTP.OTP)** variable as shown in the image below. 

<img align="middle" src="images/Au_Lab4_20.png" width="1000" />
<br/>
<br/>

- Add **HTTP Request** node to the flow builder UI and connect the success outcome of **Email** to the **HTTP Request** node. Double click the node. 

<img align="middle" src="images/Lab8_28.gif" width="1000" />
<br/>
<br/>

- Configure the node with the below details, 

**Method**: POST 
**Endpoint URL**: https://webexapis.com/v1/messages

**Header**: 
Authorization: Bearer <Access_Token_Copied_In_Step_4>
Content-Type: application/json

**Body**: 

{

"roomId": "<room_ID_captured_In_Step_4>",

"text": "OTP to verify is (n3.generateOTP.OTP)" 

}

<img align="middle" src="images/AU_Lab4_21.png" width="1000" />
<br/>
<br/>

- Configure the success path of the **HTTP Request** node by click and drag of the green dot in the node. 

<img align="middle" src="images/Lab8_30.gif" width="1000" />
<br/>
<br/>

- Configure the error path of all 3 nodes - **Generate OTP** , **SMS** and **HTTP Request** by click and drag out of the red and orange dots in the nodes. 

<img align="middle" src="images/Lab8_31.gif" width="1000" />
<br/>
<br/>

- Click **Make Live** option on the top right of the flow builder UI, and click **Make Live**


## Step 6. Agent desktop layout update 

- Login to Webex contact centre administration portal **[https://portal.wxcc-us1.cisco.com/portal](https://portal.wxcc-us1.cisco.com/portal){:target="_blank"}** and navigate to Desktop Layout section. Click **Edit**

<img align="middle" src="images/AU_Lab4_22.png" width="1000" /> 
<br/>
<br/>

- Download the desktop layout and open in a text editor. 

<img align="middle" src="images/AU_Lab4_23.png" width="1000" /> 
<br/>
<br/>

- Set the value of "webexConfigured" parameter to "true" and save the file. 

<img align="middle" src="images/AU_Lab4_24.png" width="1000" /> 
<br/>
<br/>
  
- **Upload** this updated file in Webex contact centre administration portal and click **Save**

<img align="middle" src="images/AU_Lab4_25.png" width="1000" />
<br/>
<br/>

- Login to agent dekstop and verify that the the **Webex** option is visible and the OTP verification room is seen. (If already logged in to agent desktop, please logout and login again)

<img align="middle" src="images/AU_Lab4_26.png" width="1000" />
<br/>
<br/>

## Step 7. OTP scenario verification

- Initiate an WebChat contact and accept the Chat. (Refer Lab2 - Step 7 to initiate Chat)

<img align="middle" src="images/AU_Lab4_27.png" width="1000" />
<br/>
<br/>

- Choose the **Trigger Workflow** option, select **OTP Verification** and click **Next**

<img align="middle" src="images/AU_Lab4_28.png" width="1000" />
<br/>
<br/>

- Type mobile number in e164 format and click **Trigger**

<img align="middle" src="images/AU_Lab4_29.png" width="1000" />
<br/>
<br/>


- A confirmation that the workflow has been triggered will be displayed. Also, OTP will be send on the customer's mobile number that agent entered and the same OTP will be sent to agent through the Webex app integrated to agent desktop. 

<img align="middle" src="images/AU_Lab4_30.png" width="1000" />
<br/>
<br/>

- Customer OTP 

<img align="middle" src="images/AU_Lab4_32.png" width="1000" />
<br/>
<br/>

- Agent OTP 

<img align="middle" src="images/AU_Lab4_31.png" width="1000" />
<br/>
<br/>

- On the Webchat, customer replies with the OTP received.

<img align="middle" src="images/AU_Lab4_34.png" width="1000" />
<br/>
<br/>

- Agent can now verify the OTP. 

<img align="middle" src="images/AU_Lab4_35.png" width="1000" />
<br/>
<br/>

[Back to top](#table-of-contents)
---

### Congratulations, you have completed this section! 

<script>
function mainPage() {window.location.href = "https://ciscolivelabs.github.io/wxcclabguides/LTRCCT-2336/Home.html";}
function nextLab() 
 {
 window.location.href = "https://ciscolivelabs.github.io/wxcclabguides/LTRCCT-2336/Lab5_Troubleshooting.html";;
 }
</script>

<div id="button-row">
<button onclick="mainPage()" style="
  border-radius: 5px;
  background-color: rgb(116,191,75);
  padding: 10px;">Home Page</button>
<button onclick="nextLab()" style="
  position: absolute;
  right: 200px;
  border-radius: 5px;
  background-color: rgb(116,191,75);
  padding: 10px;">Go to the Next Lab</button>

</div>
