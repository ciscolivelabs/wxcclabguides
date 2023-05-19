---
title: 'Creating a BRE Lookup'
--- 
# Table of Contents

- [Table of Contents](#table-of-contents)
  - [Before You Begin](#before-you-begin)
  - [Fill in the form with the necessary details and click "Update Directions"](#fill-in-the-form-with-the-necessary-details-and-click-update-directions)
  - [Preparing the tenant to use the BRE:](#preparing-the-tenant-to-use-the-bre)
    - [In the Attributes section:](#in-the-attributes-section)
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

> Click BRE 
Click Attributes and add a new attribute called context (case sensitive) and type text
>
> Click Labels and add <w class="label_out">routeInfo</w> (case sensitive)
>
> Click Context and Add Context with the name of the <w class = "context_out">table/Context that your CSM created for you</w> (case sensitive) then select <w class = "context_out">context</w> under Attribute

### In the Attributes section:

#### Found rule

> Click on Add Rule (Editor)
> 
> Name your rule <w class="context_out">something ending in </w>Found
> 
> Click to make the rule active
> 
> Select the label <w class = "label_out">routeInfo</w> from the drop down 
>
> Set the priority to 100
>
> Copy the rule into the editor



>> <ww id="foundRule">when<br>
    c: Contact()<br>
    eval(c.getGlobalValuesManager().getAsString( c.getTenantId(), c.getAttribute(<q>context</q>) + <q>.</q> + c.getAttribute(<q><w class = "key_out">ani</w></q>)) != null)<br>
 then<br>
    c.putAttribute(<q><w class = "label_out">routeInfo</w></q>, c.getGlobalValuesManager().getAsString(c.getTenantId(), c.getAttribute(<q>context</q>) + <q>.</q> + c.getAttribute(<q><w class = "key_out">ani</w></q>)));<br>
 end<br> </ww>
#### NotFound rule

> Click on Add Rule (Editor)
> 
> Name your rule <w class="context_out">something ending in </w>Notfound
> 
> Click to make the rule active
> 
> Select the label <w class = "label_out">routeInfo</w> from the drop down 
>
> Set the priority to 99
>
> Copy the rule into the editor




>> when<br>
    c: Contact()<br>
    eval(c.getGlobalValuesManager().getAsString( c.getTenantId(), c.getAttribute(<q>context</q>) + <q>.</q> + c.getAttribute(<q><w class = "key_out">ani</w></q>)) == null)<br>
 then<br>
   c.putAttribute(<q><w class = "label_out">routeInfo</w></q>, <q>NotFound</q>);<br>
 end<br>


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
> Select your tenant name from the TenatName drop down
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
> Select your tenant name from the TenatName drop down
>
> Select the table name you want to add/update data to in the BRE Lookup Type drop down
>
> ---




## Accessing the BRE data from your flow
> <img style="position: relative" src="images/BRE_Params.jpg"/>
<w style="position: relative; top: -275px; left: 255px; color: rgb(0,0,0)" class = "context_out">table</w>
<w style="position: relative; top: -225px; left: 15px; color: rgb(0,0,0) " class = "key_out">ani</w>
<w style="position: relative; top: -225px; left: 200px; color: rgb(0,0,0)">value</w>

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
    })})

  event.preventDefault()}
</script> 