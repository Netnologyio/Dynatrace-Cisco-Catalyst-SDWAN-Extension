# Cisco Catalyst SD-WAN Extension

This Dynatrace extension, created by Netnology, for Cisco Catalyst SD-WAN Manager provides insight into key metrics for SD-WAN device and application performance.

Netnology’s Dynatrace extension for Cisco Catalyst SD-WAN Manager offers a comprehensive solution to monitor and optimize your SD-WAN infrastructure. By seamlessly integrating with SD-WAN Manager, this extension extracts critical performance metrics in real-time, providing a holistic view of your network's health and performance. This enables IT teams to proactively identify and resolve issues, ensuring optimal network performance and reliability. With detailed insights into latency, jitter, packet loss, and other key metrics, businesses can make informed decisions to enhance user experience, improve application performance, and maintain consistent, high-quality connectivity across all locations. Whether managing a single site or a global network, this extension empowers organizations to achieve superior network performance and agility.

## Requirements and Prerequisites

This extension is designed to run on an ActiveGate. Please ensure that you have one more ActiveGates deployed in your Dynatrace monitored environment in one or more ActiveGate groups.

This extension utilizes the Cisco Catalyst SD-WAN Manager API to retrieve network information. Please ensure that you have one deployed and operational, and that there is network connectivity from any potential ActiveGate hosts to the target Cisco Catalyst SD-WAN Manager(s). Note the hostname and protocol used to reach them.

For the extension to function properly, you must create a user account for extension authentication; read-only access is sufficient. See below for the full list of metrics that will be accessed. The username and password will be needed.

## Installation

This extension is distributed as a zip file in the form of `custom_nn-sdwan-VERSION.zip`. You need to add this to your Dynatrace server as well as the hosts it will execute on.

To upload it to Dynatrace, go to **Settings** > **Monitoring** > **Monitoring technologies** > **Custom extensions** > **Upload extension** and choose the zip file.

To upload it to your ActiveGate hosts, copy the same zip file into `/opt/dynatrace/remotepluginmodule/plugin_deployment` on Linux and `C:\Program Files\dynatrace\remotepluginmodule\plugin_deployment` on Windows. Unzip the file afterwards.

Lastly, restart the service to enable the extension. On Linux, run `systemctl restart remotepluginmodule` in a terminal session. On Windows, restart the **Dynatrace RemotePlugin Module** service.

## Configuration

Setting up a new monitoring configuration is straightforward. Navigate to this extension in the Dynatrace Hub and choose **Add monitoring configuration**.

On the first page, you will designate the ActiveGate group on which the extension will run. On the second page, you may onboard one or more SD-WAN Managers. To fully configure each, simply enter the protocol, hostname, username, and password as described earlier. When complete, advance to the third and final page where you may provide a description of the configuration you made.

## Collected Metrics

|Metric                                    |Type |Unit       |Description|
|------------------------------------------|-----|-----------|-----------|
|nn_sdwan.app_aware_routing.jitter         |gauge|millisecond|The change in latency for packets when traversing a link|
|nn_sdwan.app_aware_routing.latency        |gauge|millisecond|The time required for packets to traverse a link|
|nn_sdwan.app_aware_routing.loss_percentage|gauge|percent    |The percentage of packets lost during transmission|
|nn_sdwan.app_aware_routing.rx_octets      |gauge|byte       |The number of octets received on a link|
|nn_sdwan.app_aware_routing.tx_octets      |gauge|byte       |The number of octets transmitted on a link|
|nn_sdwan.cert_summary                     |gauge|           |The number of normal, warning, and invalid certificates|
|nn_sdwan.connection_summary_stats_error   |gauge|           |The number of certificate errors for WAN edges, vBond devices, and vSmart devices|
|nn_sdwan.connection_summary_stats_total   |gauge|           |The number of certificates for WAN edges, vBond devices, and vSmart devices|
|nn_sdwan.device_control_status            |gauge|           |The number of devices that are up, partially up, and/or down|
|nn_sdwan.reboot_count                     |gauge|           |The number of times in the past 24 hours that the controller has rebooted|
|nn_sdwan.site_health                      |gauge|           |The number of sites that are up, contain warnings, and/or are down|
|nn_sdwan.top_app_stats                    |gauge|byte       |The number of bytes sent across a link by application|
|nn_sdwan.transport_interface              |gauge|           |The number of links with active throughput within a particular range|
|nn_sdwan.vmanage_count                    |gauge|           |The number of devices for each status|
|nn_sdwan.wan_edge_health                  |gauge|           |The number of normal, warning and error WAN edges|
|nn_sdwan.wan_edge_inventory               |gauge|           |The number of deployed, authorized, staging, and total WAN edges|
