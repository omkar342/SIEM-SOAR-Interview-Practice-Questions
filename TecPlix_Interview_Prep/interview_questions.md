1\. Tell me about yourself.
---------------------------

**Answer:**

> I have around 3 years of experience in software and cybersecurity, currently working as a SIEM/SOAR Engineer at Metron Security. I work across Google Security Operations, Microsoft Sentinel, Splunk, Elastic/Kibana, CrowdStrike, Splunk SOAR and Cortex XSOAR. My work includes log ingestion, parsing, normalization, detection content, alert investigation, threat enrichment and SOAR playbook automation. I also work with Python, JavaScript/Node.js and REST APIs to build security integrations and automate SOC workflows.

2\. What is SIEM?
=================

**Answer:**

> SIEM stands for Security Information and Event Management. It collects logs from different sources such as firewalls, VPNs, endpoints, applications and identity systems, normalizes and correlates them, and generates security alerts. Examples include Google Chronicle, Splunk, Microsoft Sentinel and Sumo Logic.

3\. What is SOAR?
=================

**Answer:**

> SOAR stands for Security Orchestration, Automation and Response. It connects security tools and automates investigation and response workflows using playbooks. For example, when a SIEM detects a malicious IP, SOAR can automatically enrich the IP using threat intelligence, check related endpoints, block the IP on a firewall and notify the SOC team.

4\. SIEM vs SOAR?
=================

SIEMSOARCollects and analyzes logsAutomates investigation and responseCorrelates eventsExecutes playbooksGenerates alertsActs on alertsDetection-focusedResponse-focusedExample: Chronicle, SplunkExample: Cortex XSOAR, Splunk SOAR

**Interview answer:**

> SIEM primarily focuses on collecting, correlating and detecting threats, while SOAR focuses on orchestrating and automating the investigation and response to those alerts.

5\. What happens when a SIEM alert is generated?
================================================

**Answer:**

> First, I validate the alert and understand why it was triggered. Then I investigate the related user, IP, endpoint and events, enrich the indicators using threat-intelligence sources and correlate them with other available telemetry. Based on the severity and confidence, I either close it as a false positive, escalate it, or trigger a SOAR playbook for automated containment and remediation.

6\. What is your alert investigation process?
=============================================

**Answer:**

Plain textANTLR4BashCC#CSSCoffeeScriptCMakeDartDjangoDockerEJSErlangGitGoGraphQLGroovyHTMLJavaJavaScriptJSONJSXKotlinLaTeXLessLuaMakefileMarkdownMATLABMarkupObjective-CPerlPHPPowerShell.propertiesProtocol BuffersPythonRRubySass (Sass)Sass (Scss)SchemeSQLShellSwiftSVGTSXTypeScriptWebAssemblyYAMLXML`   Alert received        ↓  Validate detection        ↓  Check severity and context        ↓  Investigate user/IP/endpoint        ↓  Correlate related events        ↓  Threat intelligence enrichment        ↓  Determine true/false positive        ↓  Contain / remediate / escalate        ↓  Document findings   `

7\. How do you create a detection rule?
=======================================

**Answer:**

> I first understand the attack behavior and identify the relevant log sources and fields. Then I define the detection logic using conditions, thresholds, exclusions and correlation requirements. After that I test the rule against historical or sample data, tune false positives, map it to MITRE ATT&CK where applicable, and finally deploy it to production with monitoring.

8\. What is correlation in SIEM?
================================

**Answer:**

> Correlation means connecting multiple events or signals to identify a meaningful security incident. For example, a VPN login from an unusual country followed by privilege escalation and suspicious endpoint activity can be correlated into a single incident rather than treating each event independently.

9\. What is a SIEM use case?
============================

**Answer:**

> A SIEM use case defines a specific security behavior that we want to detect.

Examples:

*   Multiple failed logins
    
*   Successful login after multiple failures
    
*   Impossible travel
    
*   Suspicious PowerShell execution
    
*   Data exfiltration
    
*   Malware detection
    
*   Privilege escalation
    
*   VPN anomaly
    

10\. How would you create a brute-force detection?
==================================================

**Answer:**

> I would monitor authentication logs for multiple failed login attempts from the same source IP or against the same account within a defined time window. I would then correlate a successful login after those failures and increase the severity. I would also add exclusions for known scanners, service accounts or trusted systems to reduce false positives.

11\. How would you detect impossible travel?
============================================

**Answer:**

> I would correlate successful authentication events for the same user from different geographic locations within an unrealistic time period. For example, if a user logs in from India and then from the US within 20 minutes, I would calculate the implied travel distance and flag it if it exceeds a reasonable threshold.

12\. What is MITRE ATT&CK?
==========================

**Answer:**

> MITRE ATT&CK is a knowledge base of adversary tactics and techniques based on real-world attacks. It helps SOC teams understand attacker behavior and map detections and response procedures to techniques such as Credential Access, Persistence, Execution and Command and Control.

13\. Why do you map detections to MITRE ATT&CK?
===============================================

**Answer:**

> It helps us understand what attacker behavior our detection covers and identify gaps in our detection coverage. It also provides a common language between detection engineering, threat intelligence, SOC and incident response teams.

14\. What is Sigma?
===================

**Answer:**

> Sigma is a generic, vendor-neutral rule format for describing detection logic. A Sigma rule can be written once and then converted into queries for different SIEM platforms such as Splunk, Elastic or other supported systems.

15\. Sigma vs SIEM query?
=========================

**Answer:**

> Sigma is a vendor-neutral detection format, whereas a SIEM query is specific to a particular platform.

For example:

Plain textANTLR4BashCC#CSSCoffeeScriptCMakeDartDjangoDockerEJSErlangGitGoGraphQLGroovyHTMLJavaJavaScriptJSONJSXKotlinLaTeXLessLuaMakefileMarkdownMATLABMarkupObjective-CPerlPHPPowerShell.propertiesProtocol BuffersPythonRRubySass (Sass)Sass (Scss)SchemeSQLShellSwiftSVGTSXTypeScriptWebAssemblyYAMLXML`   Sigma    ↓  Conversion    ↓  Splunk SPL / Elastic Query / SIEM-specific query   `

16\. What is YARA?
==================

**Answer:**

> YARA is a rule-based pattern-matching technology commonly used to identify malware and suspicious files based on strings, byte patterns, file characteristics or other conditions. It is primarily useful for malware identification and threat hunting.

17\. Sigma vs YARA?
===================

