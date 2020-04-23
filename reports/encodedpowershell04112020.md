---
Abstract UUID: 0f82814f-0815-4089-9507-9b66440b9aa1
Date: 04/11/2020
Incidents: 0
Countermeasures: 0
Recommendations: 0
---

# What did you hunt for?
- For this hunt, I focused on windows workstations only using the sysmon data in splunk
- I searched from the last 30 days of data 
- To reduce the noise, I first isolated powershell to only commands that were not ran interactively. e.g. parent process not explorer.exe
- I then looked for powershell commands that had -enc or -encodedcommand flags

# What did you find?
- I was unable to find any evidence of malicious encoded powershell

# What did you learn?
- I found an interesting article on hunting for powershell abuse and an interesting analytic in MITRE's cyber analytic repository (CAR)
- https://www.peerlyst.com/posts/hunting-for-powershell-abuses-part-1-ali-ahangari-1
- https://car.mitre.org/analytics/CAR-2014-04-003/

# What did you create or improve?
- I saved my queries in Splunk as `encoded powershell hunt`
