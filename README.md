# service-now-urgent-incident-notification-workflow

## System Overview

This workflow automates immediate email notifications for critical network incidents in a ServiceNow instance. Designed to prevent SLA breaches, the system monitors incidents classified under the “Network” category with a "Critical" priority and sends real-time alerts to the Network Operations team. This ensures engineers are notified immediately when high-priority issues occur, reducing downtime and improving service reliability.

## Implementation Steps

1. **Investigated the Issue**  
   Found that the original "Kura WL1" workflow had conditions that triggered only if the Urgency was set to "Medium" and the Assignment Group was not empty. Because of this, the workflow failed to send email notifications when critical incidents were created.

2. **Remediated the Flow**  
   Edited the existing Flow Designer workflow (`Kura WL1`) and renamed it to `Critical Network Notification`.

3. **Defined Trigger Conditions**  
   - **Table**: Incident  
   - **Trigger**: When a record is inserted  
   - **Conditions**:  
     - Category = Network  
     - Priority = 1 - Critical

4. **Added Email Notification Action**  
   Used the “Send Email” action to send notifications to the "Network Operations" group. Configured the email to include the incident number, short description, and a direct link to the incident.

5. **Tested the Workflow**  
   Created multiple test incidents to ensure notifications were sent. Verified delivery through the `sys_email` table, specifically under the Outbox tab.


Architecture Diagram:<img width="1240" height="344" alt="Diagram drawio" src="https://github.com/user-attachments/assets/7efc9fdd-8211-4264-be19-da06654f8053" />

## AI Scenario: Intelligent Escalation with AI Agents

As someone starting to explore AI agent use cases, I can already see how AI could improve this workflow long term. One idea is to build an AI agent that helps route critical incidents based on who’s actually available, what time zone they’re in, and which engineers have handled similar issues before.

- **Match by skills and past performance**: The agent could learn who’s solved similar network issues successfully and route alerts to them first.  
- **Factor in time zones and workload**: Instead of just following a set escalation path, it would check who’s on and not overloaded.  
- **Improve over time**: By analyzing past incidents, the agent could recommend better routing logic and suggest updates to response strategies.

This kind of AI integration would make the response process faster, smarter, and more flexible, helping avoid delays like the one Uber experienced during the San Francisco outage.