SigmaYARADetection rule formatPattern-matching rulePrimarily security logs/eventsPrimarily files/malwareSIEM-orientedMalware/threat-hunting orientedVendor-neutralUsed for identifying file/content patterns

18\. What is Chronicle / Google Security Operations?
====================================================

**Answer:**

> Google Security Operations, formerly Google Chronicle, is a cloud-native security operations platform that provides large-scale security telemetry ingestion, search, detection, investigation and threat intelligence capabilities. It can ingest security data from multiple sources and use detection rules to identify suspicious activity.

19\. What is Chronicle Backstory?
=================================

**Answer:**

> Backstory was the original name associated with Google's cloud-native security analytics platform. It provided large-scale security telemetry search, investigation and detection capabilities. In the current Google Security Operations terminology, Chronicle/Backstory concepts are generally discussed under Google SecOps.

20\. What is UDM in Chronicle?
==============================

**Answer:**

> UDM stands for Unified Data Model. It provides a normalized representation of security events so that different log sources can be searched and detected consistently.

For example:

Plain textANTLR4BashCC#CSSCoffeeScriptCMakeDartDjangoDockerEJSErlangGitGoGraphQLGroovyHTMLJavaJavaScriptJSONJSXKotlinLaTeXLessLuaMakefileMarkdownMATLABMarkupObjective-CPerlPHPPowerShell.propertiesProtocol BuffersPythonRRubySass (Sass)Sass (Scss)SchemeSQLShellSwiftSVGTSXTypeScriptWebAssemblyYAMLXML`   Firewall logs  VPN logs  Endpoint logs  Authentication logs         ↓     Parsing         ↓  UDM normalization         ↓  Detection / Investigation   `

21\. What is log parsing?
=========================

**Answer:**

> Log parsing converts raw logs into structured fields that the SIEM can understand. For example, from a raw firewall log we extract fields such as source IP, destination IP, port, action, timestamp and username.

22\. What is normalization?
===========================

**Answer:**

> Normalization means mapping different vendor-specific fields into a common schema. For example, one vendor may call a field src\_ip, another sourceAddress, but we normalize both into a common source-IP field.

23\. What would you do if logs are coming into SIEM but detection is not triggering?
====================================================================================

**Answer:**

> I would first verify ingestion and timestamps, then check whether the parser is correctly extracting the required fields. Next I would validate the normalized fields against the detection query and test the rule using actual events. I would also check filtering, time windows, thresholds and rule deployment status before identifying whether the issue is with ingestion, parsing or detection logic.

24\. What if logs are not coming into the SIEM?
===============================================

**Answer:**

> I would check the complete ingestion pipeline: source availability, network connectivity, collector/agent status, authentication, configuration, transport protocol and SIEM ingestion status. Then I would inspect raw logs and errors to identify whether the issue is at the source, transport, parser or SIEM side.

25\. What is threat intelligence enrichment?
============================================

**Answer:**

> Threat intelligence enrichment adds additional context to an indicator such as an IP, domain, URL or hash. For example, when an alert contains an IP address, we can query a threat-intelligence service to determine its reputation, associated malware, ASN, geolocation or previous malicious activity.

26\. How would you integrate threat intelligence into SOAR?
===========================================================

**Answer:**

Plain textANTLR4BashCC#CSSCoffeeScriptCMakeDartDjangoDockerEJSErlangGitGoGraphQLGroovyHTMLJavaJavaScriptJSONJSXKotlinLaTeXLessLuaMakefileMarkdownMATLABMarkupObjective-CPerlPHPPowerShell.propertiesProtocol BuffersPythonRRubySass (Sass)Sass (Scss)SchemeSQLShellSwiftSVGTSXTypeScriptWebAssemblyYAMLXML`   SIEM Alert      ↓  Extract IOC      ↓  Validate IOC      ↓  Threat Intelligence API      ↓  Reputation / Context      ↓  Risk assessment      ↓  Automated action   `

> Based on the confidence and severity, the playbook can block the IOC, isolate an endpoint, create a ticket or notify an analyst.

27\. What is a SOAR playbook?
=============================

**Answer:**

> A SOAR playbook is an automated workflow that defines the actions to perform when a security event occurs. It can contain decision conditions, API calls, enrichment, investigation, containment, notification and ticketing steps.

28\. How exactly do you create a SOAR playbook?
===============================================

**Answer:**

> I first define the alert trigger and required inputs. Then I identify the investigation and enrichment steps, integrate the required security tools using connectors or APIs, add decision conditions, and define the response actions. Finally, I test the playbook with different scenarios, handle failures and edge cases, add logging, and deploy it to production.

29\. Give an example of a SOAR playbook.
========================================

**Answer:**

### Suspicious IP Playbook

Plain textANTLR4BashCC#CSSCoffeeScriptCMakeDartDjangoDockerEJSErlangGitGoGraphQLGroovyHTMLJavaJavaScriptJSONJSXKotlinLaTeXLessLuaMakefileMarkdownMATLABMarkupObjective-CPerlPHPPowerShell.propertiesProtocol BuffersPythonRRubySass (Sass)Sass (Scss)SchemeSQLShellSwiftSVGTSXTypeScriptWebAssemblyYAMLXML`   SIEM Alert      ↓  Extract source IP      ↓  Check IP reputation      ↓  Check internal activity      ↓  Check affected users/endpoints      ↓  Is IP malicious?     / \   Yes  No   ↓     ↓  Block  Close/  IP     Escalate   ↓  Create incident   ↓  Notify SOC   `

30\. What is the most complex playbook you have worked on?
==========================================================

**Answer:**

> One of the more complex workflows I've worked with involved integrating security platforms and automating investigation and response across multiple systems. The playbook consumed an alert, extracted indicators, enriched them through external/internal security tools, correlated the results, and based on the risk level performed actions such as containment, ticket creation and notification. The challenging part was handling API failures, asynchronous operations, duplicate alerts and ensuring that automated actions were only performed when confidence was high.

31\. How do you prevent SOAR playbooks from taking dangerous automated actions?
===============================================================================

**Answer:**

> I use confidence and severity-based decision points. High-confidence indicators can be automatically contained, while uncertain cases are sent for analyst approval. I also implement allowlists, validation steps, rollback actions, error handling and audit logging before performing destructive actions.

32\. What is human-in-the-loop automation?
==========================================

**Answer:**

> Human-in-the-loop means automation performs investigation and prepares the response, but requires analyst approval before performing a sensitive action.

Example:

