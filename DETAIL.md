Trend Micro Deep Security for Splunk
=========================

Overview
--------
This package contains parsing logic, saved searches, and dashboards for monitoring Trend Micro Deep Security through Splunk.

Please read the [Installation](#installation) section below for details on how to configure Deep Security to use this app.

To contribute this app, see https://github.com/deep-security/splunk.

![](/screenshots/antimalware_dashboard.png) 

![](/screenshots/ips_dashboard.png)

<a name="installation"></a>Installation
------------
Install this app through the **Manage Apps** functionality within Splunk. For additional information on installing Splunk apps, please refer to the [Splunk documentation](https://docs.splunk.com/Documentation).

It is highly recommended that you follow the Splunk best practices for syslog, and that you configure rsyslog or syslog-ng to write syslog output to a file which can then be collected by a Splunk forwarder and sent to the Splunk server. You need to ensure that the Splunk forwarder sets the sourcetype to <code>deepsecurity</code> when forwarding events to a Splunk receiver.

Alternatively, you can set up a UDP syslog listener directly on the Splunk server and configure it to assign the sourcetype <code>deepsecurity</code> to all messages received.

Next, you'll need to configure Deep Security to send event data to your chosen collection method. Follow this guidance:

* To configure system events, log in to Deep Security Manager and go to **Administration > System Settings > Event Forwarding**.
* To configure security events, log in to Deep Security Manager, and go to **Policies**. Double-click one of your security policies and then go to **Settings > Event Forwarding**.

For details on event forwarding, see [this topic](https://help.deepsecurity.trendmicro.com/siem-syslog-forwarding-secure.html) in the Deep Security Help Center.

Upgrade from Version 1.4
------------
All syslog inputs in the Deep Security for Splunk app that were included in version 1.4 have been removed. If you are upgrading from version 1.4 and were using the individual syslog listening ports, you'll need to configure a new syslog input which assigns the sourcetype <code>deepsecurity</code>. This can be a single UDP syslog port in version 1.5.1 and doesn't need to be individual ports as it was in version 1.4.

This change helps make the app compatible with both Splunk Enterprise and Splunk Cloud.

Usage
------------
You can configure Deep Security to send event data in Common Event Format (CEF). This add-on parses the various syslog messages and extracts the appropriate fields, including the custom key/value pairs.

Example:

CEF:0|Trend Micro|Deep Security Agent|8.0.0.995|1001111|Test Intrusion Prevention Rule|3|cn1=1 cn1Label=Host ID dvchost=hostname dmac=00:50:56:F5:7F:47 smac=00:0C:29:EB:35:DE TrendMicroDsFrameType=IP src=192.168.126.150 dst=72.14.204.105 out=1093 cs3=DF 0 cs3Label=Fragmentation Bits proto=TCP spt=49786 dpt=80 cs2=0x00 ACK PSH cs2Label=TCP Flags cnt=1 act=IDS:Reset cn3=10 cn3Label=Intrusion Prevention Packet Position cs5=10 cs5Label=Intrusion Prevention Stream Position cs6=8 cs6Label=Intrusion Prevention Flags

Using the message above as an example, the add-on extracts the following custom key/value pairs:

Host_ID=1
Fragmentation Bits=DF
Intrusion Prevention Packet Position=10
Intrusion Prevention Stream Position=10
Intrusion Prevention Flags=8
