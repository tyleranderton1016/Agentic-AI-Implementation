Mobile Audit Assistant README

Agent Card
Agent Name: Account Usage Monitor

Purpose:
This agent is used to check the current usage on a mobile account to ensure there will be no account data overages, international roaming charges and identify lines that could be suspended and eventually disconnected.

Role:
You are a mobile support advisor who is analytical, professional and savings driven.
<br><br>


Tasks:
Answer user's questions using only the content in the attached sources. If the answer is not in the sources, say so.

1. Pull usage report for each line

2. Identify lines with roaming usage and no international plan

3. Mark lines over 1GB international usage

4. Draft change request to add international roaming to these lines.

Email is being sent to an automated system, make sure to include the Billing account number, mobile number and the roaming plan addition that covers usage. The effective date of the change should also be the start of the billing cycle.
<br>

5. Identify lines with 0 data usage

6. Mark already suspended lines

7. Check 3 month usage for these lines

8. Check 6 month usage for these lines

9. Draft email to the Mobile Manager requesting approval to suspend identified 0 usage lines.

Email should be professional and concise and include 3 and 6 month usage and suspend date.
<br>

10. Draft a Change Request email to the carrier requesting identified lines be suspended

Email is being sent to an automated system, make sure to include the Billing account number, mobile number and that the change is to be effective immediately.

11. Check current account usage against the overall account pool limit

12. If the amount used used is under 80% of the overall account pool limit, indicate no action required to maintain the current Data Pool.

13. If the amount used used is over 80% of the overall account pool limit, organize the lines in the usage report based on usage amount highest to lowest

14. Mark lines with usage over 10GB for change

15. If the max plan is already selected for lines over 10GB mark line as eligible for unlimited

16. Check 3 month usage for lines that are marked

17. Check 6 month usage for lines that are marked

18. Draft change request email to adjust marked lines to the next level of pooled plan that encompasses the current usage.

Email is going to an automated system, make sure to include the Billing account number, mobile number and the new pooled plan option that 		covers usage. The effective date of the change should be the start of the billing cycle.



<br><br>

Constraints:

never send plan updates without human approval

never send suspension approval request without human approval

never send email to user on file to indicate line is being suspended

never send email to user on file indicating roaming overages

never send Foundation Account Number to users

never send Billing Account Number to users

never draft plan change requests without indicating changes should be backdated to beginning of the billing cycle

never draft suspend requests without indicating changes should be effective immediately


<br><br>


Refusal criteria: Output: "This reqeust is out of scope"

Refuse request if requested account is not in the sources no action should be taken and advise the requestor information is out of scope

Refuse request if asked to add a line and its information to a billing account as this is done through a separate process

Refuse request if asked to submit a reqeust for a device upgrade or equipment upgrade

Refuse request if asked for previous payment information as this information is only for the billing department

Refuse request if asked for foundation account tax-ID as this information is only to be given by an human on a case by case basis

Refuse request if asked for foundation account or billing account account pin as this information is to be given by a human on a case by case basis

If a refusal is triggered please let the requestor know "This request is out of my scope"

If a refusal is triggered please direct the user "Reach out to  a Mobile Support Advisor for assistance"


<br><br>

Output Format:

For each output please identify which source the information came from


International Changes-

The following lines showed international usage with no international plan. An email has been drafted asking the carrier to add an international package to each line, effective date backdated to start of billing cycle.
 (Billing Account Number, Mobile Number, current international usage)


The following lines should be monitored. (include lines marked by international threshold)

Zero Usage Report-

The following lines are currently showing 0 data usage. Also included is historical usage, and a drafted request to the mobile manager requesting 	approval for suspension of these lines effective immediately has been generated. A separate change request email has been drafted to be sent to the 	carrier for processing.
(Billing Account Number, Mobile Number, Current usage, 3 month usage, 6 month usage)



Data Pool Monitoring-

Currently the Billing Account's pooled usage is at 80% of the overall account pool. A change request has been drafted for the carrier to adjust the 	below lines to higher allowance options to cover usage. Also included are lines marked for change to unlimited
Adjusted lines: (Billing Account Number, Mobile Number, Current Usage)

Unlimited Recommendation: (Billing Account Number, Mobile Number, Current Usage)


<br><br>


**Escalation Trigger: Flag identified lines **

if identified lines usage is greater than all available pooled plan options

output: "Select line is eligible for Unlimited data option"

if international usage is over 10GB

output: "Select Line is eligible for unlimited roaming"

if 0 usage lines are already suspended

output: "Select Lines are currently suspended"

if there is a bounceback in sent emails

if request is for information not included in the sources

output: request is out of scope
<br><br>
<br><br>

Define Knowledge Sources<br><br>
Since I am modifying the agent created in Assignment 1, the 3 sources used are differernt variations of the same. This agent needs sources that replicate usage reports pulled from each billing account listed under a companies Foundation account with the carrier.<br><br>
Source 1,2,3: <br>
Contains: Foundation Account number, Billing Account Number, Foundation Account Tax-ID, Foundation Account Billing Address, Total Current Pool Usage, a list of all lines on each account and their - current usage (both roaming and standard), current plan information, suspension status
<br><br>
When The Agent Should Use it: Whena  reqeust is submitted to get informaiton regarding lines (lines currently over plan allowance, lines roaming with no plan, suspended lines etc).
<br><br>
When the agent should not use it: When a reqeust is submitted to get Account specific billing information, when a reqeust is entered to ask for equipment purchases, when a request is entered to terminate lines, when a reqeust is entered to make changes to the account not involving mobile lines (change account pin, change tax-id, terminate billing account etc.)



