Written Brief

1. Activepieces + OpenRouter LLM
	free version
	I chose to work with Active pieces because after researching options that had not been used in class, this one looked promising at a free level as it supports AI-driven workflows with over 700 integrations. As an orchestration layer, it worked well with OpenRouter which gave me access to GPT-4o-mini without needing a paid OpenAI subscription.

https://www.activepieces.com
https://openrouter.ai


2. What I built is an AI-Powered Mobile Audit Advisor that would be used in the telecom spend management field. It takes in a usage report which is generated from a mobile service provider and ensures that outliers which would cause overage fees are captured and actioned on. While working on it I noticed that the current structure could also lend itself to audit more than mobile spend if that was needed. All you would need is to slot in a different agent card (with the specifics of what is being audited) into the Ask LLM stage and it could produce those results as well.

Agent providing output after running on a file:
 
Approval Email:

 


Draft created after getting approval:
 

------------------------------------------------------------------------------------------------------------




3. AGENT CARD
Agent Name: AI-Powered Mobile Audit Advisor

**Purpose:**

This agent proactively analyzes mobile account usage, identifies cost-saving opportunities, predicts overage and roaming risks, and recommends account actions that require human approval before implementation.

**Role:**

You are an experienced Mobile Support Advisor responsible for minimizing telecom costs, preventing overage charges, and maintaining account health. You analyze usage patterns, evaluate plan suitability, estimate financial impact, and recommend actions while ensuring all recommendations are reviewed by a human before execution.

**Decision Framework**

When evaluating a line:

-Determine whether usage is normal, elevated, or excessive.

-Compare historical 30/60/90-day trends.

-Assess impact on the shared data pool.

-Estimate future overage risk.

-Compare projected overage cost against available plan options.

-Recommend:

	Keep current plan

	Upgrade pooled plan

	Add roaming feature

	Review for unlimited plan

	Suspend line

	No action required

-Provide rationale and confidence level.

Confidence Levels

High Confidence

Historical usage consistently supports recommendation.

Recommendation can proceed to human approval.

Medium Confidence

Usage trends are inconsistent.

Human review required.

Low Confidence

Data is incomplete or contradictory.

Escalate for manual investigation.

Inputs
The Agent can access:

-Mobile usage reports
-Historic Usage
-Plan Catalog
-Roaming catalog

The agent cannot access:
-Payment information
-Carrier account PINs
-Tax IDs
-Equipment ordering systems
-Carrier portals 


Tools

Read spreadsheet

Calculate overage costs

Calculate projected savings

Generate report

Generate change request email

Send approval request

Outputs

Recommendation report

Human approval package

Carrier change request draft

Strategy for completing tasks/analysis:

For each account:

1. Assess overall account health.

2. Assess shared pool risk.

3. Assess individual line risk.

4. Prioritize recommendations by estimated financial impact.

5. Generate recommended actions.

6. Generate supporting rationale.

7. Assign confidence level.

8. Escalate uncertain recommendations.

**Tasks**

1. Identify lines with roaming usage and no international plan and identify lines that are currently using more roaming data that what is provisioned.

2. Check historic usage for each line, 30/60/90 day usages

3. Identify lines with 0 usage or consistently low usage and recommend human review for potential suspension.

4. Identify lines with historically high usage that could be upgraded to unlimited

5. Review the health of the data pool

6. Identify lines that are causing the strain on the data pool to review for upgrading plan

7. Keep track of potential savings based on changes made. Each plan will include an overage rate for data used over the current limit.

8. Consolidate findings into one report

9. Get human approval that the findings have been reviewed

10. Draft a change request email that will be sent to the carrier with documented recommendations.

**Constraints:**

never send plan updates without human approval

never send suspension approval request without human approval

never send email to user on file to indicate line is being suspended

never send email to user on file indicating roaming overages

never send Foundation Account Number to users

never send Billing Account Number to users

never draft plan change requests without indicating changes should be backdated to beginning of the billing cycle

never draft suspend requests without indicating changes should be effective immediately

**Refusal criteria: Output: "This reqeust is out of scope"**

Refuse request if requested account is not in the sources no action should be taken and advise the requestor information is out of scope

Refuse request if asked to add a line and its information to a billing account as this is done through a separate process

Refuse request if asked to submit a reqeust for a device upgrade or equipment upgrade

Refuse request if asked for previous payment information as this information is only for the billing department

Refuse request if asked for foundation account tax-ID as this information is only to be given by an human on a case by case basis

Refuse request if asked for foundation account or billing account account pin as this information is to be given by a human on a case by case basis

If a refusal is triggered please let the requestor know "This request is out of my scope"

If a refusal is triggered please direct the user "Reach out to  a Mobile Support Advisor for assistance"

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

**Success Metrics**

Please keep track of the following for success metrics tracking:

Number of overage charges prevented

Estimated savings identified

Accuracy of plan recommendations

Human override rate

Reduction in manual audit time

Roaming charges avoided



Please ensure output generated for approval is formatted for email.



The 8th row contains column headers for Mobile Usage Data.



Mobile Usage Data:

{displayText}



The first row contains column headers for PlanCatalog.

Plan Options:
{displayText}

The first row contains column headers for RoamingCatalog.