Plain textANTLR4BashCC#CSSCoffeeScriptCMakeDartDjangoDockerEJSErlangGitGoGraphQLGroovyHTMLJavaJavaScriptJSONJSXKotlinLaTeXLessLuaMakefileMarkdownMATLABMarkupObjective-CPerlPHPPowerShell.propertiesProtocol BuffersPythonRRubySass (Sass)Sass (Scss)SchemeSQLShellSwiftSVGTSXTypeScriptWebAssemblyYAMLXML`   Alert   ↓  Automated investigation   ↓  Threat enrichment   ↓  Risk = HIGH   ↓  Analyst approval   ↓  Disable account / isolate endpoint   `

33\. What is Cortex XSOAR / Demisto?
====================================

**Answer:**

> Cortex XSOAR, originally Demisto, is a SOAR platform used to orchestrate security tools, automate investigations and manage incident-response workflows through playbooks, integrations, scripts and commands.

34\. What is the difference between an integration, command and playbook in XSOAR?
==================================================================================

**Answer:**

ComponentPurposeIntegrationConnects XSOAR with an external productCommandPerforms a specific operation through an integrationPlaybookCombines multiple commands and decisions into a workflow

Example:

Plain textANTLR4BashCC#CSSCoffeeScriptCMakeDartDjangoDockerEJSErlangGitGoGraphQLGroovyHTMLJavaJavaScriptJSONJSXKotlinLaTeXLessLuaMakefileMarkdownMATLABMarkupObjective-CPerlPHPPowerShell.propertiesProtocol BuffersPythonRRubySass (Sass)Sass (Scss)SchemeSQLShellSwiftSVGTSXTypeScriptWebAssemblyYAMLXML`   CrowdStrike Integration          ↓  Get Host Details          ↓  XSOAR Playbook          ↓  Investigate → Decide → Contain   `

35\. How do you integrate an external security product with XSOAR?
==================================================================

**Answer:**

> I first understand the product's REST API and authentication mechanism. Then I configure or develop the integration, define commands and input/output mappings, test API connectivity, validate responses and error handling, and finally use those commands inside playbooks.

36\. How would you integrate Palo Alto with SOAR?
=================================================

**Answer:**

> I would use the Palo Alto integration/API to perform actions such as querying security events, retrieving threat information or blocking an indicator. The SOAR playbook would validate the IOC first and then invoke the appropriate Palo Alto command based on the incident severity and confidence.

37\. How would you create a playbook for a malicious IP?
========================================================

**Answer:**

Plain textANTLR4BashCC#CSSCoffeeScriptCMakeDartDjangoDockerEJSErlangGitGoGraphQLGroovyHTMLJavaJavaScriptJSONJSXKotlinLaTeXLessLuaMakefileMarkdownMATLABMarkupObjective-CPerlPHPPowerShell.propertiesProtocol BuffersPythonRRubySass (Sass)Sass (Scss)SchemeSQLShellSwiftSVGTSXTypeScriptWebAssemblyYAMLXML`   Trigger: Malicious IP Alert            ↓  Extract IP            ↓  Validate IP            ↓  Threat Intelligence Lookup            ↓  Check Firewall/Proxy Activity            ↓  Check Endpoint Connections            ↓  Is confidence HIGH?         /       \       Yes        No        ↓          ↓  Block IP     Analyst Review        ↓  Create Ticket        ↓  Notify SOC        ↓  Document Action   `

38\. What are common SOAR playbook failure scenarios?
=====================================================

**Answer:**

*   API timeout
    
*   Invalid credentials
    
*   Rate limiting
    
*   External service unavailable
    
*   Invalid IOC
    
*   Missing alert fields
    
*   Duplicate alerts
    
*   Unexpected API response
    
*   Partial execution
    
*   Permission issues
    

> I handle these using retries, timeouts, exception handling, validation, logging and fallback/manual-review paths.

39\. How do you handle duplicate alerts?
========================================

**Answer:**

> I use deduplication keys based on attributes such as incident ID, IOC, username, source IP or a combination of relevant fields. I also use correlation windows and incident grouping so that multiple events related to the same activity don't create unnecessary incidents.

40\. What is incident grouping?
===============================

**Answer:**

> Incident grouping combines related alerts into a single incident based on common attributes such as user, host, IP, campaign or time window. This reduces alert noise and gives analysts a complete picture of the attack.

41\. What is alert tuning?
==========================

**Answer:**

> Alert tuning means adjusting detection conditions to improve the balance between detection accuracy and false positives. I analyze recurring false positives, identify legitimate patterns, and use thresholds, exclusions, allowlists or additional conditions to improve the rule.

42\. How do you reduce false positives?
=======================================

**Answer:**

> I analyze why the alert is triggering, identify legitimate activity, and then improve the detection using additional context, thresholds, allowlists, correlation and time windows. I avoid simply disabling the rule because that can create a detection gap.

43\. What is detection engineering?
===================================

**Answer:**

> Detection engineering is the process of designing, implementing, testing, tuning and maintaining security detections. It includes understanding attacker behavior, identifying telemetry requirements, writing detection logic, mapping it to MITRE ATT&CK and continuously improving its accuracy.

44\. What is threat detection content?
======================================

**Answer:**

> Threat detection content includes rules, queries, correlations, alerts, dashboards and other logic used to identify suspicious behavior.

Examples:

*   Sigma rules
    
*   Chronicle rules
    
*   Splunk detections
    
*   YARA rules
    
*   Correlation rules
    
*   Detection queries
    

45\. How would you create a VPN detection?
==========================================

**Answer:**

> I would analyze VPN authentication logs for unusual login locations, impossible travel, abnormal login times, multiple failed attempts followed by success, unusual devices and excessive concurrent sessions. I would correlate VPN events with identity and endpoint telemetry to increase confidence.

46\. How would you create a firewall detection?
===============================================

**Answer:**

> I would identify behaviors such as repeated blocked connections, scanning patterns, connections to known malicious IPs, unusual outbound traffic and suspicious ports. I would correlate firewall events with threat intelligence and endpoint activity to distinguish real threats from normal network activity.

47\. How would you create a DLP detection?
==========================================

**Answer:**

> I would look for sensitive-data transfers involving unusual users, destinations, file types, volumes or applications. I would correlate DLP events with identity, endpoint and network activity and use thresholds and user context to reduce false positives.

48\. What is an Incident Response Guide?
========================================

**Answer:**

> An Incident Response Guide is a documented procedure that tells analysts how to investigate and respond to a particular security incident. It typically contains detection criteria, investigation steps, evidence to collect, containment actions, escalation criteria and recovery steps.

49\. Playbook vs Incident Response Guide?
=========================================

