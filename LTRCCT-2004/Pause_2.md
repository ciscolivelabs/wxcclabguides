---
title:"Hang out here!"
---

<img src="images/pause_1.jpg">

<script>
function mainPage() {window.location.href = "Lab_3";}
function nextLab() 
 {
 window.location.href = "Lab_4";
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