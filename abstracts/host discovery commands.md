---
uuid: 65104859-6d74-42a9-8bed-94912dcd8ed5
created by: th3y3ti
created date: 04/01/2020
last ran: N/A
classification: exploitation
status: initial
priority: 2
---

## Hypothesis
Adversaries are gaining knowledge about the environment by running "host discovery commands" on the host.

## Trigger
- Situational Awareness

## Reference
No Trigger. This hunt is based on one documented in MITRE's Cyber Analytic Repository (CAR)
- https://car.mitre.org/analytics/CAR-2016-03-001/

## Priority Explanation
This abstract produces a lot of noise but the technique is very common.

## MITRE Reference(s)
- https://attack.mitre.org/techniques/T1087/
- https://attack.mitre.org/techniques/T1069/
- https://attack.mitre.org/techniques/T1016/
- https://attack.mitre.org/techniques/T1082/
- https://attack.mitre.org/techniques/T1033/
- https://attack.mitre.org/techniques/T1057/
- https://attack.mitre.org/techniques/T1007/

## Possible Actors
Discovery using host discovery commands is fairly common amongst several actors.

## Actor Campaign
Discovery using host discovery commands is fairly common amongst several actors.

## Actor Capability with Explanation
Medium 
- Running these commands would require first gaining access to a host. Afterword, these commands are trivial to run and require only user level permissions.

## Estimated Resources
Host commands are used regularly but system admins and even standard users. This hunt should be time restricted to 2 days or else it could take a very long time.
