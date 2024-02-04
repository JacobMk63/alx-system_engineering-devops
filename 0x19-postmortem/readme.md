
#Postmortem: Internal Search Outage Due to Monitoring Blindspot
##Issue Summary:
Duration: 45 minutes (PST) - Start: 2024-01-26 10:15, End: 2024-01-26 11:00
Impact: The internal search functionality for our company's knowledge base and project management platform was unavailable for all users. This prevented employees from effectively finding information and accessing critical resources, impacting productivity across multiple departments. Approximately 80% of internal users attempted to use the search function during the outage window.
Root Cause: A recent update to the search engine software introduced a memory leak, exceeding the allocated memory on the server hosting the search index. This caused the server to crash, leading to the complete unavailability of the search function.
#Timeline:
10:15: User reports start trickling in regarding issues with the internal search function.
10:20: Monitoring system fails to detect any anomalies, as memory usage metrics were not being tracked for the specific server hosting the search index.
10:30: Engineers investigate user reports and confirm the search function is down. Initial suspicion falls on network connectivity issues.
10:45: Network troubleshooting reveals no problems. Investigation shifts to application logs on the search server, but initial scans show nothing conclusive.
10:50: The incident escalated to the senior development team for further investigation.
10:55: By manually inspecting memory usage on the search server, the memory leak is identified.
11:00: A hotfix is deployed to the search engine software, temporarily disabling the problematic indexing process. Search functionality is restored.
11:15: Post-incident analysis begins, focusing on improving monitoring and preventing future memory leaks.
#Root Cause and Resolution:
The root cause of the outage was a memory leak introduced in a recent update to the search engine software. This leak caused the server hosting the search index to gradually deplete its allocated memory, eventually leading to a crash and service unavailability. The issue was resolved by deploying a hotfix that temporarily disabled the problematic indexing process and freed up memory on the server.
Corrective and Preventative Measures:
Enhance monitoring: Implement comprehensive monitoring for all servers, including memory usage metrics for the search server. Set up alerts for critical resource utilization thresholds to trigger early warnings and prevent future outages.
Proactive code review: Establish stricter code review procedures for future software updates, particularly focusing on resource management and potential memory leaks.
Invest in load testing: Regularly conduct load testing of the search functionality to identify performance bottlenecks and resource limitations before they impact production.
Update search software: Explore upgrading the search engine software to a more stable and resource-efficient version.
Consider redundancy: Evaluate the feasibility of implementing a redundant search server setup to provide failover capabilities in case of future issues.


