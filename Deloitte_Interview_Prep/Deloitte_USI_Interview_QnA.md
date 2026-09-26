# Deloitte – Cyber Operate: SOAR + Anthropic – Consultant

## Expected Interview Questions & Answers

---

# 1. SOAR Fundamentals

## Q1. What is SOAR?

**Answer:**

SOAR stands for **Security Orchestration, Automation and Response**. It integrates different security tools and automates repetitive SOC activities such as alert enrichment, investigation, ticket creation, containment and remediation.

For example, when a phishing alert is generated, SOAR can automatically extract the URL, check it against threat-intelligence sources, investigate the sender and domain, create a ServiceNow ticket, and quarantine the email if the required conditions are satisfied.

---

## Q2. What is the difference between SIEM and SOAR?

| SIEM                                 | SOAR                                      |
| ------------------------------------ | ----------------------------------------- |
| Collects and analyzes security logs  | Automates response and orchestration      |
| Detects suspicious activity          | Responds to detected incidents            |
| Correlates events                    | Executes playbooks                        |
| Generates alerts                     | Enriches, investigates and remediates     |
| Uses detection rules                 | Uses workflows/playbooks                  |
| Example: Splunk, Sentinel, Chronicle | Example: Cortex XSOAR, Splunk SOAR, Tines |

**Interview answer:**

> SIEM is mainly responsible for collecting, correlating and detecting security events, while SOAR takes those alerts and automates investigation and response using playbooks and integrations.

---

# 2. SOAR Playbooks

## Q3. What is a SOAR playbook?

**Answer:**

A SOAR playbook is an automated workflow that defines the steps to be performed when a security alert or incident occurs.

A typical playbook can:

1. Receive an alert from SIEM.
2. Extract indicators such as IP, domain, hash or URL.
3. Enrich them using threat-intelligence platforms.
4. Investigate the endpoint or user.
5. Calculate risk/severity.
6. Create or update a ticket.
7. Perform containment if required.
8. Notify the SOC analyst.
9. Record the complete activity for auditing.

---

## Q4. What are the common types of SOAR playbooks?

**Answer:**

Common playbooks include:

* Phishing investigation
* Malware investigation
* Suspicious IP investigation
* Malicious URL investigation
* Brute-force detection
* Account compromise
* Endpoint isolation
* Threat-intelligence enrichment
* Vulnerability enrichment
* Data-exfiltration investigation
* Cloud security incident response
* Firewall blocking
* User account disablement
* Incident/ticket management

---

## Q5. How would you design a phishing-response playbook?

**Answer:**

I would design it approximately like this:

```text
Phishing Alert
      ↓
Extract sender / URL / domain / attachment hash
      ↓
Threat Intelligence Enrichment
      ↓
Check reputation
      ↓
Investigate sender and recipient
      ↓
Determine Risk
      ↓
Create/Update Incident
      ↓
If malicious → Quarantine/Delete Email
      ↓
Block IOC if required
      ↓
Notify SOC
      ↓
Close/Update Ticket
```

I would also include error handling, retries, logging and human approval before destructive actions.

---

# 3. Detection and Response

## Q6. What is detection and response?

**Answer:**

Detection is the process of identifying suspicious or malicious activity from security telemetry. Response is the set of actions taken after detection to investigate, contain, eradicate and recover from the incident.

A simplified lifecycle is:

```text
Collect → Detect → Triage → Investigate → Contain → Eradicate → Recover → Lessons Learned
```

---

## Q7. What do you do when a detection/response alert is generated?

**Answer:**

> First, I validate and triage the alert to determine whether it is a true positive or false positive. Then I enrich the alert using threat intelligence, endpoint, identity and other available data sources. If it is malicious, I investigate the scope and impact, perform appropriate containment/remediation through SOAR, update the case/ticket and document the complete response.

---

## Q8. What is alert triage?

**Answer:**

Alert triage is the initial process of determining:

* What happened?
* Is the alert legitimate?
* How severe is it?
* Which user/device is affected?
* Is there any malicious indicator?
* Is the activity isolated or part of a larger attack?
* What action should be taken?

The objective is to quickly prioritize true positives and reduce unnecessary analyst effort.

---

# 4. SOAR Integrations

## Q9. How do you integrate SOAR with another security product?

**Answer:**

I generally use the product's **REST API, webhook or native connector**.

The integration flow is:

```text
SOAR
 ↓
Authentication
 ↓
API Request
 ↓
Third-party Security Product
 ↓
Response
 ↓
Parse JSON
 ↓
Normalize Data
 ↓
Use Data in Playbook
```

I validate authentication, API permissions, request/response formats, rate limits, error handling and timeout/retry behavior.

---

## Q10. What is a REST API?

**Answer:**

REST is an architectural style used for communication between applications over HTTP.

Common methods are:

* `GET` – retrieve data
* `POST` – create/send data
* `PUT` – replace/update data
* `PATCH` – partially update data
* `DELETE` – delete data

For example:

```http
GET /api/incidents/123
```

can retrieve incident information.

---

## Q11. How do you authenticate API integrations?

