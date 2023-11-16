---
title: 'Creating a BRE Lookup'
--- 
# Table of Contents

- [Table of Contents](#table-of-contents)
  - [Before You Begin](#before-you-begin)
  - [Fill in the form with the necessary details and click "Update Directions"](#fill-in-the-form-with-the-necessary-details-and-click-update-directions)
  - [Preparing the tenant to use the BRE:](#preparing-the-tenant-to-use-the-bre)
      - [Navigate the Business Rules](#navigate-the-business-rules)
      - [Found rule](#found-rule)
      - [NotFound rule](#notfound-rule)
  - [Adding, updating, and removing data from your BRE table](#adding-updating-and-removing-data-from-your-bre-table)
    - [Logging in](#logging-in)
    - [Adding and updating data](#adding-and-updating-data)
    - [Adding, updating and removing data in bulk](#adding-updating-and-removing-data-in-bulk)
  - [Accessing the BRE data from your flow](#accessing-the-bre-data-from-your-flow)
  - [Parsing BRE data to a variable](#parsing-bre-data-to-a-variable)

---

## Before You Begin
Ask your CSM to create a BRE Table for you

You can access the BRE data here: https://rules.wxcc-us1.cisco.com/datasync

---

## Fill in the form with the necessary details and click "Update Directions" 
<form>
  
  <label for="context">Table Name Created by CSM:</label><br>
  <input type="text" id="context" name="context"><br>
  
  <label for="label">Label Name (keep default unless you have a reason):</label><br>
  <input type="text" id="label" name="label" value="routeInfo"><br>
  
  <label for="key">Key to be used in flows:</label><br>
  <input type="text" id="key" name="key"><br>
<br>

  <button onclick="update()">Update Directions</button>
</form>

---

## Preparing the tenant to use the BRE:

 ⚠️ **Important note:** All BRE are settings, rules, attributes, and labels are case sensitive!

#### Navigate the Business Rules 
> In the BRE
>
>
>> Click Attributes in the top ribbon 
>>
>> Click Add  
>> 
>>> Name: context (case sensitive) 
>>>
>>> Data Type: Text
>>>
>>> Click Save
>>
>> Click Labels in the top ribbon
>>
>>> Click Add 
>>>
>>> Name: <w class="label_out">routeInfo</w> (case sensitive)
>>>
>>> Click Save
>>
>> Click Context in the top ribbon
>>
>>> Click Add Context 
>>>
>>> Name: <w class = "context_out">Table/Context that your CSM created for you</w> (case sensitive) 
>>> 
>>> Attribute: context 
>>>
>>> Click Save
>>
>> Click on the line of the Context you just created (<w class = "context_out"></w>)
>>
>>
>> Add the rules listed below


#### Found rule

> Click on Add Rule (Editor)
> 
> Name: <w class="context_out"></w>Found
> 
> Active: True
> 
> Label: <w class = "label_out">routeInfo</w>
>
> Priority: 100
>
> Copy the rule into the editor:
>
>> <textarea id="foundruleDisplay" style="width: 1100px; height: 100px;" readonly>when
>>    c: Contact()
>>    eval(c.getGlobalValuesManager().getAsString( c.getTenantId(), c.getAttribute("context") + "." + c.getAttribute("ani")) != null)
>> then
>>    c.putAttribute("routeInfo", c.getGlobalValuesManager().getAsString(c.getTenantId(), c.getAttribute("context") + "." + c.getAttribute("ani")));
>> end </textarea><br>


<ww id="foundRule" style="display: none" >when<br>
    c: Contact()<br>
    eval(c.getGlobalValuesManager().getAsString( c.getTenantId(), c.getAttribute("context") + "." + c.getAttribute("<w class = "key_out">ani</w>")) != null)<br>
then<br>
    c.putAttribute("<w class = "label_out">routeInfo</w>", c.getGlobalValuesManager().getAsString(c.getTenantId(), c.getAttribute("context") + "." + c.getAttribute("<w class = "key_out">ani</w>")));<br>
end<br> </ww>

#### NotFound rule

> Click on Add Rule (Editor)
> 
> Name: <w class="context_out"></w>Notfound
> 
> Active: True
> 
> Label: <w class = "label_out">routeInfo</w>
>
> Priority: 99
>
> Copy the rule into the editor:
>
>
>> <textarea id="notfoundruleDisplay" style="width: 1100px; height: 100px;" readonly>when
>>    c: Contact()
>>    eval(c.getGlobalValuesManager().getAsString( c.getTenantId(), c.getAttribute("context") + "." + c.getAttribute("ani")) == null)
>> then
>>   c.putAttribute("routeInfo", "NotFound");
>> end </textarea><br>

<ww id="notfoundRule" style="display: none" >
when<br>
    c: Contact()<br>
    eval(c.getGlobalValuesManager().getAsString( c.getTenantId(), c.getAttribute("context") + "." + c.getAttribute("<w class = "key_out">ani</w>")) == null)<br>
 then<br>
   c.putAttribute("<w class = "label_out">routeInfo</w>", "NotFound");<br>
 end<br>
</ww>

## Adding, updating, and removing data from your BRE table
### Logging in
> Navigate to [https://rules.wxcc-us1.cisco.com/datasync/login](https://rules.wxcc-us1.cisco.com/datasync/login){:target="_blank"}
>
> <details> <summary>Click datasync link</summary>
> <img style="position: relative" src="images/BRE_Login.jpg"/>
>
> </details>
>
>
>> Login using your tenant admin credentials if prompted
>
> <details> <summary>Select Site A</summary>
> <img style="position: relative" src="images/BRE_Site.jpg"/>
>
> </details>
>
> ---

### Adding and updating data
>
> <details> <summary>Click Add BRE Data</summary>
> <img style="position: relative" src="images/BRE_AddData.jpg"/>
>
> </details>
>
> Select your tenant name from the Tenant Name drop down
>
> Select the table name you want to add/update data to in the BRE Lookup Type drop down
>
> Add the value you will be looking up in the Key field
>
> Add the value you want to be returned in the Value field
>
> Clicking Add Data will let you add additional rows
>
> Clicking the Remove button will remove teh row from your Add/Update
>
> Click Submit to save the updates
>
> ---


### Adding, updating and removing data in bulk
>
> <details> <summary>Click Upload BRE CSV data</summary>
> <img style="position: relative" src="images/BRE_AddDataBulk.jpg"/>
>
> </details>
>
>
> Create a CSV file with 3 columns
>
> > ⚠️ CSV must have headers in the file or the first row will be skipped 
> >
> > Key: the value you will be looking up
> >
> > Value: the value you want to be returned
> >
> > Action: the action you want taken on the key (ADD, UPDATE, DELETE)
>
>
> Select your tenant name from the Tenant Name drop down
>
> Select the table name you want to add/update data to in the BRE Lookup Type drop down
>
> ---




## Accessing the BRE data from your flow
> <div style="width: 465px; height: 357px;position:relative">
> <img style="position: relative; width: 465px; height: 357px;" src="images/BRE_Params.jpg"/>
> <w style="position: absolute; top: 27%; left:53%; color: rgb(0,0,0);" class = "context_out">table</w>
> <w style="position: absolute; top: 41%; left: 8%; color: rgb(0,0,0)" class = "key_out">ani</w>
> <w style="position: absolute; top: 41%; left: 53%; color: rgb(0,0,0)">your lookup value</w>
> </div>

---


## Parsing BRE data to a variable
> <img style="position: relative" src="images/BRE_Parse.jpg"/>
<w style="position: relative; top: -80px; left:55px; color: rgb(0,0,0)">$.</w>
<w style="position: relative; top: -80px; left:52px; color: rgb(0,0,0)" class = label_out>routeInfo</w>

---

<script>
    function update(){them = Array.from(document.querySelectorAll("input")).reduce((acc, input) => ({...acc, [input.id + "_out"] : input.value}),{});
	Object.entries(them).forEach((entry) => {
    Array.from(document.getElementsByClassName(entry[0])).forEach((element,index) => 
    {
      console.log(document.getElementsByClassName(entry[0])[index].innerHTML); 
      document.getElementsByClassName(entry[0])[index].innerHTML = entry[1];
    })});
  document.getElementById("foundruleDisplay").value = document.getElementById("foundRule").innerText;
  document.getElementById("notfoundruleDisplay").value = document.getElementById("notfoundRule").innerText;
  event.preventDefault()}
</script> 