# EventLog-CheatSheet
Searching through event logs is a daunting task.  
This cheat sheet is made to be a simple way for security practitioners to go through useful logs and find adversary activity.  
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
  
There are various ways of logging in to a system.You can use the Microsoft docs to learn about different [logon types](https://docs.microsoft.com/en-us/windows-server/identity/securing-privileged-access/reference-tools-logon-types) that exist. 
  
Before we start it is first vital that we explain the difference between Account logon and logon.  
Logon refers to local login activity that occurs on the local system hence the log will be generated on the local system.  
Account Logon refers to third party authentication. In an enterprise domain users authenticate to the domain controller because of that you will generate logs on the DC and the local system. If you login using a local account Account logon events will be generated on the local system.  

### Logon
4624: Logon  
4625: Failed Logon  
4634,4647: Successful Logoff  
4648: Logon using explicit credentials   
4672: Account logon with superuser rights (special logon)  
4720: An account was created   
4726: An account was deleted  

#### How to  
For 4624 you must whitelist DWM and UMFD.  
When a logon and logoff event have the same Logon ID the time can be used to determine the session length.  
Using 4625 with logon type 3 (network) we can detect brute force attacks against a system.  
4672 special logon is great for detecting privileged users it is common to see a 4624 and 4672 together this means that an admin account logged in to the system.  
When looking for admin accounts it is important that you whitelist built-in windows accounts because these accounts login frequently and create special logons.  
4720 is very straight forward if an adversary creates an account this event will detect it.  


### RDP
4778: Session Reconnected  
4779: Session Disconnected  
Logon Type 7 and 10  
There are also other channels to look for RDP events  




### Account logon
NTLM  
4776: Successful/Failed account authentication  
In an enterprise local ntlm authentication is rare so seeing local 4776 should interesting and should be analyzed.  
A combination of network logon 4624 type 3 and account logon for ntlm 4776 can be an indicator or pass the hash.  
  
Kerberos  
4768: Ticket Granting Ticket was granted   
4769: Service Ticket requested   
4771: Pre-authentication failed   