PlaybookIR GuideAutomated workflowHuman-readable procedureExecutes actionsGuides analystsUses integrations/APIsContains investigation instructionsAutomation-focusedProcess-focused

> Ideally, the IR guide and SOAR playbook should complement each other.

50\. What is ELK?
=================

**Answer:**

> ELK stands for Elasticsearch, Logstash and Kibana. Elasticsearch stores and searches data, Logstash processes and forwards logs, and Kibana provides visualization and dashboards.

51\. Elasticsearch vs Kibana?
=============================

**Answer:**

> Elasticsearch is the search and analytics engine used to store and query data, while Kibana is the visualization and investigation interface used to search, build dashboards and analyze that data.

52\. What is CrowdStrike and how can it work with SOAR?
=======================================================

**Answer:**

> CrowdStrike provides endpoint security and EDR capabilities. SOAR can integrate with CrowdStrike to retrieve endpoint information, investigate detections, query processes and perform response actions such as isolating an endpoint, depending on the integration and permissions.

53\. How would you handle a CrowdStrike malware alert?
======================================================

**Answer:**

Plain textANTLR4BashCC#CSSCoffeeScriptCMakeDartDjangoDockerEJSErlangGitGoGraphQLGroovyHTMLJavaJavaScriptJSONJSXKotlinLaTeXLessLuaMakefileMarkdownMATLABMarkupObjective-CPerlPHPPowerShell.propertiesProtocol BuffersPythonRRubySass (Sass)Sass (Scss)SchemeSQLShellSwiftSVGTSXTypeScriptWebAssemblyYAMLXML`   CrowdStrike Alert        ↓  Get host/user details        ↓  Retrieve detection information        ↓  Check file hash / IOC reputation        ↓  Correlate SIEM events        ↓  Determine severity        ↓  Isolate endpoint if required        ↓  Create/update incident        ↓  Notify SOC   `

54\. What is the difference between IOC and IOA?
================================================

**Answer:**

> An IOC, or Indicator of Compromise, is evidence associated with malicious activity, such as a malicious IP, domain, hash or URL. An IOA, or Indicator of Attack, focuses more on attacker behavior, such as credential dumping, suspicious PowerShell execution or lateral movement.

55\. IOC vs TTP?
================

**Answer:**

IOCTTPSpecific indicatorAttacker behaviorIP/domain/hashTechnique/tacticCan change quicklyUsually more persistentExample: malicious IPExample: Credential Dumping

56\. What is a security control?
================================

**Answer:**

> A security control is a measure implemented to prevent, detect or respond to security threats.

Examples:

*   MFA
    
*   EDR
    
*   Firewall
    
*   DLP
    
*   SIEM
    
*   SOAR
    
*   Network segmentation
    
*   Access control
    

57\. How do you identify security control gaps?
===============================================

**Answer:**

> I compare the organization's current detection and prevention capabilities against known threats and attack techniques. I look for areas where telemetry, detection, response or preventive controls are missing and then propose improvements based on risk and business impact.

58.0\. what are detection rules??
======================================

**Answer:**

> Detection rules are the logical conditions and behavioral thresholds configured within security platforms (like a SIEM or EDR) to identify malicious activity, anomalies, or policy violations. They act as the primary tripwires in a security environment.

These rules continuously analyze incoming telemetry—such as system logs, network traffic, and authentication events—looking for specific patterns. They typically fall into a few core categories:

- Signature-based: Looking for known bad indicators, like a specific malware hash or a connection to a recognized command-and-control (C2) IP address.

- Behavioral/Anomaly-based: Detecting deviations from normal baselines, such as an "impossible travel" scenario or a sudden, unexplained spike in Active Directory privilege escalation attempts.

- TTP-based: Targeting specific adversary techniques mapped to frameworks like MITRE ATT&CK, such as the execution of a base64-encoded PowerShell payload.

> When the incoming data matches the logic of a detection rule, it generates an alert. That alert is what ultimately escalates to an analyst's queue or triggers an automated SOAR playbook for immediate enrichment, containment, and triage.

58\. How do you test a detection rule?
======================================

**Answer:**

> I test it using historical events, simulated events or controlled attack scenarios. I verify that the rule triggers under the expected conditions, does not trigger excessively on legitimate activity, extracts the correct fields and produces the expected alert severity and metadata.

59\. What is detection validation?
==================================

**Answer:**

> Detection validation confirms that a detection actually identifies the intended behavior and generates the expected alert. I validate the input telemetry, rule logic, output fields, severity, MITRE mapping and downstream SOAR workflow.

60\. What is a false positive and false negative?
=================================================

**Answer:**

> A false positive occurs when a legitimate activity is incorrectly detected as malicious. A false negative occurs when malicious activity is not detected.

Plain textANTLR4BashCC#CSSCoffeeScriptCMakeDartDjangoDockerEJSErlangGitGoGraphQLGroovyHTMLJavaJavaScriptJSONJSXKotlinLaTeXLessLuaMakefileMarkdownMATLABMarkupObjective-CPerlPHPPowerShell.propertiesProtocol BuffersPythonRRubySass (Sass)Sass (Scss)SchemeSQLShellSwiftSVGTSXTypeScriptWebAssemblyYAMLXML`   False Positive → Alert but no real threat  False Negative → Real threat but no alert   `

61\. Which is more dangerous: false positive or false negative?
===============================================================

**Answer:**

> Generally, false negatives can be more dangerous because an actual attack may go undetected. However, excessive false positives are also dangerous because alert fatigue can cause analysts to miss genuine threats.

62\. How do you prioritize alerts?
==================================

**Answer:**

> I consider severity, confidence, affected assets, user privilege, threat intelligence reputation, attack stage and business impact. A confirmed compromise of a critical asset would receive much higher priority than a low-confidence suspicious event.

63\. What is alert fatigue?
===========================

**Answer:**

> Alert fatigue happens when analysts receive too many alerts, especially repetitive or low-quality alerts, causing them to become desensitized and potentially miss important threats. Detection tuning, correlation, grouping and SOAR automation help reduce it.

64\. What is the role of Python in SOAR?
========================================

**Answer:**

> Python is commonly used to build custom integrations, automation scripts, API clients, enrichment logic, parsers and data-processing workflows. I use Python along with REST APIs to automate security operations and connect systems that don't have an out-of-the-box integration.

65\. How would you build a custom security integration?
=======================================================

**Answer:**

