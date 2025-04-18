# Network Monitoring

## Plan for traffic inspection

Knowing what goes in and out of your network is essential to maintaining your security posture. You should capture all inbound and outbound traffic and perform near real-time analysis on that traffic to detect threats and mitigate network vulnerabilities.

This section explores key considerations and recommended approaches for capturing and analyzing traffic within an Azure virtual network.

## Design considerations

Azure VPN Gateway - VPN Gateway lets you run a packet capture on a VPN gateway, a specific connection, multiple tunnels, one-way traffic, or bi-directional traffic. A maximum of five packet captures can run in parallel per gateway. They can be gateway-wide and per-connection packet captures. For more information, see VPN packet capture.

Azure Network Watcher has multiple tools you should consider if you're using infrastructure-as-a-service (IaaS) solutions:

1) Packet capture - Network Watcher lets you create temporary capture packet sessions on traffic headed to and from a virtual machine. Each packet capture session has a time limit. When the session ends, packet capture creates a pcap file that you can download and analyze. Network Watcher packet capture can't give you continuous port mirroring with these time constraints. For more information, see packet capture overview.

2) Network Security Group (NSG) flow logs - NSG flow logs capture information about IP traffic flowing through your NSGs. Network Watcher stores NSG flow logs as JSON files in Azure Storage account. You can export the NSG flow logs to an external tool for analysis. For more information, see NSG flow logs overview and data analysis options.

3) Traffic Analytics - Traffic Analytics ingests and analyzes NSG flow logs. It creates a dashboard of insights on the NSG flow logs and generates a geo-map view of your resources for easy analysis. For more information, see Traffic Analytics overview.

## Design recommendations

1) Enable Traffic Analytics. The tool lets you easily capture and analyze network traffic with out-of-the-box dashboard visualization and security analysis.

2) If you need more capabilities than Traffic Analytics offers, you can supplement Traffic Analytics with one of our partner solutions. You can find available partner solutions in the Azure Marketplace.

3) Use Network Watcher packet capture regularly to get a more detailed understanding of your network traffic. Run packet capture sessions at various times throughout the week to get a good understanding of the types of traffic traversing your network.

4) Don't develop a custom solution to mirror traffic for large deployments. The complexity and supportability issues tend to make custom solutions inefficient.
