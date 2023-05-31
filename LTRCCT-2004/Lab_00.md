---
title: "Setup"
---

<form id="labInfo">
<label for="labID">Lab POD</label><br>
<input type="text" id="pod" name="POD"> <br>
<button onclick="update()">Update</button>
</form>

<script>
async function update(){
    response = await fetch(`https://63f62bf859c944921f6e89de.mockapi.io/ivrpod?pod=CL23IVRpod${document.forms.labInfo[0].value}`,
    {
    method: 'GET',
    redirect: 'follow'
})
response = await response.json()
await localStorage.setItem("EPDN",await response[0].EPDN)
await localStorage.setItem("admin",await response[0].admin)
await localStorage.setItem("agent1",await response[0].agent1)
await localStorage.setItem("agent2",await response[0].agent2)
await localStorage.setItem("admin_ext",await response[0].admin_ext)
await localStorage.setItem("agent1_ext",await response[0].agent1_ext)
await localStorage.setItem("agent2_ext",await response[0].agent2_ext)
await localStorage.setItem("PW",await response[0].PW)
await localStorage.setItem("Agent1_phone",await response[0].Agent1_phone)
await localStorage.setItem("TicketID",await response[0].TicketID)
}
</script>

<w ></w><br>
<w></w>