**Answer:**

Common methods include:

* API keys
* Bearer tokens
* OAuth 2.0
* Basic authentication
* JWT
* Client certificates

For security integrations, I prefer storing secrets in the SOAR platform's secure credential store rather than hardcoding them in scripts.

---

## Q12. What is a webhook?

**Answer:**

A webhook is an HTTP callback mechanism where one application sends an HTTP request to another application when an event occurs.

For example:

```text
EDR detects malware
       ↓
Webhook
       ↓
SOAR
       ↓
Playbook starts
```

This enables near real-time event-driven automation.

---

# 5. API Troubleshooting

## Q13. An API integration suddenly stops working. How would you troubleshoot it?

**Answer:**

I would check systematically:

1. Authentication/token validity.
2. API endpoint and HTTP method.
3. Request headers and payload.
4. API permissions.
5. HTTP status code.
6. Response body.
7. Network connectivity.
8. TLS/certificate issues.
9. Rate limiting.
10. Vendor/API changes.

For example:

```text
401 → Authentication issue
403 → Permission issue
404 → Endpoint/resource issue
429 → Rate limiting
500 → Server-side issue
502/503 → Gateway/service availability
```

I would reproduce the request using Postman/curl where appropriate and then fix the integration or connector.

---

# 6. Error Handling

## Q14. How do you handle failures in SOAR playbooks?

**Answer:**

I use:

* Try/catch or equivalent error handling
* Timeout handling
* Retry mechanisms
* Conditional branches
* Default/fallback paths
* Logging
* Error notifications
* Manual escalation

For example:

```text
Threat Intelligence API
        ↓
     Success?
     /      \
   Yes       No
   ↓          ↓
Continue    Retry
             ↓
          Still fail?
          /       \
        Yes        No
        ↓          ↓
     Manual     Continue
    Escalation
```

---

# 7. SIEM + SOAR Architecture

## Q15. Explain a typical SIEM-SOAR architecture.

**Answer:**

```text
Log Sources
    ↓
SIEM
    ↓
Detection Rules
    ↓
Security Alert
    ↓
SOAR
    ↓
Playbook
    ↓
Enrichment
    ↓
Investigation
    ↓
Response
    ↓
ITSM / SOC
```

For example:

```text
Microsoft Sentinel
        ↓
Suspicious Login Alert
        ↓
Cortex XSOAR
        ↓
Check IP Reputation
        ↓
Check User Risk
        ↓
Check Azure AD/Entra
        ↓
Disable Account / Revoke Session
        ↓
ServiceNow Ticket
```

---

# 8. Case Management

## Q16. What is case management in SOC?

**Answer:**

Case management is the process of tracking a security incident from creation to closure.

A case usually contains:

* Alert details
* Severity
* Affected users/assets
* Indicators
* Investigation evidence
* Analyst comments
* Actions performed
* Timeline
* Tickets
* Resolution
* Closure reason

SOAR can automatically create and update these cases.

---

## Q17. How would you integrate ServiceNow with SOAR?

**Answer:**

I would use either a native connector or ServiceNow REST APIs.

The workflow could be:

```text
Security Alert
      ↓
SOAR Investigation
      ↓
Create ServiceNow Incident
      ↓
Add IOC / Investigation Details
      ↓
Assign SOC Team
      ↓
Update Incident
      ↓
Response Completed
      ↓
Close/Resolve Ticket
```

I would also maintain synchronization between SOAR incident status and ServiceNow ticket status.

---

# 9. EDR Integration

## Q18. How would you automate an endpoint isolation workflow?

**Answer:**

For a confirmed malicious endpoint:

```text
EDR Alert
   ↓
SOAR
   ↓
Extract Hostname
   ↓
Check Host Risk
   ↓
Threat Intelligence Enrichment
   ↓
Analyst Approval
   ↓
Isolate Endpoint
   ↓
Collect Evidence
   ↓
Create/Update Ticket
   ↓
Notify SOC
```

I prefer approval gates before high-impact actions such as endpoint isolation unless the organization's policy explicitly allows fully automated containment.

---

# 10. Threat Intelligence

## Q19. What is threat intelligence enrichment?

**Answer:**

Threat intelligence enrichment means adding additional context to indicators such as:

* IP address
* Domain
* URL
* File hash
* Email address

For example:

```text
IOC: 185.x.x.x
       ↓
VirusTotal / TI Platform
       ↓
Reputation
ASN
Country
Malware association
Known campaigns
First/last seen
       ↓
SOAR
```

This context helps determine the severity and appropriate response.

---

# 11. MITRE ATT&CK

## Q20. What is MITRE ATT&CK?

**Answer:**

MITRE ATT&CK is a knowledge base of adversary tactics and techniques based on real-world observations.

The major tactic categories include:

* Initial Access
* Execution
* Persistence
* Privilege Escalation
* Defense Evasion
* Credential Access
* Discovery
* Lateral Movement
* Collection
* Command and Control
* Exfiltration
* Impact

SOAR can use ATT&CK mappings to understand the attack stage and automate appropriate response actions.

---