Plain textANTLR4BashCC#CSSCoffeeScriptCMakeDartDjangoDockerEJSErlangGitGoGraphQLGroovyHTMLJavaJavaScriptJSONJSXKotlinLaTeXLessLuaMakefileMarkdownMATLABMarkupObjective-CPerlPHPPowerShell.propertiesProtocol BuffersPythonRRubySass (Sass)Sass (Scss)SchemeSQLShellSwiftSVGTSXTypeScriptWebAssemblyYAMLXML`   Understand API       ↓  Authentication       ↓  Implement API client       ↓  Define inputs/outputs       ↓  Error handling       ↓  Logging       ↓  Testing       ↓  Deploy       ↓  Integrate with Playbook   `

66\. REST API experience in SOAR?
=================================

**Answer:**

> I have worked with REST APIs for security integrations and automation. Typically I handle authentication, request construction, response parsing, error handling, retries and asynchronous operations, and then expose the required functionality to the SOAR workflow.

67\. What HTTP methods do you commonly use?
===========================================

**Answer:**

Plain textANTLR4BashCC#CSSCoffeeScriptCMakeDartDjangoDockerEJSErlangGitGoGraphQLGroovyHTMLJavaJavaScriptJSONJSXKotlinLaTeXLessLuaMakefileMarkdownMATLABMarkupObjective-CPerlPHPPowerShell.propertiesProtocol BuffersPythonRRubySass (Sass)Sass (Scss)SchemeSQLShellSwiftSVGTSXTypeScriptWebAssemblyYAMLXML`   GET     → Retrieve data  POST    → Create/execute an operation  PUT     → Update/replace data  PATCH   → Partially update data  DELETE  → Delete data   `

68\. How do you troubleshoot a failed API integration?
======================================================

**Answer:**

> I first verify the endpoint, authentication and permissions. Then I inspect the request payload, headers, HTTP status code and response body. I reproduce the request using Postman or curl, check logs and API documentation, and determine whether the issue is authentication, payload, permissions, network connectivity or the remote service.

69\. What HTTP status codes are important?
==========================================

CodeMeaning200Success201Created400Bad request401Unauthorized403Forbidden404Not found429Rate limited500Server error502/503Gateway/service unavailable

70\. How do you handle API rate limits?
=======================================

**Answer:**

> I detect HTTP 429 responses, respect the API's retry information when available, use exponential backoff and avoid unnecessary API calls. For high-volume workflows, I also use caching, batching or asynchronous processing where appropriate.

71\. What is asynchronous processing and why is it useful in SOAR?
==================================================================

**Answer:**

> Some security operations take time, such as scanning an endpoint or waiting for an external analysis service. Asynchronous processing allows the workflow to continue without blocking the entire system and then process the result when it becomes available.

72\. How would you troubleshoot a SOAR playbook that is not executing?
======================================================================

**Answer:**

> I would check whether the trigger condition is being satisfied, verify the incident inputs, inspect each playbook task, validate integration connectivity and permissions, and review execution logs. I would also test individual commands separately to isolate whether the issue is in the trigger, playbook logic or integration.

73\. How do you monitor SOAR playbooks?
=======================================

**Answer:**

> I monitor execution success/failure rates, API errors, execution duration, skipped tasks, failed integrations and response actions. I also maintain logging and audit trails so that every automated action can be traced.

74\. How would you design a production-grade SOAR playbook?
===========================================================

**Answer:**

> I would make it modular, idempotent and fault tolerant. I would include input validation, conditional logic, retries, timeouts, exception handling, logging, approval gates for risky actions and clear escalation paths. I would also ensure every automated action is auditable.

75\. What does idempotent mean in SOAR?
=======================================

**Answer:**

> An idempotent action produces the same desired result even if it is executed more than once.

Example:

> If an IP is already blocked, running the block action again should not create an inconsistent state or unnecessary failure.

76\. What is the difference between orchestration and automation?
=================================================================

**Answer:**

> Automation means performing a task automatically, while orchestration means coordinating multiple automated tasks and tools as one workflow.

Example:

Plain textANTLR4BashCC#CSSCoffeeScriptCMakeDartDjangoDockerEJSErlangGitGoGraphQLGroovyHTMLJavaJavaScriptJSONJSXKotlinLaTeXLessLuaMakefileMarkdownMATLABMarkupObjective-CPerlPHPPowerShell.propertiesProtocol BuffersPythonRRubySass (Sass)Sass (Scss)SchemeSQLShellSwiftSVGTSXTypeScriptWebAssemblyYAMLXML`   Automation:  Block IP  Orchestration:  Get IOC   → Enrich IOC   → Check endpoint   → Block IP   → Create ticket   → Notify SOC   `

77\. How would you explain your experience relevant to this Tecplix JD?
=======================================================================

**Answer:**

> My current experience aligns closely with this role because I already work across SIEM/SOAR environments involving Google Security Operations, Splunk, Elastic, CrowdStrike, Splunk SOAR and Cortex XSOAR. I have worked on ingestion, parsing, normalization, detection content, alert investigation, threat enrichment and SOAR automation. I also have hands-on experience with Python, APIs and security integrations, which maps well to the integration and playbook requirements in this JD.

78\. You have worked with Chronicle, so how would you create a Chronicle detection?
===================================================================================

**Answer:**

> I would first identify the relevant UDM fields and understand the behavior I want to detect. Then I would write the detection logic, test it against available telemetry, validate the expected matches and tune false positives. After validation, I would deploy it and monitor its performance.

79\. What would you do if the required field isn't available in Chronicle?
==========================================================================

**Answer:**

> I would first verify whether the raw log contains that information. If it does, I would investigate the parser or normalization mapping and modify it so the field is correctly represented in UDM. If the raw data doesn't contain it, I would identify another available field or determine whether the source needs to be enhanced.

80\. How do you approach a new log-source onboarding?
=====================================================

**Answer:**

Plain textANTLR4BashCC#CSSCoffeeScriptCMakeDartDjangoDockerEJSErlangGitGoGraphQLGroovyHTMLJavaJavaScriptJSONJSXKotlinLaTeXLessLuaMakefileMarkdownMATLABMarkupObjective-CPerlPHPPowerShell.propertiesProtocol BuffersPythonRRubySass (Sass)Sass (Scss)SchemeSQLShellSwiftSVGTSXTypeScriptWebAssemblyYAMLXML`   Understand source        ↓  Identify required events/fields        ↓  Configure ingestion        ↓  Validate raw logs        ↓  Create/modify parser        ↓  Normalize fields        ↓  Validate search        ↓  Create detections        ↓  Test        ↓  Production monitoring   `

81\. How would you onboard a firewall into SIEM?
================================================

