# Cheat Sheet

## Contact Center Navigation

> Navigate to Entry Points
>
> Map an Entry Point
>
> Navigate to Queues
>
> Navigate to Teams
>
> Navigate to Skills
>
> Navigate to Skills Profiles
>
> Navigate to Flow Builder

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
> \{\{now()\|epoch\}\}
