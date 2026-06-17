
Workflow Description
<br><br>
1a - Name: Mobile Audit<br>
	What triggers it: Usage report is uploaded<br>
	What the end product is: Files with lines that should be reviewed for possible plan changes<br>
	who would normally do each step manually: Mobile support advisor<br><br>

1b - Agent design<br>
	Agent Name: International Reviewer<br>
	Role in one sentence: This agent checks for lines that show roaming usage and ensures they have a plan that covers usage
	tools it needs: excel or google doc, email, ticketing system, file read<br>
	tools it does not need: web access, carrier access, access to billing information, access to end users<br><br>

	Agent Name: Data Pool Reviewer
	Role in one sentence: Checks the overall pool of data to determine if changes need to be made to increase the amount of data. Identifies which lines are causing the most drain
	tools it needs: excel or google doc, email, ticketing system, file read
	tools it does not need: web access, carrier access, access to billing information, access to end users

	Agent Name: Historic Reviewer
	Role in one sentence: Reviews the usage of lines for the past 30,60,90 days to identify lines that could be moved to unlimited or suspended
	tools it needs: excel or google doc, email, ticketing system, file read
	tools it does not need: web access, carrier access, access to billing information, access to end users

<br><br>
1c - Orchestration patterns<br>
	Sequential or Hierarchial and why: Sequential due to one file being processed with different tasks that are similar in work type. Each agent can take the file and generate what they need from it before passing it along to the next agent to do the same.<br><br>

1d - Human checkpoint<br>
	1. which task is it, and why is that the right place to pause? The task is reviewing the findings and should take place before anything is sent to the carrier for processing.<br>
	2. what would a reviewer need to see in the approval packet? Name five fields, no more: Reviewer would need to see; mobile number, current plan, current usage, % of the pool it is taking up/potential overages for roaming, plan recommendation<br>
	3.is the action that follows the checkpoint reversible or not? Not entirely. Once the request is sent to the carrier for processing the automated system will action the request no matter what. In order to reverse you need to send a follow up and it is not guaranteed that it will be actioned in time.<br><br>




AI Copilot’s initial canvas
<img width="2558" height="1438" alt="Benchmark" src="https://github.com/user-attachments/assets/b3758272-1ca5-4e22-ac61-91283afc7b51" />

 <br><br><br>


Final Canvas with process type Dropdown
<img width="2551" height="1428" alt="Final Canvas with Thought Process" src="https://github.com/user-attachments/assets/56274c21-419f-44f9-8002-5c7fa5eb98c4" />

 <br><br><br>


Settings panel for human-checkpoint
<img width="2547" height="1424" alt="Human Approval" src="https://github.com/user-attachments/assets/8da434c8-dfbf-4112-9938-45c5f68a9248" />

 
<br><br><br><br>



Part 3<br><br>

Analyze International Roaming Usage<br>
	What input was received: mobile_usage_report.csv<br>
	What output was produced: Through several iterations of .xls and .csv file still getting the message I'm currently unable to access the usage report file to provide a detailed analysis as required. Please verify the file's availability or provide the necessary data for me to analyze the mobile usage and recommend appropriate plans.<br>
	Whether the handoff looks correct: No
<br><br>
Analyze Data Pool Usage and Optimization<br>
	What input was received: mobile_usage_report.csv<br>
	What output was produced: File not found. Please provide the necessary data for analysis.<br>
	Whether the handoff looks correct: No<br><br>

Historical Usage Pattern Analysis<br>
	What input was received: mobile_usage_report.csv<br>
	What output was produced: The required file is not accessible, and no data is available for analysis. Please provide the necessary data for analysis.<br>
	Whether the handoff looks correct: No<br><br>

Consolidate Mobile Audit Results<br>
	What input was received: mobile_usage_report.csv<br>
	What output was produced: The required file is not accessible, and no data is available for analysis. Please provide the necessary data for analysis.<br>
	Whether the handoff looks correct: No<br><br><br>

Human Approval<br>
	run time: 6.3s<br>
	No human was asked to enter anything<br>
	Approval output: Please provide approval to proceed. Approved by: [Your Name] Approval Timestamp: 2026-06-15<br><br>

Generate Change Request<br>
	What input was received: In theory it would have gotten the Consolidated Mobile Audit Results and approval<br>
	What output was produced: An email draft that can be sent to the carrier for processing<br>
	Whether the handoff looks correct: Yes this looks correct<br><br><br>