**Answer:**

> I would identify the firewall's supported log transport such as Syslog or API, configure the source and ingestion pipeline, validate raw events, create or validate the parser, normalize fields, and verify that important fields like source IP, destination IP, port and action are available. Then I would create relevant detections and test the end-to-end flow.

82\. What security logs are important from a firewall?
======================================================

**Answer:**

*   Allowed connections
    
*   Blocked connections
    
*   Threat events
    
*   VPN activity
    
*   NAT activity
    
*   Port scanning
    
*   Malware detections
    
*   Suspicious outbound traffic
    
*   Administrative changes
    

83\. What security logs are important from a VPN?
=================================================

**Answer:**

*   Login/logout
    
*   Failed authentication
    
*   Successful authentication
    
*   Source IP
    
*   Username
    
*   Geolocation
    
*   Device information
    
*   Session duration
    
*   Concurrent sessions
    
*   Authentication method
    

84\. What security logs are important from DLP?
===============================================

**Answer:**

*   Sensitive-data access
    
*   File transfers
    
*   Uploads
    
*   Downloads
    
*   External sharing
    
*   USB activity
    
*   Policy violations
    
*   User identity
    
*   Destination
    
*   Data classification
    

85\. How would you investigate a suspicious login?
==================================================

**Answer:**

> I would first identify the user, source IP, location and authentication method. Then I would check previous login history, failed attempts, device information, VPN activity and endpoint telemetry. I would enrich the IP and correlate other events to determine whether the login is legitimate or potentially compromised.

86\. How would you investigate a compromised user account?
==========================================================

**Answer:**

Plain textANTLR4BashCC#CSSCoffeeScriptCMakeDartDjangoDockerEJSErlangGitGoGraphQLGroovyHTMLJavaJavaScriptJSONJSXKotlinLaTeXLessLuaMakefileMarkdownMATLABMarkupObjective-CPerlPHPPowerShell.propertiesProtocol BuffersPythonRRubySass (Sass)Sass (Scss)SchemeSQLShellSwiftSVGTSXTypeScriptWebAssemblyYAMLXML`   Identify user   ↓  Check authentication history   ↓  Check source IP/location   ↓  Check MFA activity   ↓  Check endpoint activity   ↓  Check privilege changes   ↓  Check email/cloud activity   ↓  Threat intelligence enrichment   ↓  Contain account if confirmed   `

87\. What would you do when an endpoint is compromised?
=======================================================

**Answer:**

> I would validate the detection and determine the scope of compromise. I would investigate the endpoint, user, processes, network connections and indicators. If confirmed, I would isolate the endpoint through EDR, contain affected accounts or indicators where necessary, collect evidence and escalate according to the incident-response process.

88\. What is your approach to incident response?
================================================

**Answer:**

Plain textANTLR4BashCC#CSSCoffeeScriptCMakeDartDjangoDockerEJSErlangGitGoGraphQLGroovyHTMLJavaJavaScriptJSONJSXKotlinLaTeXLessLuaMakefileMarkdownMATLABMarkupObjective-CPerlPHPPowerShell.propertiesProtocol BuffersPythonRRubySass (Sass)Sass (Scss)SchemeSQLShellSwiftSVGTSXTypeScriptWebAssemblyYAMLXML`   Preparation     ↓  Detection     ↓  Analysis     ↓  Containment     ↓  Eradication     ↓  Recovery     ↓  Lessons Learned   `

89\. What is the difference between detection and response?
===========================================================

**Answer:**

> Detection is identifying suspicious or malicious activity. Response is the set of actions taken after detection to investigate, contain, eradicate and recover from the incident.

90\. What would you do if a SOAR playbook incorrectly blocked a legitimate IP?
==============================================================================

**Answer:**

> I would immediately investigate and reverse the action if required. Then I would identify why the decision logic allowed the false positive, review the enrichment and confidence criteria, add appropriate safeguards or approval gates, test the corrected workflow and document the incident.

91\. How do you make SOAR automation safe?
==========================================

**Answer:**

> I use validation, confidence thresholds, allowlists, approval gates, least-privilege credentials, rollback mechanisms, audit logging and exception handling. High-impact actions should require stronger confidence than low-risk enrichment actions.

92\. What is least privilege in SOAR?
=====================================

**Answer:**

> SOAR integrations should have only the permissions required for their specific tasks. For example, a threat-intelligence integration may only need read access, while an endpoint integration performing isolation requires a specific response permission.

93\. What is a detection gap?
=============================

**Answer:**

> A detection gap is a security behavior or attack technique for which the organization currently has insufficient telemetry or detection capability.

Example:

> If an organization has endpoint logs but no detection for credential dumping, that could represent a detection gap.

94\. How would you improve SOC processes?
=========================================

**Answer:**

> I would analyze repetitive manual tasks, high-volume alerts, common false positives and investigation bottlenecks. Then I would identify opportunities for better correlation, enrichment, automation and playbooks while maintaining appropriate analyst approval for high-risk actions.

95\. What metrics would you monitor for a SOC/SOAR environment?
===============================================================

**Answer:**

*   Mean Time to Detect — MTTD
    
*   Mean Time to Respond — MTTR
    
*   Alert volume
    
*   False-positive rate
    
*   Automation rate
    
*   Playbook success rate
    
*   Escalation rate
    
*   Detection coverage
    
*   Incident resolution time
    

96\. What is MTTD and MTTR?
===========================

**Answer:**

> MTTD is Mean Time to Detect — how long it takes to identify a security incident. MTTR is Mean Time to Respond/Recover — how long it takes to respond to and resolve the incident.

97\. How would you improve a noisy SIEM rule?
=============================================

**Answer:**

> I would analyze historical alerts and identify the common legitimate patterns. Then I would add contextual conditions, thresholds, correlation, allowlists or asset/user-based filtering. After testing the modified rule, I would compare the false-positive rate and detection coverage before deploying it.

98\. How do you prioritize detection engineering work?
======================================================

**Answer:**

> I prioritize based on business risk, threat prevalence, asset criticality, attack likelihood, MITRE ATT&CK coverage gaps and available telemetry. High-impact threats affecting critical systems receive higher priority.

99\. What is a detection-as-code approach?
==========================================

**Answer:**

> Detection-as-code means treating detection rules like software. Rules are version-controlled, reviewed, tested and deployed through controlled processes rather than being manually modified directly in production.

100\. How would you version-control detection rules?
====================================================

**Answer:**

