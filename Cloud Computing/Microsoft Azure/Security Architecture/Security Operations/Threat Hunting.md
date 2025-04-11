# Threat hunting in Sentinel

The hunting dashboard provides ready-made query examples designed to get you started and get you familiar with the tables and the query language. Queries run on data stored in log tables, such as for process creation, DNS events, or other event types.

Built-in hunting queries are developed by Microsoft security researchers on a continuous basis, both adding new queries and fine-tuning existing queries to provide you with an entry point to look for new detections and figure out where to start hunting for the beginnings of new attacks.

Use queries before, during, and after a compromise to take the following actions:

1) Before an incident occurs: Waiting on detections is not enough. Take proactive action by running any threat-hunting queries related to the data you're ingesting into your workspace at least once a week.

Results from your proactive hunting provide early insight into events that may confirm that a compromise is in process, or will at least show weaker areas in your environment that are at risk and need attention.

2) During a compromise: Use livestream to run a specific query constantly, presenting results as they come in. Use livestream when you need to actively monitor user events, such as if you need to verify whether a specific compromise is still taking place, to help determine a threat actor's next action, and towards the end of an investigation to confirm that the compromise is indeed over.

3) After a compromise: After a compromise or an incident has occurred, make sure to improve your coverage and insight to prevent similar incidents in the future.

Modify your existing queries or create new ones to assist with early detection, based on insights you've gained from your compromise or incident.

If you've discovered or created a hunting query that provides high value insights into possible attacks, create custom detection rules based on that query and surface those insights as alerts to your security incident responders.

View the query's results, and select New alert rule > Create Microsoft Sentinel alert. Use the Analytics rule wizard to create a new rule based on your query. For more information, see Create custom analytics rules to detect threats.

You can also create hunting and livestream queries over data stored in Azure Data Explorer. For more information, see details of constructing cross-resource queries in the Azure Monitor documentation.

Use community resources, such as the Microsoft Sentinel GitHub repository to find additional queries and data sources.
