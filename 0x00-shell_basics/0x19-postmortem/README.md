Incident Postmortem: Web Stack Outage on March 10, 2025

Issue Summary

Duration: March 10, 2025, 13:45 UTC - March 10, 2025, 15:30 UTC (1 hour 45 minutes)

Impact: The company’s main web application was intermittently unavailable for 60% of users. Affected users experienced slow load times, failed requests, or timeouts when accessing the platform.

Root Cause: A misconfigured load balancer update caused uneven traffic distribution, overwhelming a subset of backend servers.

Timeline

13:45 UTC - Monitoring alerts detected increased response times and elevated error rates.

13:50 UTC - Engineering team acknowledged the issue; customer support reported user complaints.

14:00 UTC - Initial assumption was a database performance issue; database metrics were analyzed but showed no anomalies.

14:20 UTC - Investigation shifted to the application layer; logs indicated specific backend servers were handling disproportionate traffic.

14:40 UTC - Load balancer configuration changes from earlier in the day were reviewed.

14:55 UTC - A misconfiguration in the load balancer’s weighted distribution was identified as the root cause.

15:10 UTC - Configuration rollback initiated and changes propagated.

15:30 UTC - System fully stabilized, and normal traffic distribution was restored.

Root Cause and Resolution

The incident was caused by an incorrect configuration applied to the load balancer. Earlier in the day, an engineer adjusted the server weight settings to optimize performance. However, an error in the configuration resulted in a subset of backend servers receiving significantly higher traffic loads than intended. This led to resource exhaustion and service degradation.

To resolve the issue, the engineering team rolled back the configuration to the last known good state. Once applied, the traffic distribution returned to normal, and all servers operated within expected capacity.

Corrective and Preventative Measures

Improvements Needed:

Enhance change management practices to prevent untested configuration changes from being applied to production.

Improve monitoring to detect and alert on uneven backend traffic distribution sooner.

Conduct post-change verification to confirm expected behavior after critical infrastructure updates.

Actionable Tasks:

Implement automated validation checks for load balancer configuration changes.

Establish a canary deployment process for infrastructure changes.

Enhance real-time traffic monitoring with alerts for server load imbalances.

Conduct a post-incident review training for engineers to reinforce best practices in system changes.

By taking these measures, we aim to improve resilience and prevent similar incidents in the future.