Plain textANTLR4BashCC#CSSCoffeeScriptCMakeDartDjangoDockerEJSErlangGitGoGraphQLGroovyHTMLJavaJavaScriptJSONJSXKotlinLaTeXLessLuaMakefileMarkdownMATLABMarkupObjective-CPerlPHPPowerShell.propertiesProtocol BuffersPythonRRubySass (Sass)Sass (Scss)SchemeSQLShellSwiftSVGTSXTypeScriptWebAssemblyYAMLXML`   Detection Rule       ↓  Git Repository       ↓  Code Review       ↓  Testing       ↓  Validation       ↓  Deployment       ↓  Monitoring   `

101\. What is the difference between prevention, detection and response?
========================================================================

StageExamplePreventionFirewall blocks malicious trafficDetectionSIEM generates an alertResponseSOAR isolates endpoint

**Simple interview answer:**

> Prevention tries to stop the attack, detection identifies it, and response contains and resolves it.

102\. Scenario: You receive a high-severity malware alert. What will you do?
============================================================================

**Answer:**

> I would validate the alert and identify the affected endpoint and user. I would investigate the malware hash, process tree, network connections and related SIEM events, then enrich the indicators using threat intelligence. If confirmed, I would isolate the endpoint through EDR, contain related indicators, create or update the incident and escalate according to the IR process.

103\. Scenario: A user logs in from India and the US within 10 minutes.
=======================================================================

**Answer:**

> I would treat it as a potential impossible-travel alert. I would verify both authentication events, source IP reputation, VPN usage, device information and historical user behavior. If the activity is suspicious, I would investigate for account compromise and potentially trigger account containment.

104\. Scenario: A detection suddenly generates 10,000 alerts.
=============================================================

**Answer:**

> I would first determine whether the increase is caused by a real security event or a detection/data issue. I would check recent rule changes, parser changes, ingestion anomalies and false-positive patterns. If necessary, I would temporarily tune or disable the problematic condition under change control while investigating the root cause.

105\. Scenario: SOAR integration API suddenly starts returning 401.
===================================================================

**Answer:**

> A 401 indicates an authentication issue. I would verify the API credentials/token, expiration, permissions and integration configuration. I would reproduce the request using Postman or curl and check whether the API authentication requirements changed. After fixing the credentials, I would test the integration before re-enabling automated response.

106\. Scenario: API returns 429.
================================

**Answer:**

> 429 indicates rate limiting. I would reduce request frequency, implement retry logic with exponential backoff and respect the API's retry-after information. I would also look for opportunities to batch or cache requests.

107\. Scenario: A SOAR playbook is partially successful.
========================================================

**Answer:**

> I would identify exactly which task failed and whether previous actions were already completed. I would prevent duplicate actions, retry only safe operations and route the incident to manual investigation if necessary. After recovery, I would investigate the root cause and improve the playbook's error handling.

108\. Scenario: You have a malicious IP but threat intelligence says "unknown."
===============================================================================

**Answer:**

> I would not automatically block it solely because it is unknown. I would correlate it with firewall, proxy, DNS, endpoint and authentication activity and investigate its behavior. Based on the combined evidence and confidence level, I would either escalate it, monitor it or perform containment.

109\. What would you say if they ask about Sumo Logic and you have less hands-on experience?
============================================================================================

**Answer:**

> My strongest hands-on experience is with Google Security Operations, Splunk, Microsoft Sentinel, Elastic and SOAR platforms. I understand the core SIEM concepts such as ingestion, parsing, normalization, detection, correlation and alerting, so I can transfer those concepts to Sumo Logic. I would be comfortable ramping up quickly on the platform-specific syntax and workflows.

**Important:** Don't claim deep Sumo Logic experience if you haven't actually used it.

110\. What would you say if they ask about YARA and your experience is limited?
===============================================================================

**Answer:**

> I understand YARA as a rule-based pattern-matching framework used primarily for malware identification and threat hunting. My stronger experience is around SIEM detection engineering, log analysis and SOAR automation, but I understand how YARA fits into the broader detection pipeline and can work with existing rules and develop them as required.

111\. What would you say if they ask about Palo Alto?
=====================================================

**Answer:**

> I understand Palo Alto from the SOAR integration and response perspective, particularly using APIs or integrations to retrieve security information and perform actions such as blocking indicators. My main strength is the automation layer—integrating the security product into investigation and response workflows.

112\. Why do you want to join Tecplix?
======================================

**Answer:**

> Tecplix is particularly interesting to me because the role is closely aligned with my current SIEM/SOAR experience, especially Google Security Operations, detection engineering, SOAR playbooks and security integrations. The opportunity to work deeply with Chronicle, detection content, threat hunting and security automation would allow me to build further expertise in the areas I am already pursuing.

113\. Why should we hire you?
=============================

**Answer:**

> I bring a combination of software engineering and security operations experience. I have around 3 years of experience working with SIEM/SOAR technologies, security integrations, log pipelines, detection content and automation. Because I also have development experience with Python, JavaScript/Node.js and APIs, I can not only operate security tools but also build and troubleshoot the integrations and automation behind them.

114\. Why are you looking for a change?
=======================================

**Answer:**

> I'm looking for a role where I can go deeper into SIEM/SOAR engineering, detection engineering and security automation. I want to work on larger-scale security operations environments and strengthen my expertise in areas such as Google Security Operations, threat detection, SOAR and incident response.

115\. What are your strongest areas for this role?
==================================================

**Answer:**

> My strongest areas are SIEM/SOAR integration, detection engineering, log ingestion and parsing, alert investigation, threat enrichment, API-based automation and SOAR playbooks. I also have a strong software-development background, which helps me build custom integrations and troubleshoot technical issues quickly.

116\. What are the most important topics to prepare for this specific JD?
=========================================================================

Priority 1 — Must Know
----------------------

Plain textANTLR4BashCC#CSSCoffeeScriptCMakeDartDjangoDockerEJSErlangGitGoGraphQLGroovyHTMLJavaJavaScriptJSONJSXKotlinLaTeXLessLuaMakefileMarkdownMATLABMarkupObjective-CPerlPHPPowerShell.propertiesProtocol BuffersPythonRRubySass (Sass)Sass (Scss)SchemeSQLShellSwiftSVGTSXTypeScriptWebAssemblyYAMLXML`   Google Chronicle / Google SecOps  SIEM vs SOAR  Detection Engineering  SIEM Use Cases  Correlation Rules  Log Ingestion  Parsing & Normalization  SOAR Playbooks  Cortex XSOAR / Demisto  MITRE ATT&CK  Sigma  YARA  Threat Intelligence  Incident Response  Alert Triage  False Positive Tuning  REST APIs  Python Automation   `

