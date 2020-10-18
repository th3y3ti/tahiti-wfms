## Playbooks Repo
This directory is for storing Threat Hunting playbooks. Threat Hunting playbooks are basically the recipes for conducting Threat Hunts.

### Instructions for creating a new playbook

Open a new `create playbook` issue and then create a new branch.  
In the new branch, copy the playbook template below, make a new playbook, paste the template into the new playbook and fill in the information.

**Note:** UUID's can be generated here (https://www.uuidgenerator.net/version4).

```
---
uuid: 00000000-0000-0000-0000-000000000000
created by: name
created date: xx/xx/20xx
last ran: xx/xx/20xx
classification: kill chain phase
status: initial
priority: 1-5
---

## Hypothesis
Initial or refined hypothesis.

## Trigger
What triggered the creation of this abstract?

## Reference
Reference to the trigger.

## Priority Explanation
Priority of this playbook.

## MITRE Reference(s)
Reference (links) to attack techniques from MITRE ATT&CK.
- https://attack.mitre.org/techniques/Txxxx/

## Possible Actors
Any actors that use these techniques?

## Actor Campaign
Is there an active campaign in which these techniques are used?

## Actor Capability with Explanation
High, Medium, Low

## Estimated Resources
Rough estimation of the time and resources required (to execute this hunt)
```