# 12. Incident Response

## Q21. What are the major phases of incident response?

**Answer:**

A commonly used lifecycle is:

```text
Preparation
    ↓
Detection & Analysis
    ↓
Containment
    ↓
Eradication
    ↓
Recovery
    ↓
Lessons Learned
```

SOAR primarily helps automate activities across detection, analysis, containment, eradication and recovery.

---

# 13. False Positives

## Q22. How do you handle false positives?

**Answer:**

First, I identify why the alert was triggered. Then I analyze historical patterns, affected users/assets and detection conditions.

If it is consistently benign, I would improve the detection or add appropriate exceptions/suppression conditions while ensuring we don't create a security gap.

In SOAR, I can also add conditions so low-risk known-benign cases are automatically closed while suspicious cases are escalated.

---

# 14. Playbook Optimization

## Q23. A SOAR playbook is taking too long. How would you optimize it?

**Answer:**

I would identify the slowest actions first by checking execution logs and metrics.

Then I would look for:

* Unnecessary API calls
* Sequential actions that can run in parallel
* Excessive polling
* Large API responses
* Missing caching
* Slow external integrations
* Unnecessary enrichment
* Poor retry logic

Where possible, independent enrichment calls can execute in parallel.

---

# 15. AI + SOAR

## Q24. How can AI be used in SOAR?

**Answer:**

AI can assist with:

* Alert triage
* Incident summarization
* IOC analysis
* Natural-language investigation
* Playbook generation
* Query generation
* Threat classification
* Recommended response actions
* Analyst decision support

For example:

```text
Security Alert
      ↓
AI analyzes context
      ↓
Summarizes incident
      ↓
Identifies likely attack technique
      ↓
Suggests investigation steps
      ↓
Human validates
      ↓
SOAR executes approved actions
```

---

# 16. What is Anthropic / Claude?

## Q25. What is Anthropic?

**Answer:**

Anthropic is an AI company that develops large language models such as **Claude**.

In a SOAR environment, an LLM such as Claude can be used to assist analysts with tasks such as incident summarization, natural-language investigation, classification, response recommendations and automation development.

The important point is that the LLM should generally operate within **controlled and governed workflows**, rather than having unrestricted access to execute security actions.

---

# 17. AI-Assisted Playbook Generation

## Q26. How can an LLM help create SOAR playbooks?

**Answer:**

An analyst can provide a natural-language requirement such as:

> "When a phishing alert occurs, extract the URL, check its reputation, investigate the sender and create a ServiceNow ticket."

The LLM can help convert that requirement into:

```text
Trigger
  ↓
Extract IOC
  ↓
Threat Intelligence Lookup
  ↓
Risk Assessment
  ↓
Investigation
  ↓
ServiceNow Ticket
  ↓
Response
```

The generated workflow should still be reviewed, tested and approved by an engineer before being deployed to production.

---

# 18. LLM Incident Summarization

## Q27. How would you use an LLM for incident summarization?

**Answer:**

I would provide the LLM with structured incident information such as:

* Alert details
* Timeline
* IOCs
* User/device information
* Detection results
* Investigation results

The LLM can produce:

```text
Incident Summary
Impact
Affected Assets
Attack Timeline
Observed IOCs
Likely Attack Technique
Actions Taken
Recommended Next Steps
```

Sensitive data should be handled according to organizational security and privacy policies.

---

# 19. Human-in-the-Loop

## Q28. What does human-in-the-loop mean in AI security automation?

**Answer:**

Human-in-the-loop means that AI can analyze information and recommend actions, but a human analyst approves important actions before execution.

For example:

```text
AI detects compromised account
        ↓
AI recommends disabling account
        ↓
SOC Analyst reviews
        ↓
Approve
        ↓
SOAR disables account
```

This is especially important for destructive or high-impact actions.

---

# 20. Guardrails for AI in SOAR

## Q29. What guardrails would you implement for AI-enabled SOAR?

**Answer:**

I would implement:

* Role-based access control
* Least privilege
* Human approval for critical actions
* Input/output validation
* Prompt injection protection
* Sensitive-data filtering
* Audit logging
* Tool/API restrictions
* Allowlisted actions
* Rate limits
* Confidence thresholds
* Monitoring and rollback mechanisms

The LLM should not have unrestricted ability to execute arbitrary commands or security actions.

---

# 21. Prompt Injection

## Q30. What is prompt injection?

**Answer:**

Prompt injection occurs when malicious or untrusted input attempts to manipulate an LLM into ignoring its intended instructions or performing unintended actions.

For example, an attacker could place malicious instructions inside an email or document that an AI security agent analyzes.

The model might incorrectly interpret the malicious text as an instruction.

---

# 22. Indirect Prompt Injection

## Q31. What is indirect prompt injection?

**Answer:**

Indirect prompt injection occurs when malicious instructions come from external data that the AI consumes rather than directly from the user.

Example:

```text
Attacker-controlled webpage
        ↓
AI agent reads webpage
        ↓
Malicious instruction embedded in content
        ↓
AI follows instruction
```

