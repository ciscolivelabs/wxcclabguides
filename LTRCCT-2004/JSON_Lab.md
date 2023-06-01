---
title: 'JSON Lab'
session: LTRCCT-2004
speaker: Kevin Simpson
---

# Lab Section

### Navigate to [JSON Path Finder](https://jsonpathfinder.com/){:target="_blank"}
   
### Exercise 1

1. Copy this text into the left pane of the JSON PathFinder
     >  <textarea cols="50" disabled style= "background-color: #ffffff">{"name":"John", "age":30, "car":null} </textarea>
2. Click Beautify
3. Click age
   > What is the JSON path for age? 
   >
4. Delete the contents of the left pane and copy this text into the left pane of the JSON PathFinder
   >
   >   <textarea cols="50" disabled style= "background-color: #ffffff">{"name":"John","age":30,"cars":["Ford","BMW","Fiat"]}</textarea>
5. Click Beautify
   > Click on cars and observe that there is an array.
   >
   > What is the JSON path for BMW?

### Exercise 2

1. Delete the contents of the left pane and copy this text into the left pane of the JSON PathFinder
   >  <textarea cols="70" rows = "8" disabled style= "background-color: #ffffff">{"name":"John Smith","sku":"20223","price":23.95,"shipTo":{"name":"Jane Smith","address":"123 Maple Street","city":"Pretendville","state":"NY","zip":"12345"},"billTo":{"name":"John Smith","address":"123 Maple Street","city":"Pretendville","state":"NY","zip":"12345"}}</textarea>
   >

2. Click Beautify
   > Note that shipTo and BillTo have additional JSON objects in them.
   >
   > What is the JSON path for the ship to state?
   >
3. Delete the contents of the left pane and copy this text into the left pane of the JSON PathFinder
   > <textarea cols="70" rows = "10" disabled style= "background-color: #ffffff">[{"name":"John Smith","sku":"20223","price":23.95,"shipTo":{"name":"Jane Smith","address":"123 Maple Street","city":"Pretendville","state":"NY","zip":"12345"},"billTo":{"name":"John Smith","address":"123 Maple Street","city":"Pretendville","state":"NY","zip":"12345"}},{"name":"Alice Brown","sku":"54321","price":199.95,"shipTo":\{"name":"Bob Brown","address":"456 Oak Lane","city":"Pretendville","state":"HI","zip":"98999"},"billTo":{"name":"Alice Brown","address":"456 Oak Lane","city":"Pretendville","state":"HI","zip":"98999"}}]</textarea>
   >

4. Click Beautify
   > Note that we now have an array of objects (0 and 1)
   >
   > What is the JSON path for Alice Brown's ship to state?

### Exercise 3

1. Delete the contents of the left pane and copy the raw text from [this flow](flows/CL_1_salesService_lang.json){:target="_blank"} into the left pane of the JSON PathFinder
2. Click Beautify
   > How many variables are there in this flow?
   >
   > What is the name and default value of variable 4?
    
    ---





















<script>
function mainPage() {window.location.href = "Lab_4";}
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