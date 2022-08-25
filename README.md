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
Account Logon refers to third party authentication



