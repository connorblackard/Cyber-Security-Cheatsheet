## Incident Response 

### Process
1. Preparation
2. Detection
3. Analysis
4. Containment
5. Eradication
6. Recovery
7. Post Incident/Lessons Learned

### Investigation Questions
Investigating an event/incident untimely comes down to asking and answering questions. One of more questions will need to be answered before being able to close or action an alert. Below is a non-comprehensive list of example questions that may be asked during an investigation. As your experience grows as an analyst, so will your skill in identifying which questions are relevant and which questions should be prioritized.

- Were there any unusual login activity?
- Were there any successful logins?
- Were there any failed login attempts? How many?
- Has activity been seen from this IP address before?
- What users have logged in from this IP address?
- Has this account done this type of activity before?
- Are there any past alerts or incidents may be related?
- Is the file digitally signed?
- When was the file created?
- Did any installation activity/system maintenance happen around the same time?
- Who was logged in at the time?
- Where did the file originate from?
- Is this activity disallowed by organizational policy?
- What do the command line parameters mean?
- Is this file normally in this location?
- Does the users job role make sense for this action?
- What application does this server run?
- Is this server internet facing?
- Does this email sender regularly interact with other users?
- Was the link clicked?
- Was anything downloaded from the site?
- Were there external data transfers? What size?
- What service does this port belong to?

Additional Resources:
- https://chrissanders.org/2016/05/how-analysts-approach-investigations/

*** 
[Return to home page](../README.md)