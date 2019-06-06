Trend Micro Deep Security for Graylog
=========================

Overview
--------
This package contains parsing logic, saved searches, and dashboards for monitoring Trend Micro Deep Security through Graylog.

Please read the [Installation](#installation) section below for details on how to configure Deep Security to use this app.

![](/screenshots/antimalware_dashboard.png) 

![](/screenshots/ips_dashboard.png)

<a name="installation"></a>Installation
------------
TO DO

Next, you'll need to configure Deep Security to send event data to your chosen collection method. Follow this guidance:

* To configure system events, log in to Deep Security Manager and go to **Administration > System Settings > Event Forwarding**.
* To configure security events, log in to Deep Security Manager, and go to **Policies**. Double-click one of your security policies and then go to **Settings > Event Forwarding**.

For details on event forwarding, see [this topic](https://help.deepsecurity.trendmicro.com/siem-syslog-forwarding-secure.html) in the Deep Security Help Center.

Usage
------------
Please configure Deep Security to send event data in Common Event Format (CEF). This add-on parses the various syslog messages and extracts the appropriate fields, including the custom key/value pairs.

Example:

<code>CEF:0|Trend Micro|Deep Security Agent|8.0.0.995|1001111|Test Intrusion Prevention Rule|3|cn1=1 cn1Label=Host ID dvchost=hostname dmac=00:50:56:F5:7F:47 smac=00:0C:29:EB:35:DE TrendMicroDsFrameType=IP src=192.168.126.150 dst=72.14.204.105 out=1093 cs3=DF 0 cs3Label=Fragmentation Bits proto=TCP spt=49786 dpt=80 cs2=0x00 ACK PSH cs2Label=TCP Flags cnt=1 act=IDS:Reset cn3=10 cn3Label=Intrusion Prevention Packet Position cs5=10 cs5Label=Intrusion Prevention Stream Position cs6=8 cs6Label=Intrusion Prevention Flags</code>

Using the message above as an example, the add-on extracts the following custom key/value pairs:

* <code>Host_ID=1</code>
* <code>Fragmentation Bits=DF</code>
* <code>Intrusion Prevention Packet Position=10</code>
* <code>Intrusion Prevention Stream Position=10</code>
* <code>Intrusion Prevention Flags=8</code>