This is particularly important for AI-powered SOC agents that process emails, documents, websites or threat-intelligence data.

---

# 23. AI Agent Security

## Q32. What is an AI agent?

**Answer:**

An AI agent is an AI system that can reason about a task and interact with external tools or systems to accomplish it.

For example:

```text
User
 ↓
AI Agent
 ↓
SIEM Search
 ↓
Threat Intelligence
 ↓
EDR
 ↓
ServiceNow
 ↓
Response
```

The main security concern is **excessive agency**—giving the agent more permissions than it actually needs.

---

# 24. How would you secure an AI SOC agent?

**Answer:**

I would apply:

1. Least-privilege permissions.
2. Tool allowlisting.
3. Human approval for high-risk actions.
4. Input validation.
5. Prompt-injection defenses.
6. Output validation.
7. Strong authentication.
8. Audit logging.
9. Rate limiting.
10. Continuous monitoring.

The agent should only have access to the tools and actions required for its specific use case.

---

# 25. LLM Hallucination

## Q33. What is hallucination and why is it dangerous in security?

**Answer:**

Hallucination occurs when an LLM generates information that sounds correct but is actually incorrect or unsupported.

In cybersecurity, this can result in:

* Incorrect incident classification
* False IOC attribution
* Wrong investigation conclusions
* Incorrect remediation
* False positives/negatives

Therefore, AI-generated recommendations should be validated against authoritative security data before critical actions are executed.

---

# 26. Natural Language → Security Query

## Q34. How can LLMs help SOC analysts generate queries?

**Answer:**

An analyst could ask:

> "Show me failed logins for this user from unusual countries during the last 24 hours."

The LLM could translate that into the appropriate query language, such as KQL, SPL or another SIEM query language.

The query should then be validated and executed with appropriate permissions.

---

# 27. SOAR + AI Architecture

## Q35. Design an AI-enabled SOAR architecture.

**Answer:**

I would propose:

```text
                 Security Sources
                       |
        +--------------+--------------+
        |              |              |
       SIEM            EDR            TI
        |              |              |
        +--------------+--------------+
                       |
                    SOAR
                       |
              Incident/Playbook
                       |
                +------+------+
                |             |
             Rules          LLM
                |             |
                +------+------+
                       |
                Decision Support
                       |
               Human Approval
                       |
                Response Tools
                       |
       +-------+-------+-------+
       |       |       |       |
      EDR   IAM    Firewall  ITSM
```

The LLM should assist with reasoning, summarization and recommendations, while deterministic SOAR logic controls actual security actions.

---

# 28. Python Automation

## Q36. How have you used Python in security automation?

**Answer:**

Python can be used to:

* Consume REST APIs
* Process JSON responses
* Extract IOCs
* Normalize security data
* Call threat-intelligence APIs
* Automate investigation
* Generate reports
* Build custom SOAR integrations
* Handle authentication
* Implement retry/error handling

For example:

```python
response = requests.get(
    api_url,
    headers={"Authorization": f"Bearer {token}"}
)

data = response.json()
```

In production, I would also include proper exception handling, timeouts, logging and secure credential management.

---

# 29. JSON

## Q37. Why is JSON important in SOAR?

**Answer:**

Most security products expose REST APIs that exchange data in JSON.

For example:

```json
{
  "alert_id": "12345",
  "severity": "high",
  "source": "EDR",
  "hostname": "host01",
  "indicator": "192.168.1.10"
}
```

SOAR playbooks commonly extract and transform these fields to pass information between different security products.

---

# 30. Cortex XSOAR

## Q38. What are the important concepts in Cortex XSOAR?

**Answer:**

Important concepts include:

* Incidents
* Indicators
* Playbooks
* Integrations
* Commands
* Context
* Automations
* Scripts
* Jobs
* Classifiers
* Incident types
* Layouts
* War Rooms

A playbook orchestrates multiple commands and integrations to automate investigation and response.

---

# 31. Splunk SOAR

## Q39. What is Splunk SOAR?

**Answer:**

Splunk SOAR is a security orchestration and automation platform used to automate security operations.

It provides:

* Playbooks
* Apps
* Actions
* Investigations
* Case management
* Integrations
* Automation workflows

It can integrate with SIEM, EDR, firewalls, threat intelligence and ITSM platforms.

---

# 32. XSOAR vs Splunk SOAR

## Q40. What is the difference?

**Answer:**

Both provide SOAR capabilities, but their ecosystems differ.

**Cortex XSOAR** is strongly integrated with Palo Alto Networks' security ecosystem and provides extensive incident/indicator management and playbook capabilities.

**Splunk SOAR** integrates naturally with Splunk and provides app-based orchestration and visual playbook automation.

The core concept remains similar:

```text
Alert → Investigation → Enrichment → Decision → Response
```

---

# 33. SOAR Automation Example

## Q41. Give a real-world SOAR automation example.

**Answer:**

Suppose Sentinel detects a suspicious login.