Run Tab Timeline<br>
<img width="2551" height="1431" alt="Timeline Panel Completed Tasks" src="https://github.com/user-attachments/assets/0d0f1060-df80-418b-9da2-086cd0c38e8f" />

 
<br><br><br>


Full governance audit<br>


Design vs reality:<br>
	1. For each of the agents I added the Search a CSV's Content and Google sheets tools in an attempt to make it easier for each tool to process possible inputs for this task.<br>
	2. Yes it did pick the same. It seemed to follow the same logic of having the file passed along so each agent could get the necessary information out of it. I did also think it could have gone with Hierarchical and had a "manager" give the file to each agent so they could work simultaneously but there may be limitations with doing this and only having 1 file. <br>
	3. The main part that I did not understand was its beginning was a triggers where I did not have any options to work with excel or google sheets. I could only choose to have this run via a teams message, email, calendar event or Microsoft oneDrive update. It did not give me any opportunity to add excel access.<br><br><br>


tool scope table<br>
	Tools in Part 1b Plan:<br>
	International Reviewer<br>
	Data Pool Reviewer<br>
	Historic Reviewer<br>
<br>

	Tools in Final Crew:<br>
	Analyze International Roaming Usage<br>
	Analyze Data Pool Usage and Optimization<br>
	Historical Usage Pattern Analysis<br>
	Consolidate Mobile Audit Results<br>
	Human Approval<br>
	Generate Change Request<br>
The final product did include a match for each of the tools I had outlines with the difference being it added in a tool for consolidating the results, getting approval and generating an email that can be used to submit a change request.
<br><br><br>

threat class table<br>
	Prompt Injection: A prompt injection could be someone asking for billing account or foundation account information. I believe the crew has some mitigations for this as it was initially defined stating it should not have access to billing information in the tools it does not need. The outputs it generates also would ultimately be reviewed by a human before anything is sent externally.<br>
	Tool Abuse: This could look like an agent overriding information in a file rather than just reading from the file. From what I can see from the tool descriptions they appear to be read only. The only tool I am concerned with is the google sheets access.<br>
	Over-permissioning: This could look like an agent having access to billing information. There is mitigation built in with setting the guardrails at the beginning of no billing information should be accessed.<br>
	Data leakage: This could come in the form of presenting billing information. It does appear there is mitigation built in for data leakage.
<br><br><br>

audit trail evaluation<br>
	1. The Timeline appears to capture what each agent did during its run time. As long as I would be able to see a copy of exactly what was generated, a problematic agent devicion cuold be reconstructed and addressed.<br>
	2. For the human approval task the timeline indicates that approval was asked for and received however no prompt for human interaction was generated as it should have been. This shows that hallucination can and does happen during the overall process which reduces trust in the audit trail.<br>
	3. In a real organization the mobile support team would need access to this log daily as account are often checked each day to ensure nothing major has happened overnight. This would allow for the team to stay on top of potential issues and errors in the auditing process.<br>
	4. At the very most I would feel comfortable letting this crew go week to week. Typically a billing cycle is 1 month in total so the first few weeks could do with less interaction. The need for interaction would increase within the last week and a half as this is the critical window to ensure anything that was previously missed can still be actioned before the cycle closes.<br><br>


top 3 risks + top 3 mitigations<br>
	Risks: Billing information being included in outputs, agents missing mobile numbers that should be actioned, a change request being sent without review<br>
	Mitigations: Human review, tool access/email access guardrails preventing sending on its own, strict guardrails around reading permissions
<br><br><br><br>


Reflection Questions<br><br>

1. The main addition would be the Human Approval tool. This was something that was mentioned in the original input to have the platform generate the tools on the canvas however it did not initially get generated. This is a crucial step to ensure that the list of change requests generated is accurate before anything is sent to the carrier for processing. Reversing a change request sent in via email is a lengthy process and depending on how close the end of the billing cycle is may not be possible to do. It was also necessary to add a took for generating the change request email draft.<br>

2. If this were run in a live environment, the owner of an erroneous output would be owned by the mobile support team. For a response they would need to see the files outputted for review and the notes, if any, that were left by the agent who reviewed them before approving and sending the change requests off.


