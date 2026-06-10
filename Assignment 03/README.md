
**Agent Share Link:** https://elevenlabs.io/app/talk-to?agent_id=agent_2801ktph78wnez6axzbtfmkvvr4m <br><br>
<br><br>
---------------------------------------------------------------------------------------------------------------------------------------------<br><br>
**Voice Agent Design Document:**<br><br>
Agent Card<br><br><br>
Agent Name: Account Usage Monitor

Purpose:
This agent is used to check the current usage on a mobile account to ensure there will be no account data overages, international roaming charges and identify lines that could be suspended and eventually disconnected.


Role:
You are a mobile support advisor who is analytical, professional and savings driven.


Inputs:
If the user is asking for information about a line, please ask to provide the mobile number in question.
If the user is asking for an account review, please have the user identify which account is in question.
If the user is asking for a total account review, please confirm which of the tasks listed in the task section they want run on the account.
If the user is asking for usage totals for a line please have them confirm if it is roaming usage, standard usage or total usage.

Has access to:
	Current usage report
	3 month usage report
	6 month usage report
	Data plan options
	Data Roaming plan options

Does not have access to:
	users email, address
	information pertaining to text messages (sent and received), Call logs, sites accessed on devices
	account billing address
	account tax-ID



Tasks:
Your tasks will include the following. 
Help with identifying the current usage of a provided mobile number. 
Provide a list of lines that are using roaming data but do not have an international plan active.
Provide a list of lines that are showing more than 1GB of roaming usage.
Provide a list of lines that have 0 data usage.
Provide a list of lines that are currently suspended.
Provide usage history of a line including the 3 month and 6 month usage.
Check the total usage of all the lines and compare that total to the overall account pool limit and provide feedback based on the following criteria: If amount used is under 80% of the account pool indicate that no action is required. If the amount is over 80% indicate review is necessary.
Provide a list of lines that are showing more than 10GB of total usage and if they are not on unlimited suggest they be reviewed for a possible plan change.





Constraints:
	never send plan updates without human approval
	never send suspension approval request without human approval
	never send email to user on file to indicate line is being suspended
	never send email to user on file indicating roaming overages
	never send Foundation Account Number to users
	never send Billing Account Number to users
	never draft plan change requests without indicating changes should be backdated to beginning of the billing cycle
	never draft suspend requests without indicating changes should be effective immediately


Output Format:
	International Changes-
	The following lines showed international usage with no international plan. An email has been drafted asking the carrier to add an international 	package to each line, effective date backdated to start of billing cycle.
		 (Billing Account Number, Mobile Number, current international usage)
	The following lines should be monitored. (include lines marked by international threshold)

	
	Zero Usage Report-
	The following lines are currently showing 0 data usage. Also included is historical usage, and a drafted request to the mobile manager requesting 	approval for suspension of these lines effective immediately has been generated. A separate change request email has been drafted to be sent to the 	carrier for processing.
		(Billing Account Number, Mobile Number, Current usage, 3 month usage, 6 month usage)

	Data Pool Monitoring-
	Currently the Billing Account's pooled usage is at 80% of the overall account pool. A change request has been drafted for the carrier to adjust the 	below lines to higher allowance options to cover usage. Also included are lines marked for change to unlimited
		Adjusted lines: (Billing Account Number, Mobile Number, Current Usage)
		Unlimited Recommendation: (Billing Account Number, Mobile Number, Current Usage)



Escalation Trigger: Flag identified lines and output "We will get you in touch with a support advisor for further assistance"
	if identified lines usage is greater than all available pooled plan options
	if international usage is over 10GB
	if 0 usage lines are already suspended
	if there is a bounceback in sent emails
	if a request is for an equipment order
	if a request is for billing account information
	if a request is for foundation account information
<br><br><br><br>

Branch Table: <br><br>