```text
Sentinel Alert
      ↓
SOAR
      ↓
Extract User + IP
      ↓
Check IP Reputation
      ↓
Check User Risk
      ↓
Check Previous Login History
      ↓
Determine Risk
      ↓
If High Risk
      ↓
Revoke Sessions
      ↓
Disable Account / Require Password Reset
      ↓
Create ServiceNow Ticket
      ↓
Notify SOC
```

This reduces manual investigation time and allows analysts to focus on complex incidents.

---

# 34. Automation vs Manual Response

## Q42. What should and shouldn't be automated?

**Answer:**

Good automation candidates are:

* IOC enrichment
* Reputation checks
* Data collection
* Ticket creation
* Notification
* Repetitive investigation
* Low-risk remediation

High-impact actions such as:

* Disabling critical accounts
* Isolating critical production servers
* Blocking business-critical IPs
* Deleting large numbers of emails

may require human approval depending on the organization's risk policy.

---

# 35. Automation Metrics

## Q43. How do you measure SOAR effectiveness?

**Answer:**

Important metrics include:

* Mean Time to Detect — MTTD
* Mean Time to Respond — MTTR
* Automation rate
* Alert closure time
* False-positive rate
* Playbook success rate
* Playbook failure rate
* Analyst hours saved
* Number of automated incidents
* API/integration failure rate

The ultimate goal is to reduce response time while maintaining accuracy and control.

---

# 36. Troubleshooting Playbooks

## Q44. A playbook is failing randomly. How do you troubleshoot it?

**Answer:**

I would inspect the playbook execution logs and identify the failing action.

Then I would check:

```text
Input Data
   ↓
Authentication
   ↓
API Request
   ↓
HTTP Status
   ↓
Response Payload
   ↓
Parsing
   ↓
Next Action
```

I would also check whether the issue is caused by API rate limits, inconsistent input data, expired credentials, vendor changes, timeouts or race conditions.

---

# 37. Rate Limiting

## Q45. What is API rate limiting?

**Answer:**

Rate limiting restricts the number of API requests that a client can make within a specific period.

For example:

```text
100 requests/minute
```

If the SOAR platform exceeds this limit, the API may return:

```text
HTTP 429 Too Many Requests
```

I would handle this using throttling, exponential backoff, retries and batching where supported.

---

# 38. Idempotency

## Q46. What is idempotency and why is it useful in SOAR?

**Answer:**

An operation is idempotent when performing it multiple times produces the same final result.

This is important in automation because retries can accidentally perform the same action multiple times.

For example, before creating a ServiceNow ticket, the playbook can check whether an existing ticket already exists for the same incident.

---

# 39. Security of Integrations

## Q47. How do you secure SOAR integrations?

**Answer:**

I would use:

* Least-privilege service accounts
* Secure credential stores
* API tokens with minimum permissions
* TLS
* Network restrictions
* IP allowlisting where appropriate
* Secret rotation
* Audit logging
* RBAC
* Separate credentials for environments

Credentials should never be hardcoded inside playbooks or scripts.

---

# 40. Cloud Security

## Q48. How can SOAR integrate with AWS/Azure/GCP?

**Answer:**

SOAR can integrate with cloud security services through APIs or native connectors.

Examples:

```text
Cloud Alert
   ↓
SOAR
   ↓
Investigate IAM/User
   ↓
Check CloudTrail / Activity Logs
   ↓
Determine Risk
   ↓
Revoke Credentials / Disable User
   ↓
Create Ticket
```

The exact response depends on the cloud platform and organizational policies.

---

# 41. Scenario-Based Question

## Q49. Sentinel generates a high-severity alert for a compromised user. What would you do?

**Answer:**

I would:

1. Validate the alert.
2. Identify the affected user.
3. Check sign-in history.
4. Investigate source IP/location/device.
5. Check threat intelligence.
6. Check endpoint activity.
7. Determine whether the account is actually compromised.
8. Revoke sessions or disable the account if required.
9. Create/update the ServiceNow case.
10. Document the investigation and response.

---

# 42. Scenario-Based Question

## Q50. A SOAR playbook isolates the wrong endpoint. What would you do?

**Answer:**

First, I would stop or disable the problematic automation if it is still running.

Then I would:

* Identify why the wrong hostname was selected.
* Check input parsing and correlation logic.
* Review API requests/responses.
* Validate asset identifiers.
* Check enrichment results.
* Add validation/approval gates.
* Test the corrected playbook in a non-production environment.
* Deploy after proper validation.

I would also review whether the automation caused any business impact.

---

# 43. Scenario-Based AI Question

## Q51. An AI agent recommends disabling an employee account. Would you allow it automatically?

**Answer:**

Not blindly.

I would use a governed workflow where the AI provides the reasoning and recommendation, but a deterministic policy and/or human analyst validates the evidence before a high-impact action is executed.

For example:

```text
AI Recommendation
       ↓
Risk/Policy Validation
       ↓
Human Approval
       ↓
SOAR Action
```

---

# 44. AI Prompt Engineering

## Q52. What is prompt engineering?

**Answer:**

Prompt engineering is the process of designing instructions and context so that an LLM produces reliable and useful output.

For security automation, I would clearly define:

* Role
* Task
* Context
* Expected output format
* Security constraints
* Allowed actions
* Examples where appropriate

I would also avoid allowing untrusted input to override system-level instructions.

---

# 45. Structured Output

## Q53. Why is structured output important for LLM-based SOAR?

**Answer:**

Structured output makes AI responses easier and safer for automation to consume.

Instead of:

```text
I think this is probably a high-risk incident...
```

we can require:

```json
{
  "severity": "high",
  "confidence": 0.91,
  "recommended_action": "isolate_endpoint"
}
```

The SOAR workflow can then validate the fields before taking any action.

---

# 46. AI Decision Support

## Q54. What is AI decision support?

**Answer:**

AI decision support means the AI assists analysts by summarizing evidence, identifying patterns and recommending actions, while the final decision remains controlled by predefined policies or human analysts.

This is safer than allowing the LLM to independently make unrestricted security decisions.

---

# 47. Your Experience Question

## Q55. Tell me about your SOAR experience.

**Answer:**

> In my current role, I work as a SIEM/SOAR Engineer where I build and maintain security integrations, event-processing pipelines, detection content and automation workflows. I have worked with platforms such as Cortex XSOAR, Splunk SOAR, Microsoft Sentinel, Google Security Operations, Elastic and Splunk, along with EDR, threat-intelligence and ITSM integrations. I develop custom integrations using Python, Go, Node.js, REST APIs and webhooks, and work on playbooks for enrichment, investigation, alert handling and response automation.

---

# 48. Why Deloitte?

## Q56. Why do you want to join Deloitte?

**Answer:**

> Deloitte's Cyber Operate practice is interesting to me because it combines SOC operations, SOAR automation, security engineering and emerging AI capabilities. My current experience in SIEM/SOAR integrations, playbook development, API automation and security operations aligns well with the role. I also see this as an opportunity to work with different client environments and build scalable security automation solutions.

---

# 49. Why this role?

## Q57. Why are you interested in the SOAR + Anthropic role?

**Answer:**

> The role combines two areas I am particularly interested in: security automation and AI. I already have experience building SOAR integrations, playbooks and security workflows, and I have also been working with AI/LLM-based automation. The opportunity to apply LLMs to alert triage, incident summarization and governed response workflows is a natural extension of my current experience.

---

# 50. Most Important Rapid-Fire Questions

Before the interview, make sure you can answer these without hesitation:

### SOAR

* What is SOAR?
* SIEM vs SOAR?
* What is a playbook?
* What is an integration?
* What is a connector?
* What is an automation?
* What is case management?
* What is incident enrichment?
* What is orchestration?
* What should be automated?

### APIs

* REST API?
* GET vs POST vs PUT vs PATCH?
* Webhook?
* OAuth?
* API key?
* Bearer token?
* HTTP status codes?
* 401 vs 403?
* 429?
* Retry mechanism?
* Rate limiting?
* Idempotency?

### SOC

* Alert triage?
* True positive vs false positive?
* Incident response lifecycle?
* MTTD?
* MTTR?
* Severity vs priority?
* IOC?
* TTP?
* Threat intelligence?

### Security

* MITRE ATT&CK?
* EDR?
* SIEM?
* IAM?
* Firewall?
* Phishing?
* Malware?
* Account compromise?
* Endpoint isolation?

### AI / Anthropic

* What is an LLM?
* What is Anthropic?
* What is Claude?
* Prompt engineering?
* Prompt injection?
* Indirect prompt injection?
* Jailbreaking?
* Hallucination?
* Excessive agency?
* AI agents?
* Human-in-the-loop?
* AI guardrails?
* LLM-based incident summarization?
* Natural language → KQL/SPL?
* AI-assisted playbook generation?

---

# 51. Highest-Priority Topics for This Deloitte JD

If you have limited preparation time, prioritize in this order:

```text
★★★★★ SOAR Playbooks
★★★★★ Cortex XSOAR / Splunk SOAR
★★★★★ SIEM → SOAR workflow
★★★★★ REST APIs + Webhooks
★★★★★ Incident Response
★★★★★ Alert Triage
★★★★★ ServiceNow / ITSM
★★★★★ Python Automation
★★★★★ EDR + Threat Intelligence integrations
★★★★★ Troubleshooting integrations/playbooks

★★★★ MITRE ATT&CK
★★★★ Cloud Security
★★★★ SOAR Metrics
★★★★ API Authentication
★★★★ Error Handling / Retry / Rate Limiting

★★★★★ AI + SOAR
★★★★★ LLM Security
★★★★★ Prompt Injection
★★★★★ AI Agents
★★★★★ Human-in-the-Loop
★★★★★ AI Guardrails
★★★★★ Incident Summarization
★★★★★ AI-assisted Playbook Generation
```

---

# 52. One-Minute Architecture Answer

If the interviewer asks:

**"Explain how you would build an automated SOC response system."**

Use this answer:

