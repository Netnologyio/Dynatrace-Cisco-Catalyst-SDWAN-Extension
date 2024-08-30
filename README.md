# Cisco Catalyst SD-WAN Extension

This Dynatrace extension, created by Netnology, for Cisco Catalyst SD-WAN Manager provides insight into key metrics for SD-WAN device and application performance.

Netnology’s Dynatrace extension for Cisco Catalyst SD-WAN Manager offers a comprehensive solution to monitor and optimize your SD-WAN infrastructure. By seamlessly integrating with SD-WAN Manager, this extension extracts critical performance metrics in real-time, providing a holistic view of your network's health and performance. This enables IT teams to proactively identify and resolve issues, ensuring optimal network performance and reliability. With detailed insights into latency, jitter, packet loss, and other key metrics, businesses can make informed decisions to enhance user experience, improve application performance, and maintain consistent, high-quality connectivity across all locations. Whether managing a single site or a global network, this extension empowers organizations to achieve superior network performance and agility.

## Requirements and Prerequisites

This extension is designed to run on an ActiveGate. Please ensure that you have one more ActiveGates deployed in your Dynatrace monitored environment in one or more ActiveGate groups. This extension does not run on OneAgents.

This extension utilizes the Cisco Catalyst SD-WAN Manager API to retrieve network information. Please ensure that you have one deployed and operational, and that there is network connectivity from any potential ActiveGate hosts to the target Cisco Catalyst SD-WAN Manager(s). Note the hostname and protocol used to reach them.

For the extension to function properly, you must create a user account that the extension will use to authenticate with the SD-WAN Manager; read-only access is sufficient. See below for the full list of metrics that will be obtained. The username and password for this account will be required during configuration later.

## Installation

Installing this extension is a two-part process. The first is the root certificate for this extension, which is generally a one-time only part. The second part must be done for every version of the extension you install.

First, download the required files. You can click [this link](https://github.com/adeelahmed373/Dynatrace_SD-WAN_Extension/archive/refs/heads/main.zip) to download the zip file. Alternatively, above and to the right of the files, you should see a green "Code" button with a drop down indicator. Click this button, and then click "Download ZIP" from the menu that appears. This will provide you with a `.zip` file containing all the files you see within it.

### Extension Root Certificate

Because this extension uses the Python-based Extensions 2.0 Framework, you are required to upload a certificate that is unique to this extension (but not to each version of this extension). This is provided as `custom_nn-sdwan_root.pem`. You must upload this both to Dynatrace as well as any hosts that will execute the extension.

To upload it to Dynatrace, follow these steps:
- Log in to your environment and go to the **Credential Vault**.
- Click on **Add new credential**.
- For *Credential type*, select *Public Certificate* from the dropdown.
- For *Credential name*, choose any identifying string, such as _"Cisco Catalyst SD-WAN Extension Certificate by Netnology"_.
- For *Credential scope*, check only the checkbox for *Extension validation*.*
- For *Certificate file*, upload `custom_nn-sdwan_root.pem`. At the time of writing, passwords are not supported, but for future reference, there is no password.
- For *Description*, You may enter a long-form description for this credential if you'd like.
- Configure who has access to this credential as you see fit.
- Click **Save**.

Next, the file needs to be uploaded to each and every ActiveGate host that may execute the extension. Refer to [this documentation](https://docs.dynatrace.com/docs/extend-dynatrace/extensions20/sign-extension#upload) for the upload location. Follow the instructions for "Remote extensions", as this extension is designed for ActiveGate execution ("remote" execution) only. For tracking purposes, we suggest that you do not change the name of the file.

### Extension Executable Files

This extension itself is distributed as a zip file in the form of `custom_nn-sdwan-VERSION.zip`. You need to add this to your Dynatrace environment, just as with the certificate above. However, these steps will need to be repeated for every new version of the extension.

To upload it to Dynatrace, follow these steps:
- Go to the **Dynatrace Hub**
- Click on the **Manage & upload extensions** tab
- Scroll to the bottom and click on **Upload custom Extension 2.0**
- Upload the `custom_nn-sdwan-VERSION.zip` file.
- Upload the provided `CiscoCatalystSdwanExtIcon.png` file as the extension icon.
- For *Extension 2.0 name*, enter "Cisco Catalyst SD-WAN Extension by Netnology".
- Click **Upload Extension**.

Once you set up and deploy a monitoring configuration (next step), the extension should be distributed to your hosts automatically.

## Configuration

Setting up a new monitoring configuration is straightforward. Navigate to this extension in the Dynatrace Hub and choose **Add monitoring configuration**.

On the first page, you will designate the ActiveGate group on which the extension will run. On the second page, you may onboard one or more SD-WAN Managers. To fully configure each, simply enter the protocol, hostname, username, and password as described earlier. When complete, advance to the third and final page where you may provide a description of the configuration you made.

A dashboard has been provided to view the collected data. To view it, upload it to your environment. Go to **Dashboards**, click on **Import dashboard**, and choose `Cisco Catalyst SD-WAN Overview.json`. If/when metrics are being collected, the tiles will automatically begin populating.

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
