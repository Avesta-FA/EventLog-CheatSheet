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
For 4624 you must whitelist DWM and UMFD.  
  
4625: Failed Logon  
Using 4625 with logon type 3 (network) we can detect brute force attacks against a system.  

  
4634,4647: Successful Logoff  
When a logon and logoff event have the same Logon ID the time can be used to determine the session length.  
  
4672: Account logon with superuser rights (special logon)  
Special logon is great for detecting privileged users it is common to see a 4624 and 4672 together this means that an admin account logged in to the system.  
When looking for admin accounts it is important that you whitelist built-in windows accounts because these accounts login frequently and create special logons.  
  
4720: An account was created  
4720 is very straight forward if an adversary creates an account this event will detect it.  
4726: An account was deleted  
  
  
### Groups
4728: A member was added to a security-enabled global group  
4732: A member was added to a security-enabled local group  
4756: A member was added to a security-enabled universal group  
These are great for monitoring Administrator groups    

 

### RDP
4778: Session Reconnected  
4779: Session Disconnected  
Logon Type 7 and 10  
There are also other channels to look for RDP events.  
These logs give us information about hostname and IP addresses.  



### Account logon
NTLM  
4776: Successful/Failed account authentication  
In an enterprise local NTLM authentication is rare so seeing local 4776 should be interesting.  
A combination of network logon 4624 type 3 and account logon for NTLM 4776 can be an indicator of pass the hash.  
  
Kerberos  
4768: Ticket Granting Ticket was granted   
4769: Service Ticket requested   
4771: Pre-authentication failed   

### Enumeration
4758: A user'slocal group membership was enumerated  
4755: A security-enabled local group membership was enumerated  
These events were added with windows 10 and it allows you detect reconnaissance activity in the network.  
You will need to whitelist mmc, services, taskhostw, explorer and focus on important groups and accounts.  


### USB
4663: An attempt was made to access an object  
4656: A handle to an object was requested  
6416: A new external device was recognized by the System  


### Log clearing
1102: The audit log was cleared  
In the system channel look for:  
104: The audit log was cleared

### Services
4697: A new service was installed on the system  
7045: A new service was installed on the system   
7040: Start type changed   
7036: Service started or stopped  
Services are a great way to escalate privileges or persist on a system.  



### Network Share  
5140: Network share was accessed  
5145: Shared object accessed  
Adversaries might use shares to laterally move in your environment.  
Adversaries will commonly use these shares: C$, ADMIN$, IPC$  


### RunAs  
4648: Logon using explicit credentials   
This event can occur during RDP, Network share, Process creation, and etc.  
It is a great way to detect how an adversary is moving from one compromised account to another.  


### Scheduled Tasks  
4698: Scheduled Task Created  
4699: Scheduled Task Deleted  
4700: Scheduled Task Enabled  
4701: Scheduled Task Disabled  
4702: Scheduled Task Updated  

You can also look into the Task Scheduler channel  
106: Scheduled Task Created  
140: Scheduled Task Updated  
141: Scheduled Task Deleted  
200: Scheduled Task Executed  
201: Scheduled Task Completed  

### Registry  
4657: a registry value was modified   




