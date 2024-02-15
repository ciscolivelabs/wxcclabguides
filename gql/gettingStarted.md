---
Title: "Getting Started"
---
<script>
Function vidPop(id){
video = new CustomEvent("vidPop",{bubbles: true, composed: true, detail: id })
document.body.dispatchEvent(video)
}
</script>


# Introduction
In this group of labs we will be exploring how to use Graph QL to get data from the Webex Contact Center's search API.

## Pre-requisites
- You will need to have an administrator or supervisor account on the tenant from which you will accessing data. (**You cannot use and external or partner account for these labs**)
- You will nee dto know the ORG ID of the tenant from which you will accessing data.
- Make sure tha you watch the introduction video so that you understand how to navigate the tools in the lab.

## Lab Objective
- Get your Bearer token set as a global environment variable in Altair.
- Retrieve introspection information from the Search API
- Execute your first query


### testing section

<button onclick="vidPop('b2cb6220-bebe-4a47-a110-26ca150b2173')">Launch Video</button>
