## Challenge Brief

<img width="600" height="314" alt="image" src="https://github.com/user-attachments/assets/3e7406ac-c968-4014-8ad9-8ffc9fdec929" />

## Scenario
Can you analyze logs from an attempted RDP bruteforce attack?

One of our system administrators identified a large number of Audit Failure events in the Windows Security Event log.

There are a number of different ways to approach the analysis of these logs! Consider the suggested tools, but there are many others out there!
   
## Question 1) How many Audit Failure events are there? (Format: Count of Events)
Open the Excel file and filter the 'Event ID' column to 4625; the resulting record count indicates the number of failure events. There were `3103` failure events.

<img width="877" height="785" alt="image" src="https://github.com/user-attachments/assets/a0a46460-a0a0-4fa1-b793-61a976e791e0" />

## Question 2) What is the username of the local account that is being targeted? (Format: Username) 
Convert the EVTX file with GKape using Eric Zimmerman's EZParser. The payload targeting the `administrator` was identified.

<img width="1688" height="112" alt="image" src="https://github.com/user-attachments/assets/c4aaa64e-0b89-4583-aef6-724977b7277f" />

## Question 3) What is the failure reason related to the Audit Failure logs? (Format: String) 
Open the provided text file and use Ctrl+F to search for 'Failure Reason.' The result indicates the failure was due to an `unknown user name or bad password`.

<img width="752" height="165" alt="image" src="https://github.com/user-attachments/assets/9a11f27a-6368-4a94-812b-f37c75142953" />

## Question 4) What is the Windows Event ID associated with these logon failures? (Format: ID) 
Refer to Question 1, the Event ID is `4625`.

## Question 5) What is the source IP conducting this attack? (Format: X.X.X.X) 
`113.161.192.227`

<img width="712" height="418" alt="image" src="https://github.com/user-attachments/assets/d6094d65-4afc-4300-b5af-f298c560c947" />

## Question 6) What country is this IP address associated with? (Format: Country) 
Analysis via public threat intelligence tools indicates the IP address originates from Viet nam. 

<img width="760" height="479" alt="image" src="https://github.com/user-attachments/assets/45fe64d0-6d2f-458c-9729-3b52f2cd412b" />

## Question 7) What is the range of source ports that were used by the attacker to make these login requests? (LowestPort-HighestPort - Ex: 100-541)
Open Windows PowerShell, navigate to the text file's directory using cd, then run the following command to extract and sort the source ports, identifying the lowest and highest values:
```powershell
Select-String "Source Port:" BTLO_Bruteforce_Challenge.txt | 
ForEach-Object { ($_ -split ':')[-1].Trim() } | 
Sort-Object {[int]$_}
```
Lowest Value: 

<img width="551" height="264" alt="image" src="https://github.com/user-attachments/assets/57e5e8bd-a10b-4d16-a860-e198e578d476" />

Highest Value:

<img width="445" height="138" alt="image" src="https://github.com/user-attachments/assets/35cf7cc7-c978-4917-a727-5acfd940d12f" />