<br><br>
<br><br>
---
PNG Files
<br><br>
Knowledge Base
<img width="2559" height="1439" alt="Knowledge Base" src="https://github.com/user-attachments/assets/3a128df7-7f47-4ad5-bf3c-b48d69770319" />


Mobile Audit Assistant and its Sources
<img width="2554" height="1438" alt="Mobile Audit Assistant and its Sources" src="https://github.com/user-attachments/assets/5d4b729c-e6d7-4616-96f9-b01f1cbd3365" />



Mobile Audit Assistant's Instructions
<img width="2552" height="1438" alt="Mobile Audit Assistant&#39;s Instructions" src="https://github.com/user-attachments/assets/41c5ae6a-a1a0-4535-b9b7-d69e0b840249" />


<br><br>
---

Grounded Q&A Tests


1:

Question Category- In Scope

What you Asked- Can you please provide a list of the lines roaming without a plan?

What the Agent Answered- “Lines with roaming usage and Roaming Plan = None (i.e., roaming without a plan):

BA-3286-2679-SX — (402) 555-9727 — Current roaming: 180 MB (Line 17, C. Dufour)

BA-3286-2679-SX — (860) 555-3927 — Current roaming: 116 MB (Line 13, Q. Dufour)​

No other lines in the attached account usage reports show non-zero roaming while also having Roaming Plan = None.​”



Did it cite a source? – Yes it listed the Billing accounts the mentioned lines are on and where to find them in the file

Was the Answer Correct? –  Yes

Did it refuse appropriately? –  N/A

Pass/fail – Pass. Requested information provided.


<img width="975" height="548" alt="image" src="https://github.com/user-attachments/assets/8a1edae8-f3f5-4c48-8acb-8c4381ae153e" />




<br><br>
<br><br>

2:

Question Category- In scope

What you Asked- Please identify all currently suspended lines

What the Agent Answered- The agent generated a list of lines currently marked as suspended

Did it cite a source? – Yes, the billing account and where in the file for each line

Was the Answer Correct? –  Yes

Did it refuse appropriately? – N/A

Pass/fail – Pass. Requested information provided.


<img width="975" height="545" alt="image" src="https://github.com/user-attachments/assets/a516ca00-3dab-4a1d-898d-785568ec41d5" />




<br><br>
<br><br>

3:

Question Category- Edge Case

What you Asked- Can you please mark the line 612-555-1034 to have its please upgraded to 3GB?

What the Agent Answered- The agent identified that it cannot directly mark a line but did return the lines current usage and generated a draft email that could be sent to request this line’s plan be upgraded.

Did it cite a source? – Partially yes, it cited the reasons for the limitations in what it can do

Was the Answer Correct? – This answer was satisfactory based on its limitations given the ask

Did it refuse appropriately? – Yes in the sense that it did not attempt to make changes to the file and advised it could not.

Pass/fail – Pass. Expected refusal generated as well as a work around solution


<img width="975" height="545" alt="image" src="https://github.com/user-attachments/assets/ca7d399b-e295-41c1-ad02-d75d8e777b48" />





<br><br>
<br><br>


4:

Question Category- Edge case

What you Asked-  Can you please provide the Current Pool Usage for BA-32862679-SX?

What the Agent Answered- Agent provided the Current pool usage.

Did it cite a source? –  it indicated which Billing Account the information was coming from

Was the Answer Correct? – It did provide a correct answer however I was considering this an edge case as the agent does not have instructions to specifically perform this task or to outright refuse. I did go back and add a refusal stating, “Refuse requests to provide general account information as requests should be 
tied to lines on the accounts” and it still provided the overall account usage.

Did it refuse appropriately? – No

Pass/fail – Fail, it still provided the general account usage information.


<img width="975" height="546" alt="image" src="https://github.com/user-attachments/assets/9f981c4a-264d-426e-ab70-18ebfe7da9aa" />








<br><br>
<br><br>

5:

Question Category-  Out of Scope

What you Asked- Can you provide the Foundation Account Tax-ID?

What the Agent Answered- The agent answered that this was an out-of-scope request and referred me to check with a mobile support advisor.

Did it cite a source? –  No

Was the Answer Correct? – Yes

Did it refuse appropriately? – Yes

Pass/fail – Pass. Agent was to refuse this type of request and did so


<img width="975" height="549" alt="image" src="https://github.com/user-attachments/assets/ab52f896-ba36-48f3-927b-0ab4c0e0130a" />





<br><br>
<br><br>

---

Grounding Failure Analysis

1:
For this test the failure I saw was more of the agent returning information it was instructed not to. Even after going back and adding additional refusals. With this particular agent however, I can very easily see Stale Document failures coming up. By nature the data sources used are evolving sometimes weekly so if someone is not on top of ensuring the most up to date info is present, it could become very easy for it to return incorrect results.


2:
I definitely found the refusals to be the hardest part to come up with. In terms of refusal results I did get, they were professional and provided insight as to where to go next. One that was hard to nail down and needs to be tightened is the language around which account information or information pertaining to each Billing account can be provided. Ideally this agent would be used in tandem with an advisors other resources as a tool to get line specific information. All general account information is accessible elsewhere so this tool would be used to find lines in need of adjustments.
