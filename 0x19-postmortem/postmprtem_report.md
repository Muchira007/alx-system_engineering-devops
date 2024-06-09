Issue Summary
Duration of the Outage:
Start: June 8, 2024, 14:00 UTC
End: June 8, 2024, 16:30 UTC

Impact:
Our main e-commerce platform was significantly slowed, affecting the shopping experience for users. Approximately 70% of our users experienced delays in page loading, which led to a 25% drop in completed transactions during the outage.

Root Cause:
The root cause was a misconfigured database index, which resulted in severe query performance degradation during peak traffic.

Timeline
14:00 UTC: Issue detected via automated monitoring alerts indicating high database response times.
14:05 UTC: Initial investigation by the on-call engineer focused on the web server performance.
14:15 UTC: Assumption was that a recent deployment caused the issue, leading to a rollback of the latest changes.
14:30 UTC: Rollback completed, but no improvement in performance.
14:40 UTC: Incident escalated to the database team.
15:00 UTC: Database team identified high CPU usage and long-running queries.
15:15 UTC: Analysis of slow queries revealed missing index on the orders table.
15:45 UTC: New index created on the orders table, significantly improving query performance.
16:00 UTC: Monitoring confirmed that database performance returned to normal.
16:30 UTC: All systems fully operational and normal user experience restored.
Root Cause and Resolution
Root Cause:
The performance degradation was caused by a missing index on the orders table in our database. During peak traffic, queries that filtered and sorted orders by customer ID and order date were not efficiently using the available indexes. This resulted in full table scans, high CPU usage, and long response times.

Resolution:
The database team analyzed the slow queries and identified the missing index as the primary issue. A new composite index on the customer_id and order_date columns was created. This improved the efficiency of the queries, reducing CPU usage and query response times. Post index creation, database performance was monitored to ensure stability, confirming that the issue was resolved.

Corrective and Preventative Measures
Improvements/Fixes:

Database Index Monitoring: Implement regular monitoring and auditing of database indexes to ensure all necessary indexes are in place and optimized.
Performance Testing: Enhance pre-deployment performance testing to simulate peak traffic conditions and identify potential performance bottlenecks.
Alert Thresholds: Fine-tune monitoring alert thresholds for quicker detection of performance degradation.
Tasks to Address the Issue:

Audit Existing Indexes:

Conduct a comprehensive audit of all database tables to ensure proper indexing.
Task owner: Database Team Lead
Deadline: June 20, 2024
Automate Index Monitoring:

Develop scripts to automatically monitor and report on index usage and performance.
Task owner: DevOps Engineer
Deadline: June 25, 2024
Update Performance Testing Suite:

Integrate more rigorous performance testing scenarios into the CI/CD pipeline.
Task owner: QA Team Lead
Deadline: June 30, 2024
Revise Alert Configuration:

Review and adjust alert thresholds to improve the speed and accuracy of issue detection.
Task owner: Monitoring Specialist
Deadline: June 18, 2024
By addressing these measures, we aim to prevent similar incidents in the future and enhance the overall robustness of our e-commerce platform.






