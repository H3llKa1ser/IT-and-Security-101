# Threat intelligence in Microsoft Sentinel

Cyber threat intelligence (CTI) is information describing existing or potential threats to systems and users. This intelligence takes many forms, from written reports detailing a particular threat actor's motivations, infrastructure, and techniques, to specific observations of IP addresses, domains, file hashes, and other artifacts associated with known cyber threats. CTI is used by organizations to provide essential context to unusual activity, so security personnel can quickly take action to protect their people, information, and assets. CTI can be sourced from many places, such as open-source data feeds, threat intelligence-sharing communities, commercial intelligence feeds, and local intelligence gathered in the course of security investigations within an organization.

For SIEM solutions like Microsoft Sentinel, the most common forms of CTI are threat indicators, also known as Indicators of Compromise (IoC) or Indicators of Attack (IoA). Threat indicators are data that associate observed artifacts such as URLs, file hashes, or IP addresses with known threat activity such as phishing, botnets, or malware. This form of threat intelligence is often called tactical threat intelligence because it can be applied to security products and automation in large scale to detect potential threats to an organization and protect against them. In Microsoft Sentinel, you can use threat indicators to help detect malicious activity observed in your environment and provide context to security investigators to help inform response decisions.

Integrate threat intelligence (TI) into Microsoft Sentinel through the following activities:

1) Import threat intelligence into Microsoft Sentinel by enabling data connectors to various TI platforms and feeds.

2) View and manage the imported threat intelligence in Logs and in the Threat Intelligence blade of Microsoft Sentinel.

3) Detect threats and generate security alerts and incidents using the built-in Analytics rule templates based on your imported threat intelligence.

4) Visualize key information about your imported threat intelligence in Microsoft Sentinel with the Threat Intelligence workbook.

Microsoft enriches all imported threat intelligence indicators with GeoLocation and WhoIs data, which is displayed together with other indicator details.

Threat Intelligence also provides useful context within other Microsoft Sentinel experiences such as Hunting and Notebooks. For more information, see Jupyter Notebooks in Microsoft Sentinel and Tutorial: Get started with Jupyter notebooks and MSTICPy in Microsoft Sentinel.