Priority 2 — Very Likely
------------------------

Plain textANTLR4BashCC#CSSCoffeeScriptCMakeDartDjangoDockerEJSErlangGitGoGraphQLGroovyHTMLJavaJavaScriptJSONJSXKotlinLaTeXLessLuaMakefileMarkdownMATLABMarkupObjective-CPerlPHPPowerShell.propertiesProtocol BuffersPythonRRubySass (Sass)Sass (Scss)SchemeSQLShellSwiftSVGTSXTypeScriptWebAssemblyYAMLXML`   CrowdStrike  Palo Alto  ELK  Splunk  Sumo Logic  VPN Detection  Firewall Detection  DLP Detection  Endpoint Integration  Threat Hunting  Incident Response Guides  Security Control Gaps  IOC / IOA / TTP   `

Priority 3 — Scenario-Based
---------------------------

Plain textANTLR4BashCC#CSSCoffeeScriptCMakeDartDjangoDockerEJSErlangGitGoGraphQLGroovyHTMLJavaJavaScriptJSONJSXKotlinLaTeXLessLuaMakefileMarkdownMATLABMarkupObjective-CPerlPHPPowerShell.propertiesProtocol BuffersPythonRRubySass (Sass)Sass (Scss)SchemeSQLShellSwiftSVGTSXTypeScriptWebAssemblyYAMLXML`   Malware Alert  Brute Force  Impossible Travel  Compromised Account  Malicious IP  Endpoint Compromise  10,000 Alert Spike  Failed API Integration  401 / 403 / 429 API errors  Failed SOAR Playbook  False Positive Detection  Missing SIEM Fields  Broken Parser   `

117\. The most important interview flow to memorize
===================================================

Plain textANTLR4BashCC#CSSCoffeeScriptCMakeDartDjangoDockerEJSErlangGitGoGraphQLGroovyHTMLJavaJavaScriptJSONJSXKotlinLaTeXLessLuaMakefileMarkdownMATLABMarkupObjective-CPerlPHPPowerShell.propertiesProtocol BuffersPythonRRubySass (Sass)Sass (Scss)SchemeSQLShellSwiftSVGTSXTypeScriptWebAssemblyYAMLXML`   LOG SOURCE      ↓  INGESTION      ↓  PARSING      ↓  NORMALIZATION      ↓  SIEM      ↓  CORRELATION / DETECTION      ↓  ALERT      ↓  SOAR      ↓  ENRICHMENT      ↓  INVESTIGATION      ↓  DECISION      ↓  CONTAINMENT / RESPONSE      ↓  TICKET + NOTIFICATION      ↓  DOCUMENTATION   `

One-line explanation
--------------------

> **SIEM detects the threat, SOAR investigates and orchestrates the response, and security integrations provide the actions required to contain it.**

118\. Best 30-second answer for "What exactly do you do in your current role?"
==============================================================================

> I work as a SIEM/SOAR Engineer where I handle security log ingestion, parsing, normalization, detection content and alert investigation across platforms such as Google Security Operations, Splunk, Sentinel and Elastic. On the SOAR side, I work with Splunk SOAR and Cortex XSOAR to build automation workflows and integrate security products through REST APIs. I also use Python and JavaScript/Node.js for custom security integrations and automation.

119\. Best answer for "Why are you a good fit for this JD?"
===========================================================

> This JD closely matches my current SIEM/SOAR work. I already have experience with Google Security Operations, Splunk, Elastic, CrowdStrike, Cortex XSOAR and Splunk SOAR, along with detection engineering, log parsing, normalization, threat enrichment and playbook automation. My software-development background in Python, Node.js and REST APIs also helps me build and troubleshoot custom security integrations.

120\. Final preparation strategy
================================

Before the interview, be able to explain these without hesitation:
------------------------------------------------------------------

### SIEM

Plain textANTLR4BashCC#CSSCoffeeScriptCMakeDartDjangoDockerEJSErlangGitGoGraphQLGroovyHTMLJavaJavaScriptJSONJSXKotlinLaTeXLessLuaMakefileMarkdownMATLABMarkupObjective-CPerlPHPPowerShell.propertiesProtocol BuffersPythonRRubySass (Sass)Sass (Scss)SchemeSQLShellSwiftSVGTSXTypeScriptWebAssemblyYAMLXML`   Ingestion  → Parsing  → Normalization  → Correlation  → Detection  → Alert   `

### SOAR

Plain textANTLR4BashCC#CSSCoffeeScriptCMakeDartDjangoDockerEJSErlangGitGoGraphQLGroovyHTMLJavaJavaScriptJSONJSXKotlinLaTeXLessLuaMakefileMarkdownMATLABMarkupObjective-CPerlPHPPowerShell.propertiesProtocol BuffersPythonRRubySass (Sass)Sass (Scss)SchemeSQLShellSwiftSVGTSXTypeScriptWebAssemblyYAMLXML`   Alert  → Enrichment  → Investigation  → Decision  → Automated Response  → Ticket  → Notification   `

### Detection Engineering

Plain textANTLR4BashCC#CSSCoffeeScriptCMakeDartDjangoDockerEJSErlangGitGoGraphQLGroovyHTMLJavaJavaScriptJSONJSXKotlinLaTeXLessLuaMakefileMarkdownMATLABMarkupObjective-CPerlPHPPowerShell.propertiesProtocol BuffersPythonRRubySass (Sass)Sass (Scss)SchemeSQLShellSwiftSVGTSXTypeScriptWebAssemblyYAMLXML`   Threat  → Required Telemetry  → Detection Logic  → Testing  → Tuning  → MITRE Mapping  → Deployment  → Monitoring   `

### SOAR Engineering

Plain textANTLR4BashCC#CSSCoffeeScriptCMakeDartDjangoDockerEJSErlangGitGoGraphQLGroovyHTMLJavaJavaScriptJSONJSXKotlinLaTeXLessLuaMakefileMarkdownMATLABMarkupObjective-CPerlPHPPowerShell.propertiesProtocol BuffersPythonRRubySass (Sass)Sass (Scss)SchemeSQLShellSwiftSVGTSXTypeScriptWebAssemblyYAMLXML`   Trigger  → Extract Data  → Integrate APIs  → Enrich  → Decision Logic  → Response  → Error Handling  → Logging   `

### Your strongest positioning

> **"I am a software engineer who moved deeply into SIEM/SOAR engineering, so I understand both the security operations side and the engineering side required to build reliable integrations, detections and automation."**