> I would have the SIEM collect and correlate security telemetry and generate alerts. The alerts would be sent to SOAR, where a playbook performs enrichment using threat intelligence, EDR, IAM and other security tools through APIs or native connectors. Based on deterministic rules and risk scoring, the playbook can automatically perform low-risk actions, while high-impact actions can require analyst approval. For AI-enabled workflows, an LLM can assist with incident summarization, investigation and response recommendations, but I would keep it behind strong guardrails, validation and human-in-the-loop controls. Finally, the response and evidence would be recorded in the case-management/ITSM system.

---

# 53. Strong Closing Statement

If the interviewer asks **"Do you have anything else you'd like to add?"**, you can say:

> My experience sits at the intersection of software engineering and security operations. I bring hands-on experience with SIEM/SOAR platforms, API-based integrations, event processing, playbook automation and security response workflows. I am particularly interested in the AI side of this role because I believe LLMs can significantly improve SOC efficiency when they're implemented with proper security controls, deterministic automation and human oversight.

# 54. detection and response, what are types of it, stages of that, what u do when detection & response alerts are generated

1. What are the types of Detection & Response?

There isn't one universal classification, but in a SOC we commonly talk about detection/response based on the security domain:

- Endpoint Detection & Response (EDR) – detects malware, suspicious processes, ransomware, etc.
- Network Detection & Response (NDR) – detects malicious network traffic, C2, lateral movement, etc.
- Identity Detection & Response (IDR) – detects compromised accounts, impossible travel, brute force, privilege abuse.
- Cloud Detection & Response – detects suspicious cloud activity, IAM misuse, abnormal API calls.
- Email Detection & Response – detects phishing, malicious attachments, malicious URLs.
- Threat Detection & Response – detects known/unknown threats using IOCs, TTPs and behavioral analytics.

You can also mention XDR (Extended Detection & Response), which correlates signals across endpoint, network, identity, email and cloud.

1. What are the types of Detection & Response?

There isn't one universal classification, but in a SOC we commonly talk about detection/response based on the security domain:

Endpoint Detection & Response (EDR) – detects malware, suspicious processes, ransomware, etc.
Network Detection & Response (NDR) – detects malicious network traffic, C2, lateral movement, etc.
Identity Detection & Response (IDR) – detects compromised accounts, impossible travel, brute force, privilege abuse.
Cloud Detection & Response – detects suspicious cloud activity, IAM misuse, abnormal API calls.
Email Detection & Response – detects phishing, malicious attachments, malicious URLs.
Threat Detection & Response – detects known/unknown threats using IOCs, TTPs and behavioral analytics.

You can also mention XDR (Extended Detection & Response), which correlates signals across endpoint, network, identity, email and cloud.

2. Stages of Detection & Response

A good interview answer is:

1. Detection
      ↓
2. Alert Generation
      ↓
3. Triage
      ↓
4. Investigation
      ↓
5. Enrichment
      ↓
6. Containment
      ↓
7. Eradication / Remediation
      ↓
8. Recovery
      ↓
9. Closure & Lessons Learned
1. Detection

Security tools detect suspicious activity using rules, signatures, behavioral analytics, correlation, or threat intelligence.

2. Alert Generation

The SIEM/EDR/NDR generates an alert containing information such as:

User
Host
IP
Timestamp
IOC
Severity
Detection rule
3. Triage

The SOC analyst determines:

Is this a true positive or false positive, and how serious is it?

4. Investigation

Analyze logs and security telemetry to understand:

What happened?
Who/what is affected?
How did it happen?
Is the attacker still active?
What is the scope?
5. Enrichment

Use additional sources such as:

Threat Intelligence
EDR
SIEM
IAM
DNS
WHOIS
VirusTotal
Firewall
Cloud logs

to get more context.

6. Containment

Stop the attack from spreading.

Examples:

Isolate endpoint
Disable compromised account
Block malicious IP/domain
Revoke sessions
Quarantine email
7. Eradication / Remediation

Remove the root cause.

Examples:

Remove malware
Kill malicious process
Delete persistence
Reset credentials
Patch vulnerability
8. Recovery

Restore affected systems and monitor them to ensure the attacker is gone.

9. Closure

Document the incident, actions taken, evidence, root cause and lessons learned.

# 55. What is ai security?

Yes — partially, but saying “AI security is just normal security with a different data source” would be too simplistic in an interview.

What is AI Security?

AI security is the practice of protecting AI/LLM systems, their data, models, agents, APIs and users from security threats, while also monitoring AI-specific risks such as prompt injection, data leakage, model abuse and excessive agency.

Is the data source different?

Yes, that's one major difference, but there are additional AI-specific attack surfaces.

Traditional SOC:

Endpoint / Network / Firewall / IAM
              ↓
             SIEM
              ↓
            Alert
              ↓
        Investigation
              ↓
           Response

AI Security:

AI App / LLM / Agent / API
          ↓
 Prompts + Responses + AI Logs
          ↓
    AI Security Platform
          ↓
        Alert
          ↓
   Investigation
          ↓
      Response

The SOC process remains largely the same:

Detect → Triage → Investigate → Enrich → Respond → Recover

But the things you're detecting are different.

Example

Traditional security alert:

"User logged in from an unusual IP."