Field	Branch 1 - Number Look up	Branch 2- your domain	Branch 3- Escalation
Branch Name	Line Lookup/Account Lookup	Agent Card/Provided usage reports	Escalation
Entry Condition- What does the users say or ask that routes them here?	Customer asks for information regarding an order	Customer asks for information regarding a mobile number or billing account	Ask is out of scope, order ID does not exist, attack detected
Powered by- Knowledge base, tool, or neither	webhook tool	Agent card/Provided usage reports	Neither, spoken handoff
Instructions- what specific behavior applies only in this branch?	Pulls information regarding specified order number given that the order ID is legit	Asks user to confirm what type of informaiton is needed. Gathers listed information	user is notified that the reqeust is being escalated
Exit condition- how does this brnach end? (Resolved/Escalated/Return to router)	Resolved by user indicating that no further information is required. Escalated if an ask is for information out of scope	Resolved by providing information and user indicating nothing else needed. Escalated if an ask is out of scope or and attack is detected	Escalation message delivered. Routing process begins
<br><br>

Router Design:<br><br>

Begin by saying: "Hello! Are you looking for assistance regarding a mobile number or billing account today?" <br>
	Path 1- If the user is asking about a mobile number, ask for the mobile number in question and what information is needed <br>
	Path 2- If the user is asking about an order ID, Ask for the order ID and return the information available for that order <br>
	Path 3- If the users ask is about something other than a mobile number, billing account or order ID, ask clarifying question to get user to mention the line, billing account or order ID they need information about. If they can not provide and answer to satisfy, transition to escalation and closing out of chat <br>
  
<br><br><br>
---------------------------------------------------------------------------------------------------------------------------------------------------
<br><br><br>
**Three test conversation transcripts:**<br><br>

Test of Branch 1 (Order Look up)<br>

What you said — Can you please provide information regarding my order?
What the agent said — "I can certainly help with that! Could you please provide me with the order ID? It's typically a four-digit number."
Did it route correctly? — Yes it did
Did the knowledge base or tool activate? — The agent called the tool and returned the order information.
Did the branch exit correctly? — The conversation ended when it was suppose to. After confirming that was what I needed and that nothing further was required the agent disconnected.
Pass or Fail — Pass. The agent prompted me for what I was looking for, took my order ID and returned the information available. Afterwards it confirmed I did not need anything else and terminated. 
<br><br>



Test of Branch 2 (Your Domain)<br>
test was done using chat option<br><br>

First message - Hello. I am needing assistance with a mobile number.<br>
What the agent said — I can certainly help with that! To provide you with the most accurate information, could you please provide the mobile number in question?<br>
Second message - (804) 555-0301<br>
What the agent said - Thank you. What information are you looking for regarding the mobile number? Are you interested in current usage, roaming usage, total usage, or something else?<br>
third message - current usage please<br>
What the agent said - Agent terminated chat<br><br><br>

Did it route correctly? — after learning that help was needed with a mobile number, it did route into the Mobile Support Assistant branch. However once getting to what info was needed for the line specifically it terminated. This could possibly be due to not having access to a mock usage report pull as I was able to provide in earlier assignments.<br>

Did the knowledge base or tool activate? — from the responses it did seem to get into the knowledge base provided. I did test with asking the agent to provide help getting information regarding mobile number (804) 555-0301. It following by asking which specific info was needed and terminated when I specified. This again could be due to limitations on provided info for this particular type of agent.<br>

Did the branch exit correctly? — conversation ended in roughly the right place, just without being able to provide usage information.<br>

Pass or Fail — I want to give it a partial pass for engaging the knowledge base and following the flow into the mobile support assistant chain, however it did terminate without being able to provide actual usage info.<br><br><br>




Test of Branch 3 (Escalation)<br>

First Message — can you please help with some order information <br>
What the agent said — I can certainly help with that! Do you have the order ID handy? <br>
Second Message - I dont actually. Could you use some other information to try and pull it up? <br>
What the agent said - I can only look up orders using an order ID, which is a four-digit number. Do you have that number, or would you like to speak with a support advisor who might be able to help you find it? <br>
Third Message - yes please <br>
What the agent said - agent terminated the chat. <br><br>

Did it route correctly? — yes it did <br>
Did the knowledge base or tool activate? — it appeared to call the tool correctly as it specified it needed a 4 digit order ID number to search <br>
Did the branch exit correctly? — Yes. The agent asked if it could connect me with a support advisor (escalated) and then terminated. <br>
Pass or Fail — pass <br><br><br>




