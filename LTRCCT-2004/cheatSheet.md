---
title: 'Cheat Sheet'
---

## Contact Center Navigation

> <summary> Navigate to Entry Points </summary>
> 
> <img src="images/openEP.gif"/> 
>
> Map an Entry Point
>
> <img src="images/openEPmap.gif"/>
>
> Navigate to Queues
>
> <img src="images/openQueue.gif"/>
>
> Navigate to Teams
>
> <img src="images/openEP.gifx"/>
>
> Navigate to Skills
>
> <img src="images/openEP.gifx"/>
>
> Navigate to Skills Profiles
>
> <img src="images/openEP.gifx"/>
>
> Navigate to Flow Builder
>
> <img src="images/rsToFlow.gif"/>

## Pebble
> Official pebble template documentation [https://pebbletemplates.io/](https://pebbletemplates.io/){:target="_blank"}

#### Retrieve the last 10 digits of an ANI 
> \{\{NewPhoneContact.ANI \| slice (NewPhoneContact.ANI.length -10,NewPhoneContact.ANI.length)\}\}

#### Retrieve the last 10 digits of an DNIS
> \{\{NewPhoneContact.DNIS \| slice (NewPhoneContact.DNIS.length -10,NewPhoneContact.DNIS.length)\}\}




### Time

#### Time Now
> \{\{now()\}\}

#### Time Now as Epoch
> \{\{now() \| epoch\}\}
