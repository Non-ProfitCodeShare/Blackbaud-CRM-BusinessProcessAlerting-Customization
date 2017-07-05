## Process Management
This is a customization which alerts when a business process runs longer than the specified time. 

This customization takes all previous runs of a business process, calculates the mean for their 
run time, then takes x number of standard deviations + y number of seconds of fudge factor 
then adds these together and sends an email alert if any business process is running outside of that 
window. 

We set ours to 800 seconds + 2 standard deviations which seems to work well for us. 


To deploy: 
1. Copy the dll to the /bin/custom folder. 
2. Load it
3. Create the global change called "BPAlerting - LoadStatsTable Global Change"
	a. Fudge factor is the number of seconds to be added to the standard deviations that you specify.
	b. The number of standard deviations to use for a threshold. 
4. Save and run the global change
5. Set this up to run / refresh the statistics on the table at a reasonable rate... 
	can be 4 times a day or maybe once a day or once an hour. 
6. Go to Administration -> Email Alerts -> Custom Email Alert Types
7. Click Add
	a. Set the email subject and body to whichever values you want. Ours are posted below for a reference. 
	b. Add an instance
	c. Add users to this instance
	d. Create a job schedule 
	e. We set ours to run every 5 minutes but it's up to you. 
8. Done. 




Email Body Example: 
Alert for Business Process: <<BUSPROCTYPE>>
Business Process Instance: <<BUSPROCNAME>>

Started On: <<STARTEDON>>
Running for: <<DURATION>>
Status: <<STATUS>>

Alert Started At: <<ALERTSTARTEDON>>
Mean run time: <<RUNTIMEMEAN>>
Our grace period: <<RUNTIMESTDDEV>>

Error Message:<<ERRORMESSAGE>>

Current Running Business Processes: 
https://link-to-the-current-running-business-process-in-crm

Business Process Alerting History: 
https://link-to-the-business-processes-history-in-crm