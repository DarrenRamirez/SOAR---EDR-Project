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
- Create a Slack Channel to receive alerts from LimaCharlie through Tines

  <img src="https://imgur.com/qIZ88tn.png" alt="Imgur Image" />
  
*Ref 4: Slack channel creation*
- Add an Action in Tines to send Slack messages whenever an alert is received from LimaCharlie.

<img src="https://imgur.com/5MPZcb2.png" alt="Imgur Image" />

*Ref 5: Tines webhook from slack*
- Using LimaCharlie, we can gather information such as:
  * Time 
  * Computer name 
  * Source IP
  * Process
  * Command line
  * File Path
  * Sensor ID
  * Link to detection
  * Username
- By passing this information through Tines, we can include these details in our Slack and email alerts.
  
- Incorporate Email Notifications

### 5. In Tines, add an Email Action to send alert details (host name, IP, suspicious activity) to a designated distribution list.

<img src="https://imgur.com/c1kZxX8.png" alt="Imgur Image" />

*Ref 6: Tines to email Creation*

- We use similar parameters to create emails with the same information as our Slack alerts.

- Build the Decision Workflow (Human-in-the-Loop)

### 6. In Tines, after sending an alert to Slack, prompt the user with a question: “Isolate endpoint?”
- Listen for “Yes” or “No” responses in Slack.

<img src="https://imgur.com/RTzLJL4.png" alt="Imgur Image" />

*Ref 7: User Prompt triggered on alerts*

### 7. Endpoint Isolation via LimaCharlie
- If Yes is received, Tines triggers an Action to call LimaCharlie’s API and isolate the Vultr device. Tines will also send another request to LimaCharlie for that status on the isolation after the user prompt was answered.

<img src="https://imgur.com/6QaX6tB.png" alt="Imgur Image" />

*Ref 8:Yes, Result alert in slack*

- If No, the workflow notifies the user to investigate further.

<img src="https://imgur.com/DlRweEC.png" alt="Imgur Image" />

*Ref 9: No, Result alert in slack*
- Audit & Logging
## Conclusion 

This project demonstrated the power of integrating security tools to automate threat detection and response. By deploying LimaCharlie on a Vultr server, orchestrating workflows through Tines, and delivering alerts via Slack and email, I created an efficient and scalable incident response pipeline. This experience not only deepened my understanding of EDR solutions and SOAR automation but also enhanced my skills in security tool integration, workflow design, and real-time alerting. The project highlights the value of automation in cybersecurity and reinforces my ability to design, implement, and document effective security solutions.


