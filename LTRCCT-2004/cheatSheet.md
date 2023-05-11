---
title: 'Cheat Sheet'
---

## Contact Center Navigation

> <details> <summary>Navigate to Entry Points </summary>
> 
> <img src="images/openEP.gif"/> 
> 
> </details>
>
> <details> <summary>Map an Entry Point</summary>
>
> <img src="images/openEPmap.gif"/>
>
> </details>
>
> <details> <summary>Navigate to Queues</summary>
>
> <img src="images/openQueue.gif"/>
>
> </details>
>
> <details> <summary>Navigate to Teams</summary>
>
> <img src="images/openEP.gifx"/>
>
> </details>
>
> <details> <summary>Navigate to Skills</summary>
>
> <img src="images/openEP.gifx"/>
>
> </details>
>
> <details> <summary>Navigate to Skills Profiles</summary>
>
> <img src="images/openEP.gifx"/>
>
> </details>
>
> <details> <summary>Navigate to Flow Builder</summary>
>
> <img src="images/rsToFlow.gif"/>
>
> </details>

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
