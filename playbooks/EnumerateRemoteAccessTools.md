---
title: Enumerate Remote Access Tools
uuid: d81c6bb6-67a4-11ea-bc55-0242ac130003
short_description: >
  This playbook is intended to help identify remote access tools that are used within the client environment.
long_description: >
  **Objective**
  
  
  Even sophisticated adversaries may use commercial and/or open source remote access tools instead of
  using bespoke malware to support their operations. In order to identify the malicious use of remote
  access tools, we could start by enumerating where these tools are present in the client environment.
  Any use of remote access tools that are not approved in corporate policy should receive further scrutiny.
  
  
  **Background**
  
  
  Adversaries leverage commercial and/or open source remote access tools in victim environments for
  the same reason as IT administrators:
  
  
  * Remote access tools such as `TeamViewer`, `VNCViewer`, and `AmmyyAdmin` may offer a fully
  interactive desktop experience, including clipboard and audio support, for IT administrators
  providing technical support or remote administration. It is common to find the legitimate use
  of these applications in most client environments.
  
  * Due to their legitimate commercial use, remote access tools may contain valid cryptographic
  signatures and/or are explicitly whitelisted by application control and anti-virus vendors.

  *   Some of organizations, however, rely on remote access tools for unauthorized (but well-intentioned)
  "Shadow IT" purposes - meaning it is also common to find a variety of different remote access
  tools within a given environment.
  
  * Many of these remote access tools broker their connections between the system and the remote
  user through externally-accessible cloud services, which has the effect of bypassing network
  segmentation and other impediments.
  
  * Remote access tools often require their own application-specific credentials instead of
  integrating with Active Directory or LDAP. This usually means that corporate password policies
  (such as complexity, re-use, and reset frequency) are not enforced for these tools. During remediation,
  credentials for remote access tools are often overlooked and provide easy means of redundant access
  to the victim environment.
  
  * Lastly, these applications usually have minimal or no logging. Few organizations remember to
  forward and retain logs from third-party remote access tools. This is particularly convenient
  for exfiltrating data.
attack_techniques:
- T1219 - Remote Access Tools
data_sources:
- process monitoring
- registry monitoring
- file collection
- dns logs
platforms:
- windows
tags: []
findings:
- Did you find any remote access tools that were not approved for use by corporate policy?
- If unapproved remote access tools were found, can the use of these tools be attributed to Shadow IT?   
- Did you find any hosts with artifacts from multiple remote access tools?
- Did you find any remote access tools masquerading as other files?
- Did you find any evidence of remote access tools running in the context of service or other privileged accounts?
- Did you find any evidence of explicit credentials passed on the commandline for a remote access tool?
- If so, what kind of systems were these remote access tools found on? Do any of these systems hold special importance for the client or their infrastructure (ie, domain controllers)?
---

# Enumerate Remote Access Tools

## Objective

Even sophisticated adversaries may use commercial and/or open source remote access tools instead of using bespoke malware to support their operations. In order to identify the malicious use of remote access tools, we could start by enumerating where these tools are present in the client environment. Any use of remote access tools that are not approved in corporate policy should receive further scrutiny.

## Background

Adversaries leverage commercial and/or open source remote access tools in victim environments for the same reason as IT administrators:

*   Remote access tools such as `` TeamViewer ``, `` VNCViewer ``, and `` AmmyyAdmin `` may offer a fully interactive desktop experience, including clipboard and audio support, for IT administrators providing technical support or remote administration. It is common to find the legitimate use of these applications in most client environments.
*   Due to their legitimate commercial use, remote access tools may contain valid cryptographic signatures and/or are explicitly whitelisted by application control and anti-virus vendors.
*   Some of organizations, however, rely on remote access tools for unauthorized (but well-intentioned) "Shadow IT" purposes - meaning it is also common to find a variety of different remote access tools within a given environment.
*   Many of these remote access tools broker their connections between the system and the remote user through externally-accessible cloud services, which has the effect of bypassing network segmentation and other impediments.
*   Remote access tools often require their own application-specific credentials instead of integrating with Active Directory or LDAP. This usually means that corporate password policies (such as complexity, re-use, and reset frequency) are not enforced for these tools. During remediation, credentials for remote access tools are often overlooked and provide easy means of redundant access to the victim environment.
*   Lastly, these applications usually have minimal or no logging. Few organizations remember to forward and retain logs from third-party remote access tools. This is particularly convenient for exfiltrating data.


## Data Collection

### Preparation

Before proceeding with the following analysis tasks, reach out to the customer and ask which remote access tools, if any, are approved for use in their environment.

```python tags=["remove_cell"]
%load automate.py
```

