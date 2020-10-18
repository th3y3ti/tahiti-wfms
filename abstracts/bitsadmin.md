# Abuse of Background Intelligent Transfer Service (BITS)

## Hypothesis
Adversaries are abusing BITS

## Description
Brief description of the TTP or behavior you are looking for.

## Review Existing Watchlists
- Powershell BITSAdmin Downloader
- https://redcloak.secureworks.com/portal/countermeasures/watchlists/2335c235-a96f-4d5c-a5a1-b28a3865980a

- BITSadmin Suspicious Job Completion
- https://redcloak.secureworks.com/portal/countermeasures/watchlists/fc36c80b-e86a-458a-b7c6-408a837c95a5

- Suspicious BITSadmin Command
- https://redcloak.secureworks.com/portal/countermeasures/watchlists/6344866e-a022-4425-bff0-7a11c4185614

- Bitsadmin Job Will Launch Executable
- https://redcloak.secureworks.com/portal/countermeasures/watchlists/bf16fb0e-89d7-47cb-be35-7ce142a288e2

- BITSadmin File Transfer
- https://redcloak.secureworks.com/portal/countermeasures/watchlists/d02f4bee-c97f-413a-8eb4-2ffd3c6e9b40

- Suspicious BITSadmin Command 2
- https://redcloak.secureworks.com/portal/countermeasures/watchlists/dfc8a09c-ce3d-40dd-b7c4-924a57dae9f3

- BITSadmin Command Sending Host Information
- https://redcloak.secureworks.com/portal/countermeasures/watchlists/1066378c-a6f2-40ed-9129-0d6b457425e9

- BITSAdmin Uploader
- https://redcloak.secureworks.com/portal/countermeasures/watchlists/210cd919-2b19-42d9-b964-db5282dc0997

- BITSAdmin File Download
- https://redcloak.secureworks.com/portal/countermeasures/watchlists/8c4b6b3a-2715-421e-a0b1-0a982901e4af

- BITSadmin file transfer 2
- https://redcloak.secureworks.com/portal/countermeasures/watchlists/9f35af58-2660-4b6e-aead-6a9fad8a9f15

- Suspicious stop of Background Intelligent Transfer (BITS) service
- https://redcloak.secureworks.com/portal/countermeasures/watchlists/37db7cd7-b029-4140-9948-8a80fb7f2f01

## Analytic 1 - Investigate Processes and Commandlines
`image_path:bitsadmin.exe AND -commandline:(list OR getieproxy OR reset OR setieproxy OR info)`

`commandline:"bitstransfer" AND -commandline:"allusers"`

`commandline:SetNotifyCmdLine`

## Reference(s)
https://isc.sans.edu/forums/diary/Investigating+Microsoft+BITS+Activity/23281/
https://www.dfrws.org/sites/default/files/session-files/pres-finding_your_naughty_bits.pdf
http://0xthem.blogspot.com/2014/03/t-emporal-persistence-with-and-schtasks.html
