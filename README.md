# EventLog-CheatSheet
Searching through event logs is a daunting task.  
This cheat sheet is made to be a simple way for security practitioners to go through all the logs and find adversary activity.  
Events can be written to event log channels and each event has an event ID.   
Common channels are:  
* Security
* System
* Application  

There are 4 channel types:  
* Common
	- Administrative 
	- Operational
* Uncommon
	- Debug
	- Analytic



Our main focus will be on the security channel because it's the most relevant.  

## User/Account Activity
There are various ways of logging in to a system.You can use the microsoft docs to learn about different [logon types](https://docs.microsoft.com/en-us/windows-server/identity/securing-privileged-access/reference-tools-logon-types) that exist. 
  
Before we start it is first vital that we explain the difference between Account logon and logon.  
Logon refers to local login activity that occurs on the local system hence the log will be generated on the local system.  
Account Logon refers to third party authentication. In an enterprise domain users authenticate to the domain controller because of that you will generate logs on the DC and on the local system.  
If you login using a local account Account logon events will be generated on the local system.  

### Logon
4624: Logon
4625: Failed Logon
4634,4647: Successful Logoff
4648: Logon using explicit credentials (RunAs)
4672: Account logon with superuser rights (special logon)
4720 : An account was created 
4726 : An account was deleted

#### How to

for 4624 you must whitelist DWM and UMFD  
Interesting fields are:  
Logon type, Computer, Account, date and time, Logon ID  
When a logon and logoff event have the same Logon ID the time can be used to determine the session length.  
Using 4625 with logon type 3 (network) we can detect brute force attacks against a system.  
4672 special logon is great for detecting privileged users it is common to see a 4624 and 4672 together this means that an admin account logged in to the system.  
4720 is very straight forward if an adversary create an account this event will detect it.  


### RDP
4778: Session Reconnected  
4779: Session Disconnected  
Logon Type 7 and 10  
There are also other channels to look for RDP events  




### Account logon










