# Brute Force-SUCCESS-Windows

Work the incidents being generated within Azure Sentinel, in accordance with the
NIST 800-61 Incident Management Lifecycle. 

Step 1: Preparation
(Already initiated this already by ingesting all of the logs into Log Analytics Workspace and Sentinel and configuring alert rules)

Step 2: Detection & Analysis 

Set Severity, Status, Owner

Beginning by setting the Severeity Status and Owner. Shown below I will engage highlighted box and set owner of ticket and set status to "active". In this instance due to our setup of our enviornment the severity already was generated along with ticket.

<img width="1150" alt="Screenshot 2024-12-17 at 1 45 37 PM" src="https://github.com/user-attachments/assets/79935524-47e4-4bf3-a8aa-c340467abe67" />


![image](https://github.com/user-attachments/assets/8b5cc096-b616-4e3f-9dd1-d3d09a429245)

View "Full Details" of incident

![image](https://github.com/user-attachments/assets/00616c00-8d25-4ac4-82f7-eb29f5c6633a)

![image](https://github.com/user-attachments/assets/1d7023a5-dea8-4e5d-ad5e-d3f4ba861863)
Observe the Activity Log (for history of incident)
![image](https://github.com/user-attachments/assets/929c77ee-6e13-42cd-ae63-0bc18d516331)

Observe Entities and Incident Timelines (are they doing anything else?)
![image](https://github.com/user-attachments/assets/f5fe1084-58d2-4c42-92d1-8182a94c6aa0)

“Investigate” the incident and continue trying to determine the scope

![image](https://github.com/user-attachments/assets/1acd2ff4-4cb8-45a9-af41-36b4c4da6186)

Inspect the entities and see if there are any related events

![image](https://github.com/user-attachments/assets/bfa73a26-41bd-44f8-84c4-e3e9209fe0a9)

Created some notes based off related events involving Attacker/Enitity I.P and Windows VM

CUSTOM: Brute Force SUCCESS - Windows
Incident ID 4
Looks like there is 1 alert triggered for this, which is expected because we tested our enviornment and this alert correlates to our test.
Attacker/Entity "70.125.56.206" is also involved in other test and is matches a familiar I.P used for testing.
Potentially compromised system "windows-vm" involved in several other incidents/ alerts not including test. Possible overexposure to the public Internet
Inspected actions from 70.125.56.206, there were several incidents involving enitity from the service account but upon further investigation, it was found that the alert raised was a false positive created by a service account.

Though the alert was a false positive, other traffic found that is reaching VM is troubling and needs to be rectified.

Closing out incident as false-positive, but will start the processes for hardening.

Determine legitimacy of the incident (True Positive, False Positive, etc.)
If True Positive, continue, if False positive, close it out. In this case this is a Benign Positive.

![image](https://github.com/user-attachments/assets/43e9fc78-0e97-45b4-a176-e9da1141053d)


Step 3: Containment, Eradication, and Recovery

Need to setup some protection for Windows VM given we found so many unexpected incidents involving it.

Navigated to Virtual machines and selected VM in question "Windows VM"
![image](https://github.com/user-attachments/assets/8e182966-78f9-49c7-a538-b799a6f593ea)

Then navigated to Networkwork settings to add Inbound Port Rule
![image](https://github.com/user-attachments/assets/4f14ca23-481f-4d63-93df-ac2501997085)

![image](https://github.com/user-attachments/assets/7733d7fd-d82d-47a1-ad94-2651c6f7e6db)

Changed source to " My IP Address". Allowed any traffic from personal I.P address which in turn denies traffic from other I.P's

Step 4: Document Findings/Info and Close out the Incident in Sentinel

Already closed out incident but here my notes for incident. 

Notes: Brute Force SUCCESS - Windows
Incident ID 4
Looks like there is 1 alert triggered for this, which is expected because we tested our enviornment and this alert correlates to our test.
Attacker/Entity "70.125.56.206" is also involved in other test and is matches a familiar I.P used for testing.
Potentially compromised system "windows-vm" involved in several other incidents/ alerts not including test. Possible overexposure to the public Internet
Inspected actions from 70.125.56.206, there were several incidents involving enitity from the service account but upon further investigation, it was found that the alert raised was a false positive created by a service account.
