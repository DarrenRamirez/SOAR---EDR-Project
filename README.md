# SOAR-EDR-Project

## Objective
The SOAR EDR project aimed to build an automated environment for detecting and responding to security threats. The primary focus was to ingest real-time alerts from LimaCharlie and orchestrate the response within Tines, including user prompts for endpoint isolation. This hands-on approach was designed to streamline threat detection, reduce response times, and integrate communication channels (Slack and email), ultimately enhancing the overall security posture through a repeatable and auditable process.

### Skills Learned
- Automation & Orchestration – Designing workflows in Tines to automate alert handling and endpoint isolation
- Endpoint Detection & Response (EDR) – Leveraging LimaCharlie to detect suspicious activity and execute isolation commands
- Incident Response – Coordinating rapid decision-making and manual approvals for containment within a structured playbook
- Security Tool Integration – Establishing seamless communication among Slack, email, and EDR solutions
- Process Documentation & Auditing – Logging activities and decisions for compliance, auditing, and iterative improvements

### Tools Used

- LimaCharlie – Endpoint Detection & Response (EDR) platform for detecting and isolating threats.
- Tines – SOAR platform for automating incident-response workflows and orchestrating security actions.
- Slack – Real-time communication channel for sending alerts and receiving user decisions.
- Vultr – Hosting provider for deploying and managing servers used in the lab/testing environment.

## Steps
drag & drop screenshots here or use imgur and reference them using imgsrc

Every screenshot should have some text explaining what the screenshot is about.

Example below.

*Ref 1: Network Diagram*

Provision a Device on Vultr

### 1. Log in to Vultr and create a new server (e.g., Ubuntu or Windows).
- Once the server is running, note its IP address and hostname. In this case I will be using a windows server and keeping the default hostname. 

<img src="https://imgur.com/X1wTg64.png" alt="Imgur Image" />

*Ref 1: Vultr Dashboard*
- Install the LimaCharlie Agent (EDR) on the Vultr Device.

### 2. Follow LimaCharlie’s documentation to install the EDR agent on your new server.
- Verify the device shows up in your LimaCharlie console as “online.” As you can see in the image below its show the hostname and that the server is in fact online

<img src="https://imgur.com/vCUfvJW.png" alt="Imgur Image" />

*Ref 2: LimaCharlie Dashboard*
- Set Up Tines to Ingest Alerts from LimaCharlie

### 3. In Tines, create a Story dedicated to processing LimaCharlie alerts.
- Configure a Webhook Action or a HTTP Request Action that listens for events from LimaCharlie. 

<img src="https://imgur.com/mQdjobw.png" alt="Imgur Image" />

*Ref 3: Tines Dashboard*
- Enable Slack Integration in Tines

### 4. Create a Slack webhook.
Add an Action in Tines to send Slack messages whenever an alert is received from LimaCharlie.

Incorporate Email Notifications

5. In Tines, add an Email Action to send alert details (host name, IP, suspicious activity) to a designated distribution list.
(Screenshot Opportunity: Tines Email Action configuration, showing recipients and subject line.)
Build the Decision Workflow (Human-in-the-Loop)

6. In Tines, after sending an alert to Slack, prompt the user with a question: “Isolate endpoint?”
Listen for “Yes” or “No” responses in Slack.
(Screenshot Opportunity: Slack channel showing the automated prompt with “Yes” or “No” response options.)
Endpoint Isolation via LimaCharlie

7. If Yes is received, Tines triggers an Action to call LimaCharlie’s API and isolate the Vultr device.
If No, the workflow notifies the user to investigate further.
(Screenshot Opportunity: Confirmation message in Slack showing the endpoint was isolated, plus the LimaCharlie console reflecting isolation status.)
Audit & Logging

8. Ensure Tines logs every step (alert details, Slack message, user’s decision, isolation call) for future reference.
(Screenshot Opportunity: Tines Story log showing timestamps for each action.)
Document in Your GitHub Repository

In your README.md, outline each step in brief text.
Include screenshots for each key milestone (Vultr instance creation, LimaCharlie agent install, Tines workflow, Slack messages).
Add any Shields.io badges for the tools used (Vultr, LimaCharlie, Tines, Slack, etc.).