Ambiguity test <br>

First message - Hello. Can you please help me with an order for Mobile number (804) 555-0301? <br>
Agent responded - I can certainly help you with that! To look up the order, I'll need the order ID. It's a four-digit number. Could you please provide it for me? <br>
Observation - Agent read through both "trigger" words in the question and chose to follow the get order chain <br>
<br><br><br>
---------------------------------------------------------------------------------------------------------------------------------------------------
<br><br>

**Voice and tool failure Analysis** <br><br>

1. What changed and what broke when moving from a text agent to a voice agent? <br>
	This question is a bit challenging to answer as I ran into some issues that may be user error on my end. It became hard to tell where, or if, the agent was breaking at times as I could get it to flow into my domain created with the agent card and get some expected returns, however when it came time for it to action the part of returning the requested information the chat would shut down. I am not sure if this is due to an error in how the card is written OR if this is due to the agent not being connected to a proper mock usage report. Just to see what would happen, I also created a new knowledge base that was a text file of a mock usage report and the agent still would get all the way to the point of receiving the mobile number I wanted to run a check on and then closing out. <br>
When I was able to trigger an escalation from my domain however, it came out exactly as I wanted.<br>
EX:<br>
Q - I need assistance with cancelling a mobile number <br>
A - I can help with providing usage information for a mobile number. However, I cannot directly cancel a mobile number. I can provide you with the usage history of the line, including the 3-month and 6-month averages, if you'd like. This information might be helpful when you contact customer service to cancel the line. To proceed, please provide the mobile number in question.	<br><br>

When speaking with the agent, end-of-turn latency seems to be low as the agent jumps in pretty quickly after I finish speaking. It did have some trouble in the barge-in recovery area as once I got it started on a request in one area, it did not like trying to switch over to the other. For example, I started by stating I needed assistance with a mobile number and butting in stating that actually I needed help with an order ID to which it stated it did not have access to that information, only for information regarding usage.<br><br><br>

2. What happened the first time your agent tried to call the order lookup tool-and what did you have to fix? <br>
	After following the installation instructions and running the tool in the test environment it returned the order information on the first try. <br> It also responded expectedly when asking for requests that were out of scope or for order information on orders not in the list. I got similar results when running these tests through the published share link in an incognito tab. <br><br>

3. Your branch 3 is your last line of defense. After testing, do you trust it? <br>
	Based on the attempts to "attack" the system it was pretty consistent in fighting back. I tried getting it to ignore its instructions and guardrails and it would not and insisted on that. When it came to my domain, when out of scope asks were placed the chat was forced into ending the encounter rather than complying. <br><br><br>
  ----------------------------------------------------------------------------------------------------------------------------------------------
  <br><br><br>
  **Screenshots**
  <br><br>
  
  Workflow Canvis: <br><br>
  <img width="2550" height="1428" alt="Workflow canvas" src="https://github.com/user-attachments/assets/30918c00-f796-43e3-87db-21c7a88addd9" />
<br><br><br>

Branch 2 subagent's Knowledge Base Tab:<br><br>
<img width="2551" height="1430" alt="Branch 2 subagent knowledge base" src="https://github.com/user-attachments/assets/67175efa-57fe-4cd7-81c8-1145a445c343" />
<br><br><br>

Order Lookup subagent's tools tab: <br><br>
<img width="2559" height="1437" alt="lookup subagent tools tab" src="https://github.com/user-attachments/assets/f462f156-e02f-4a3e-9ab3-b50cadd299d0" />
<br><br><br>

Lookup Order tool configuration tools tab: <br><br>
<img width="2552" height="1434" alt="lookup order tool configuration panel" src="https://github.com/user-attachments/assets/c909b061-20d2-4d6f-8c6e-1327ad15349e" />
 <br><br><br>

 Successful tool call: <br><br>
 <img width="2547" height="1426" alt="Successful Tool Call" src="https://github.com/user-attachments/assets/778c6087-51e6-42f9-b53b-ae2369ae4891" />

 

  