AI security alert:

"User prompt attempted to bypass system instructions using a prompt injection."

Or:

"AI agent attempted to access a sensitive database that it wasn't authorized to access."

Or:

"LLM response exposed sensitive customer information."

Key difference
Traditional Security	AI Security
Network attacks	Prompt injection
Malware	Jailbreaking
Phishing	Data leakage through LLM
Credential attacks	Model abuse
Suspicious processes	Malicious AI-agent behavior
Unauthorized access	Excessive AI-agent permissions
C2 traffic	Malicious tool/API invocation
Best interview answer

AI security follows the same fundamental detection and response principles as traditional cybersecurity, but the attack surface and telemetry are different. Instead of only monitoring endpoints, networks and identities, we also monitor AI applications, prompts, responses, models, agents and tool/API interactions. So the SOC workflow remains similar—detect, triage, investigate and respond—but we need additional AI-specific detections such as prompt injection, jailbreaks, sensitive-data leakage and excessive agency.

One important point: AI security isn't only about the data source. It's also about securing the AI system itself and controlling what the AI is allowed to do.

# 56. what action / step u take when aleert is generated?

When an alert is generated, I first **triage and validate** it to determine whether it is a true positive or false positive.
Then I **enrich and investigate** the alert using SIEM, EDR, threat intelligence, identity, and network data.
If it is a confirmed threat, I **contain and remediate** it using SOAR actions such as isolating an endpoint, blocking an IOC, or disabling a compromised account.
Finally, I **update the incident/ticket, document the actions taken, and escalate or close** the alert based on the investigation outcome.

# 57. How exactly u create playbooks?

> I first understand the **alert/use case and response requirement**, including what needs to be investigated and what actions should be automated. Then I identify the required **integrations and data sources**, such as SIEM, EDR, threat intelligence, IAM, firewall, and ServiceNow, and verify their APIs/connectors and permissions.
>
> Next, I design the workflow with **trigger → enrichment → investigation → decision/conditions → response → ticket update**. I add error handling, retries, timeouts, logging, and approval gates for high-impact actions.
>
> After development, I test the playbook with **sample alerts and different scenarios**, including success, failure, missing data, and false-positive cases. I validate the API responses and each action before deploying it to production.
>
> Finally, I monitor the playbook in production using **execution logs, success/failure rates, response time, and automation metrics**, and continuously optimize it based on SOC analyst feedback.

### Example: Suspicious IP Playbook

```text
SIEM Alert
    ↓
Extract IP Address
    ↓
Check IP Reputation
    ↓
Threat Intelligence Enrichment
    ↓
Check EDR / Network Activity
    ↓
Is IP Malicious?
    ├── No → Update Case → Close
    │
    └── Yes
          ↓
     Assess Severity
          ↓
   Analyst Approval
          ↓
     Block IP / IOC
          ↓
   Create/Update ServiceNow
          ↓
      Notify SOC
          ↓
        Close
```

### Simple formula to remember

**Understand Use Case → Identify Integrations → Design Workflow → Build → Add Error Handling → Test → Deploy → Monitor & Optimize**

## 58. What is the most complex playbook you have created so far?

> One of the more complex playbooks I worked on was an **automated security incident investigation and response workflow involving multiple security platforms**. The playbook was triggered by a SIEM alert and extracted indicators such as IP addresses, domains, hashes, users, and host information.
>
> It then performed **parallel enrichment** using threat-intelligence and EDR integrations, correlated the results, and applied conditional logic to determine the risk and severity of the incident. Based on the result, it could perform actions such as blocking a malicious IOC, isolating an endpoint, or initiating additional investigation, with approval required for high-impact actions.
>
> I also integrated **ServiceNow for case management**, so the playbook automatically created and updated incidents with investigation evidence and response actions. I handled API authentication, timeouts, retries, error scenarios, and logging to make the workflow reliable.
>
> The challenging part was ensuring that data from different security products was **normalized and correctly correlated**, while making sure a failure in one integration didn't stop the entire investigation. I tested the playbook with true-positive, false-positive, missing-data, API-failure, and timeout scenarios before production deployment.

### Architecture

```text
                    SIEM Alert
                        ↓
                 SOAR Playbook
                        ↓
               Extract IOCs/Entities
                        ↓
              ┌─────────┴─────────┐
              ↓         ↓         ↓
             EDR        TI        IAM
              ↓         ↓         ↓
              └─────────┬─────────┘
                        ↓
                Correlate Results
                        ↓
                 Risk Assessment
                        ↓
              ┌─────────┴─────────┐
              ↓                   ↓
          Low/Medium              High
              ↓                   ↓
        Automated Action     Analyst Approval
              ↓                   ↓
              └─────────┬─────────┘
                        ↓
               Containment/Response
                        ↓
                  ServiceNow
                        ↓
                Notify SOC / Close
```

### If they ask "What made it complex?"

I would say:

> **The complexity came from orchestrating multiple integrations, handling different API formats and failures, correlating data from multiple sources, implementing conditional response logic, and ensuring that high-impact actions were properly controlled.**
