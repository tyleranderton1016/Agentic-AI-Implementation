presentation: <br><br>

Activepieces and OpenRouter<br>
Activepieces is a no-code and low-code automation platform with over 740 integrations that lets you connect apps and build workflows to eliminate repetitive tasks. OpenRouter acts as a universal AI gateway, giving you access to 400+ language models through one API Key. <br>Together, they let you build AI-powered automations using Activepieces to orchestrate workflows and OpenRouter to switch between models like GPT, Claude or Gemini without changing your setup. In my case I was able to get access to gpt-4o-mini with free access to power my Ask LLM steps. This combination provides flexibility, cost optimization, and rapid deployment of AI agents and business processes.
<br><br><br>



Demo<br>
Currently manual trigger but the next step would be to fully automate the process by monitoring a 'To Be Processed' folder and moving completed files to prevent duplicate audits.<br>

Get worksheets step gets the selected usage report information from OneDrive<br>

First ask LLM step calls the agent and feeds in the usage report from the output generated in step 2. Agent then runs on the provided report<br>

After it has been run and determined what changes should be made, an email approval is sent out. Once approved the second Ask LLM step runs generating an email draft for review. Changes can be made here and the draft copied and used to send to the carrier for processing.<br>

<br><br>

Example outputs from successful tests: <br>
<img width="630" height="691" alt="image" src="https://github.com/user-attachments/assets/1a18913f-1c41-4d17-80d5-d6e6fc3a0029" />
<br><br>
<img width="621" height="702" alt="image" src="https://github.com/user-attachments/assets/722ba662-260a-4e18-b175-e96f3e7efcfe" />
<br><br>
<img width="613" height="709" alt="image" src="https://github.com/user-attachments/assets/a1628690-4f62-44b7-bbdf-35cf850e2ab0" />
<br><br>
<img width="617" height="711" alt="image" src="https://github.com/user-attachments/assets/7d26a9d5-dcb0-4967-a214-4547f41670ed" />


Email Success output: <br><br>
<img width="624" height="702" alt="image" src="https://github.com/user-attachments/assets/4e1253f4-7b5b-44b4-8765-4dac294ad70d" />
<br>
<img width="621" height="709" alt="image" src="https://github.com/user-attachments/assets/4b504d84-8741-4e5b-b788-d2023d855d33" />


<br><br><br>
Concepts<br><br>

Agent Card<br>
"I started by creating an Agent Card that defined the AI's role as a Mobile Support Advisor. I provided a decision framework, available recommendations, confidence levels, and hard constraints. <br>
I also required the agent to explain its rationale and assign confidence scores so recommendations could be reviewed by a human."
<br><br>

Evaluation: <br>
The agent was tested using three scenarios: a standard usage report containing a mix of roaming activity, overages, and suspended lines;<br>
a low-usage scenario with no roaming or overages and a healthy data pool;<br>
and an extreme-case file with multiple significant overages.<br>
The agent produced accurate and complete outputs for the first two scenarios, although the standard test revealed some false positives on unlimited plans. In the extreme-case test, it successfully identified excessive roaming usage and overall pool risk, but it did not consistently call out the specific lines responsible for high regular data usage, instead recommending that the pool be reviewed. Overall, the agent performed well in typical scenarios but needs improvement in handling edge cases and reducing false positives.

<br><br>
Deep Dive: Risk and Governance<br>
"The area I focused on most was risk and governance. Since incorrect carrier changes can be expensive and difficult to reverse, I intentionally limited the agent's permissions. It has no access to billing information, account PINs, or carrier portals, and it cannot execute changes itself. Instead, it only generates recommendations and draft emails. Every action requires a human approval step before anything is sent externally. Then there are the issues of hallucinations and model drift which can be mitigated through confidence scoring, periodic evaluation, and versioned prompts and workflows. These controls ensure the agent remains a decision-support tool rather than an autonomous system, reducing the risk of costly mistakes."

<br><br>
Business case- By automating the most time-consuming parts of mobile audits, this tool can reduce a process that often stretches across one to two days down to a fraction of the time. <br>
This allows advisors to focus on support calls and tickets, improving response times and customer satisfaction while generating an estimated $12,000+ in annual productivity savings per agent running audits."
<br><br><br>




Honest limits section <br>
One of the initial challenges was triggering the workflow. We solved this by manually injecting the carrier usage file, but the next step would be to fully automate the process by monitoring a 'To Be Processed' folder and moving completed files to prevent duplicate audits. While I trust the agent to analyze data and generate recommendations, I would still require human approval before anything is sent externally to avoid costly carrier errors. Looking ahead, I see opportunities to expand into processing simple requests like plan changes, suspensions, and disconnects, and eventually add a metrics dashboard to track accuracy, overrides, savings, and overages prevented to continuously improve performance.