```python
%%jinja --markdown
{% if domain_ids %}
### Scope
This playbook was executed for the following domains:
  {% for domain_id in domain_ids -%}
    * {{ domain_id }}
  {% endfor %}
{% endif %}
```

```python
%%jinja --markdown
### Query Pack Results Summary
{% if playbook.query_packs %}
The {{ playbook.title }} playbook has {{ playbook.query_packs | length }} associated query packs.

* Results: {{ query_packs_with_results.query_pack.unique() | length }} / {{ playbook.query_packs | length }}

{{ query_pack_results_summary.to_markdown() }}

The following query packs had results. Please review in the Red Cloak portal
and add relevant files to an investigation.

**Reminder:** don't forget to set your impersonation in the portal!

{% for query_pack, results in query_packs_with_results.groupby('query_pack') %}
### {{ query_pack }}

|Doc Type|Results|Query|
|--------|-------|:----|
{% for query in results.to_dict(orient='records') -%}
|{{ query['doc_type'] }}|{{ query['num_total'] }}|[{{ query['query'] }}]({{ convert_to_new_portal_url(query['url']) }})|
{% endfor %}
{% endfor %}
{% endif %}
```

### Step 1 - Identify Use of Remote Access Tools through Process Execution Auditing

Search through process execution data for `` image_path `` or `` commandline `` fields with known remote access tool filenames:

Document any the filenames, hostnames, and user accounts

### Step 2 - Identify Use of Remote Access Tools through Persistence Mechanisms

Search through installed services for `` image_path `` fields with known remote access tool filenames, `` service_names ``, or `` registry_paths `` associated with remote access tools.

Example service name: `` TeamViewer Remote Software ``

Document any services, hostnames, and user accounts

### Step 3 - Identify Use of Remote Access Tools through Collected Files

Compare the observed filenames with filenames contained in the file Version Information metadata to identify remote access tools masquerading as a different files.

Search for file signatures referencing known remote access tools.

Document any files, hostnames, and user accounts

### Step 4 - Identify Use of Remote Access Tools through Domain Resolution

Search through netflow or DNS logs to find hosts communicating with known cloud remote access providers. If necessary, resolve any internal IP addresses to their associated hostnames

Document any hostnames and domains

For each data source, attempt to deduplicate the data so that you have list of unique hosts and the names of the remote access tools found on them.


## Analysis


> Did you find any remote access tools that were not approved for use by corporate policy? If unapproved remote access tools were found, can the use of these tools be attributed to Shadow IT?   


> Did you find any hosts with artifacts from multiple remote access tools?


> Did you find any remote access tools masquerading as other files?


> Did you find any evidence of remote access tools running in the context of service or other privileged accounts?


> Did you find any evidence of explicit credentials passed on the commandline for a remote access tool? If so, what kind of systems were these remote access tools found on? Do any of these systems hold special importance for the client or their infrastructure (ie, domain controllers)?


<!-- #region tags=["remove_cell"] -->

## Outputs

### Threats

*   The identification of unapproved remote access tools

### Countermeasures

*   Does the client want to change how they are alerted for remote access tools? If so, consider either suppression rules or domain-specific watchlists.
*   Does the client want to block the execution of specific remote access tools to assist with remediation? If so, consider blacklisting relevant files by hash or blocking traffic to the remote access service provider.

### Recommendations

*   Did the client have the necessary data available to perform this analysis?
*   To prevent the use of unapproved remote access tools, the client should consider Software Restriction Policies or Application Whitelisting.
*   If Shadow IT is responsible for the use of unapproved remote access tools, then the client should consider vetting and institutionalizing a viable remote access tool.

## Future Research

*   Need to expand lists of remote access tool indicators, such as file names, service names, file signing information, etc.
*   Consider expanding data collection to include information from SCCM or other software auditing tools.
*   Consider future playbook that describes how to collect data from remote access tool logs to identify file copies, client IP addresses, etc.

## References

*   None

## Change History

|Date|Author|Description|
|---|---|---|
|2019-01-30|Ryan Cobb|First Release|
|2019-06-18|John Drafke|Added 41 process execution additions and searches|
|2019-09-10|John Drafke|Added 15+ process execution additions, removed several FPs, updated advanced query searches for New Portal|
|2020-02-06|Matthew Hajski|Added "RPCSuite.exe" to advanced searches. Found during normal ATH workflow, related to RPCProxyLatency.exe and RemotePCService.exe which are already included in the playbook.|
|2020-02-26|Matthew Hajski|Added binaries and command-lines related to Netop Remote Control to both advanced searches|

<!-- #endregion -->

```python
save_report(notebook_filename, format='md') # or save_report(notebook_filename, format='html')
```