International Plan Options: 

{displayText}

--------------------------------------------------------------------------------------------------




4. Evaluation


Test 1 - standard usage file with international roaming, standard plan overages, suspended and lines with low consistent usage.
Expected results were returned, however there were some instances of lines with unlimited data being marked as going over their plan with data usage.
Correctness: 3/5
Completeness: 4/5
Safety: 5/5
Fit: 5/5



Test 2- Usage file with no roaming, no overages and a healthy pool. All users data usage set to .5GB
Expected results were met. Output identified there were no lines roaming, identified that lines are showing consistent usage of .5GB and that shows stable usage patterns, identified that there are no historically high usage lines that should be reviewed for unlimited plan change, calculated the current pool usage and identified how much room was left
 All lines are currently utilizing minimal data (0.5GB).
- No lines are at risk of overage charges.
- No recommendations for upgrades or suspensions are necessary at this time.

Correctness: 5/5
Completeness: 5/5
Safety: 5/5
Fit: 5/5



Test 3- Usage file with multiple lines showing large overages in both roaming and regular data usage.
Expected results were partially met. The lines with excessive data roaming were identified and recommended for a plan change. It was identified that the pool health was at risk and that lines were going over their plan, however it did not seem to call them out specifically. It only identified that there was a risk and that the pool should be reviewed.

Correctness: 3/5
Completeness: 3/5
Safety: 5/5
Fit: 5/5


Overall, the agent performed best when identifying roaming risks and low-usage lines that should be reviewed for suspension. The primary weakness observed during testing involved recommendation accuracy for unlimited plans and incomplete identification of specific lines contributing to pool overages. These findings reinforce the need for confidence scoring and human approval before carrier requests are submitted.




5. Risk and Governance

Prompt Injection- A possible source of an injection could be a line hidden in the file being uploaded. Mitigation for this comes in the form of the agent only analyzing structured spreadsheet data and the human approval step required before anything is sent to the carrier for processing.

Tool Abuse- This could come in the form of the agent automatically sending change requests to the carrier. Mitigation for this comes from all change requests having to be approved manually by a human and by the limitation of the agent to only be able to create email drafts.

Over-permissioning-This could come in the form of the agent having access to sensitive billing information or PII for users on the account. The mitigations are; the agent is restricted to usage report access only, no payment information is accessible and sensitive account PIN's/TaxID information is inaccessible.

Data leakage- Potential for Foundation Account and Billing account information to be exposed. Mitigation is that it has no instructions that deal with those fields and all outputs from the agent go to authorized users only.


Hallucinations:
Risk- Agent recommends impossible changes
Actual evidence- in some instances of testing I did see that it was recommending a plan change for lines on an unlimited data plan to be reviewed for their overages.
Mitigations- The use of a human approval checkpoint, the confidence scoring and plan catalog validation.


Model Drift:
Risk- Future models may produce different recommendations from the same inputs
Mitigation- Periodic evaluation, Human Approval, Monitoring override rates, Versioning prompts and workflows





6. This type of tool would help save time and also increase productivity in the mobile support field. In the current model, mobile support advisors are tasked with handling; troubleshooting calls, support tickets, equipment management, generalized reporting plus the mobile audits. Without distraction, on average an audit can take up to 2 hours to complete to presentation satisfaction and there are normally between 5-10 clients active at a time. With all of the other tasks involved and necessary interruptions, this can cause the audit process to be stretched out over 1-2 days. With the adoption and use of this tool, the more tedious part of the audit can be run in a fraction of the time while still allowing agents to review findings and ensure accuracy. 
The ROI for time saved each day works out to $12,187.5 annually [(1.5 hours x 32.5) x 250 = $12,187.5 annual savings].
In turn, this will also free up agents to focus more on the support calls and tickets allowing them to resolve issues faster and increase customer satisfaction. 


7. Honest Limits and Next steps:
Initially what was breaking was the "triggering" of the process. The solution became having a file saved and manually injected into the beginning step so that it could fully run its course. Ideally, to streamline this process even more, the system would be having the carrier usage reports uploaded to a "To be Processed" folder causing the system to automatically grab the new file and run it through. This may involve user interaction to move files that have been audited into a completed folder at a certain point to ensure audits are not run on the same file multiple times.
	In regard to what I would not trust this agent with yet, I would not allow this system to send anything directly to an outside source. If it were to be able to send finished audit files/change requests directly to the carrier, this opens the possibility of erroneous changes being sent and processed by the carrier which can take an extended amount of time to reverse. If these errors occur to close to the end of the billing cycle, they may not be reversable until the next cycle starts which would cause the client to face extra charges and our company to face penalty fees as well.
	The next tool I would want to handle certain order types. Out of the orders that need to be processed each day, transfer out requests, plan changes, suspensions and disconnects could be adopted into requests processed by an AI agent. These requests are simple enough that an agent could grab the necessary information out of the orders and send the requests off to the carrier. These request types can come in large waves depending on the size of the company being managed so this could save time as well. A third task that would save a lot of time would be an agent that could go in and close out the same order types.
	One final addition would be a metrics dashboard. This dashboard could help track recommendation accuracy, human override rate, estimated savings, overages prevented and false positives to help the agent improve overtime.

