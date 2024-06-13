# CUCM 12.0 Installation - Touchless

# Contents

[CUCM 12.0 Installation - Touchless [1](#_Toc533088250)](#_Toc533088250)

[Useful Links [1](#useful-links)](#useful-links)

[Environment [1](#environment)](#environment)

[Prerequisite Tasks [2](#prerequisite-tasks)](#prerequisite-tasks)

[Create the CUCM Answer Files
[2](#create-the-cucm-answer-files)](#create-the-cucm-answer-files)

[Download the Answer Files
[5](#download-the-answer-files)](#download-the-answer-files)

[Create the Cisco Unified Communications IM & P Answer Files
[7](#create-the-cisco-unified-communications-im-p-answer-files)](#create-the-cisco-unified-communications-im-p-answer-files)

[Edit the clusterConfig.xml
[10](#edit-the-clusterconfig.xml)](#edit-the-clusterconfig.xml)

[Create The Virtual Floppies for Touchless Install
[14](#create-the-virtual-floppies-for-touchless-install)](#create-the-virtual-floppies-for-touchless-install)

[Figure 1 Answer File Generator Web Page
[2](#_Toc533088259)](#_Toc533088259)

[Figure 2 Add Secondary Node to Answer File Generator
[5](#_Toc533088260)](#_Toc533088260)

[Figure 3 Answer File Generator Steps to Download Files
[5](#_Toc533088261)](#_Toc533088261)

[Figure 4 Example of View Page Source
[6](#_Toc533088262)](#_Toc533088262)

[Figure 5 Formatted XML for platformConfig.xml
[7](#_Toc533088263)](#_Toc533088263)

[Figure 6 Cisco Unified Communications IM and Presence Answer File
[9](#_Toc533088264)](#_Toc533088264)

[Figure 7 Map Floppy Images to VM [15](#_Toc533088265)](#_Toc533088265)

[Figure 8 Map Floppy Images Continued
[16](#_Toc533088266)](#_Toc533088266)

[Figure 9 Select the Floppy Image for the CUCM Publisher
[17](#_Toc533088267)](#_Toc533088267)

[Figure 10 Verify that the new Floppy Image is Connected
[18](#_Toc533088268)](#_Toc533088268)

[Table 1 CUCM Clusterwide Parameters
[3](#_Toc533088269)](#_Toc533088269)

[Table 2 Primary Node Configuration Parameters
[4](#_Toc533088270)](#_Toc533088270)

[Table 3 Secondary Node Configuration Parameters
[4](#_Toc533088271)](#_Toc533088271)

[Table 4 Cisco Unified Communications IM and Presence Clusterwide
Configuration [9](#_Toc533088272)](#_Toc533088272)

[Table 5 Cisco Unified Communications Mananger (Publisher) Configuration
[9](#_Toc533088273)](#_Toc533088273)

[Table 6 Cisco Unified Communications IM and Presence Configuration
[10](#_Toc533088274)](#_Toc533088274)

[Table 7 Answer File to Node Mapping
[14](#_Ref532794697)](#_Ref532794697)

## Useful Links

<https://www.cisco.com/c/en/us/td/docs/voice_ip_comm/cucm/install/11_0_1/CUCM_BK_IDF93684_00_installing-cucm_1101/Installation_tasks.html#CUCM_RF_A234242C_00>

<https://www.cisco.com/c/en/us/applicat/content/cuc-afg/index.html>

<https://community.cisco.com/t5/unified-communications/solved-unattended-installation/td-p/2699965>

## Environment

The environment for this installation includes the following hardware
and software.

-   Windows 2012r2 (running as a virtual machine)

-   Cisco 2921 IOS Router configured for NTP Master

-   VMWare ESXi 6.5

-   VMWare vCenter 6.5

-   Cisco Unified Communications Manager 12.0

-   Cisco Unified Communications Manager Instant Messaging and Presence
    12.0

## Prerequisite Tasks

### Create the CUCM Answer Files

A Cisco UCM cluster touchless installation is dependent on several
components. A breakdown in the process can make the touchless install
fail completely or lead to an instance where manual intervention to
resolve the issues and continue the installation post error is required.

The creation of the answer files for the installation is twofold. First,
a clusterConfig.xml file is generated via the input provided to the
Answer File Generator (AFG) web portal. Second, a platformConfig.xml
file is created for each node in the cluster based on the information
provided previously.

To begin the creation of the answer files open a browser such as FireFox
or Chrome and navigate to
<https://www.cisco.com/c/en/us/applicat/content/cuc-afg/index.html>.

On at the website select the application that will be deployed including
the version, all the while ensuring that the radio button for Virtual
Machine is selected.

<img
src=".\attachments\CUCM 12.0 Installation - touchless/media/image1.png"
style="width:6.5in;height:4.15486in" />

The following fields will need to be populated for both the CUCM Pub and
CUCM Sub

<table>
<caption><p><span id="_Toc533088259" class="anchor"></span>Figure 1
Answer File Generator Web Page</p></caption>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th colspan="2">Hardware</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Primary Node Installed on</td>
<td>Virtual Machine</td>
</tr>
<tr class="even">
<td colspan="2">Product</td>
</tr>
<tr class="odd">
<td>Product</td>
<td>Cisco Unified Communications Manager</td>
</tr>
<tr class="even">
<td>Version</td>
<td>12.0.1</td>
</tr>
<tr class="odd">
<td colspan="2">Administrator Credentials</td>
</tr>
<tr class="even">
<td>Administrator Username</td>
<td></td>
</tr>
<tr class="odd">
<td>Password</td>
<td></td>
</tr>
<tr class="even">
<td colspan="2">Security Password</td>
</tr>
<tr class="odd">
<td>Password</td>
<td></td>
</tr>
<tr class="even">
<td colspan="2">Application User Credentials</td>
</tr>
<tr class="odd">
<td>Application Username</td>
<td></td>
</tr>
<tr class="even">
<td>Password</td>
<td></td>
</tr>
<tr class="odd">
<td colspan="2">Certificate Information</td>
</tr>
<tr class="even">
<td>Organization</td>
<td></td>
</tr>
<tr class="odd">
<td>Unit</td>
<td></td>
</tr>
<tr class="even">
<td>Location</td>
<td></td>
</tr>
<tr class="odd">
<td>State</td>
<td></td>
</tr>
<tr class="even">
<td>Country</td>
<td>United States of America</td>
</tr>
<tr class="odd">
<td colspan="2">SMTP</td>
</tr>
<tr class="even">
<td>Configure SMTP Host (optional)</td>
<td>NOT Checked</td>
</tr>
<tr class="odd">
<td>SMTP Location (greyed out unless Configure SMTP is enabled)</td>
<td></td>
</tr>
</tbody>
</table>

<span id="_Toc533088259" class="anchor"></span>Figure 1 Answer File
Generator Web Page

The table below continues the information provided to the AFG website,
this portion however is for the CUCM Publisher

<table>
<caption><p><span id="_Toc533088269" class="anchor"></span>Table 1 CUCM
Clusterwide Parameters</p></caption>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th colspan="2">Primary NIC Settings</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Use Auto Negotiation*</p>
<p>*Virtual Machines do not use this setting</p></td>
<td>Checked (greyed out)</td>
</tr>
<tr class="even">
<td>NIC Speed</td>
<td>100 (greyed out)</td>
</tr>
<tr class="odd">
<td>NIC Duplex</td>
<td>Full (greyed out)</td>
</tr>
<tr class="even">
<td>Change MTU Size</td>
<td>Not checked</td>
</tr>
<tr class="odd">
<td>MTU Size</td>
<td></td>
</tr>
<tr class="even">
<td colspan="2">Network Information</td>
</tr>
<tr class="odd">
<td>Use DHCP for IP Address Resolution</td>
<td>Not Checked</td>
</tr>
<tr class="even">
<td>Host Name</td>
<td></td>
</tr>
<tr class="odd">
<td>IP Address</td>
<td></td>
</tr>
<tr class="even">
<td>IP Mask</td>
<td></td>
</tr>
<tr class="odd">
<td>Gateway Address</td>
<td></td>
</tr>
<tr class="even">
<td colspan="2">DNS</td>
</tr>
<tr class="odd">
<td>Configure Client DNS</td>
<td>Checked</td>
</tr>
<tr class="even">
<td>Primary DNS</td>
<td></td>
</tr>
<tr class="odd">
<td>Secondary DNS (optional)</td>
<td></td>
</tr>
<tr class="even">
<td>Domain</td>
<td></td>
</tr>
<tr class="odd">
<td colspan="2">Time Zone</td>
</tr>
<tr class="even">
<td>Region</td>
<td></td>
</tr>
<tr class="odd">
<td>Time Zone</td>
<td></td>
</tr>
<tr class="even">
<td colspan="2">Network Time Protocol</td>
</tr>
<tr class="odd">
<td>NTP Server 1</td>
<td></td>
</tr>
<tr class="even">
<td>Repeat as needed for additional NTP Servers (NTP servers should
Stratum 3 or better)</td>
<td></td>
</tr>
<tr class="odd">
<td colspan="2">Dynamic Cluster Configuration</td>
</tr>
<tr class="even">
<td>Dynamic Cluster Config Enable</td>
<td>Checked</td>
</tr>
<tr class="odd">
<td><p>Dynamic Cluster Config Timer</p>
<p>The default of 24 hours is left but can be changed based on network
requirements.</p></td>
<td>24</td>
</tr>
</tbody>
</table>

<span id="_Toc533088269" class="anchor"></span>Table 1 CUCM Clusterwide
Parameters

With the Publisher configuration documented it is necessary to configure
the options for the Subscriber. The configuration of the Subscriber will
not be as detailed as the Publisher because it will reuse many of the
settings from the Publisher. If the deployment calls for not using the
Publisher settings for DNS, Time Zone, etc then populate the values
accordingly.

<table>
<caption><p><span id="_Toc533088270" class="anchor"></span>Table 2
Primary Node Configuration Parameters</p></caption>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th colspan="2">NIC Interface Settings</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Use Auto Negotiation*</p>
<p>*Virtual Machines do not use this setting</p></td>
<td>Checked (greyed out)</td>
</tr>
<tr class="even">
<td>NIC Speed</td>
<td>100 (greyed out)</td>
</tr>
<tr class="odd">
<td>NIC Duplex</td>
<td>Full (greyed out)</td>
</tr>
<tr class="even">
<td>Change MTU Size</td>
<td>Not checked</td>
</tr>
<tr class="odd">
<td>MTU Size</td>
<td></td>
</tr>
<tr class="even">
<td colspan="2">Network Information</td>
</tr>
<tr class="odd">
<td>Use DHCP for IP Address Resolution</td>
<td>Not Checked</td>
</tr>
<tr class="even">
<td>Host Name</td>
<td></td>
</tr>
<tr class="odd">
<td>IP Address</td>
<td></td>
</tr>
<tr class="even">
<td>IP Mask</td>
<td></td>
</tr>
<tr class="odd">
<td>Gateway Address</td>
<td></td>
</tr>
<tr class="even">
<td colspan="2">DNS</td>
</tr>
<tr class="odd">
<td>Configure Client DNS</td>
<td>Checked</td>
</tr>
<tr class="even">
<td>Use Primary Node DNS settings</td>
<td>Checked</td>
</tr>
<tr class="odd">
<td colspan="2">Time Zone</td>
</tr>
<tr class="even">
<td>Use Primary Node Time Zone Settings</td>
<td>Checked</td>
</tr>
<tr class="odd">
<td colspan="2">Network Time Protocol</td>
</tr>
<tr class="even">
<td>NTP Server 1</td>
<td></td>
</tr>
</tbody>
</table>

<span id="_Toc533088270" class="anchor"></span>Table 2 Primary Node
Configuration Parameters

Select the button titled “**Add Secondary Node**” to add the
configuration to the answer files.

Once selected verify the node has been added.

<img
src=".\attachments\CUCM 12.0 Installation - touchless/media/image2.png"
style="width:6.5in;height:1.84931in" />

### Download the Answer Files

Select Generate Answer Files

**Read the pop-up!**

<img
src=".\attachments\CUCM 12.0 Installation - touchless/media/image3.png"
style="width:5.72917in;height:5.3125in" />

<span class="mark">This tells you that you have to select the page
source so it is displayed as XML for each file being generated prior to
saving it. When you save it you will need to use specific file names
based on the file type. This also means that the platform config file
for the nodes will need to be in separate directories since the name
doesn’t change based on node.</span>

View the page source of the new window

<img
src=".\attachments\CUCM 12.0 Installation - touchless/media/image4.png"
style="width:6.5in;height:6.39375in" />

In the browser window select all the xml and paste in a text editor like
notepad++.

<img
src=".\attachments\CUCM 12.0 Installation - touchless/media/image5.png"
style="width:6.5in;height:5.88125in" />

Save the file as platformConfig.xml

Repeat for the subscriber answer file

Repeat for the clusterconfig answer file

### Create the Cisco Unified Communications IM & P Answer Files

In order to support the automagical touchless install of the Cisco IM&P
node it is necessary to copy a portion of the Cisco IM&P
clusterConfig.xml file and paste it in to the clusterConfig.xml created
when the CUCM nodes answer files were created.

Select the option to “Clear All Data” from the main webpage for the
answer files.

<https://www.cisco.com/c/en/us/applicat/content/cuc-afg/index.html>

From the drop down menu select Cisco Unified Communications Manager IM
and Presence along with the appropriate version being installed.

<img
src=".\attachments\CUCM 12.0 Installation - touchless/media/image6.png"
style="width:6.5in;height:1.56111in" />

The same process should be followed for the initial portion of the
answer file where the clusterwide configuration is populated first. The
settings called out should match those configured when the initial CUCM
answer files were created.

<table>
<caption><p><span id="_Toc533088271" class="anchor"></span>Table 3
Secondary Node Configuration Parameters</p></caption>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th colspan="2">Hardware</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Primary Node Installed on</td>
<td>Virtual Machine</td>
</tr>
<tr class="even">
<td colspan="2">Product</td>
</tr>
<tr class="odd">
<td>Product</td>
<td>Cisco Unified Communications Manager</td>
</tr>
<tr class="even">
<td>Version</td>
<td>12.0.1</td>
</tr>
<tr class="odd">
<td colspan="2">Administrator Credentials</td>
</tr>
<tr class="even">
<td>Administrator Username</td>
<td></td>
</tr>
<tr class="odd">
<td>Password</td>
<td></td>
</tr>
<tr class="even">
<td colspan="2">Security Password</td>
</tr>
<tr class="odd">
<td>Password</td>
<td></td>
</tr>
<tr class="even">
<td colspan="2">Application User Credentials</td>
</tr>
<tr class="odd">
<td>Application Username</td>
<td></td>
</tr>
<tr class="even">
<td>Password</td>
<td></td>
</tr>
<tr class="odd">
<td colspan="2">Certificate Information</td>
</tr>
<tr class="even">
<td>Organization</td>
<td></td>
</tr>
<tr class="odd">
<td>Unit</td>
<td></td>
</tr>
<tr class="even">
<td>Location</td>
<td></td>
</tr>
<tr class="odd">
<td>State</td>
<td></td>
</tr>
<tr class="even">
<td>Country</td>
<td>United States of America</td>
</tr>
<tr class="odd">
<td colspan="2">SMTP</td>
</tr>
<tr class="even">
<td>Configure SMTP Host (optional)</td>
<td>NOT Checked</td>
</tr>
<tr class="odd">
<td>SMTP Location (greyed out unless Configure SMTP is enabled)</td>
<td></td>
</tr>
</tbody>
</table>

<span id="_Toc533088271" class="anchor"></span>Table 3 Secondary Node
Configuration Parameters

Once the cluster wide configuration is complete, the CUCM Publisher will
be configured in the Cisco Unified Communications Manager (Publisher)
Configuration.

<table>
<caption><p><span id="_Toc533088260" class="anchor"></span>Figure 2 Add
Secondary Node to Answer File Generator</p></caption>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th colspan="2">Primary NIC Settings</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Use Auto Negotiation*</p>
<p>*Virtual Machines do not use this setting</p></td>
<td>Checked (greyed out)</td>
</tr>
<tr class="even">
<td>NIC Speed</td>
<td>100 (greyed out)</td>
</tr>
<tr class="odd">
<td>NIC Duplex</td>
<td>Full (greyed out)</td>
</tr>
<tr class="even">
<td>Change MTU Size</td>
<td>Not checked</td>
</tr>
<tr class="odd">
<td>MTU Size</td>
<td></td>
</tr>
<tr class="even">
<td colspan="2">Network Information</td>
</tr>
<tr class="odd">
<td>Use DHCP for IP Address Resolution</td>
<td>Not Checked</td>
</tr>
<tr class="even">
<td>Host Name</td>
<td></td>
</tr>
<tr class="odd">
<td>IP Address</td>
<td></td>
</tr>
<tr class="even">
<td>IP Mask</td>
<td></td>
</tr>
<tr class="odd">
<td>Gateway Address</td>
<td></td>
</tr>
<tr class="even">
<td colspan="2">DNS</td>
</tr>
<tr class="odd">
<td>Configure Client DNS</td>
<td>Checked</td>
</tr>
<tr class="even">
<td>Primary DNS</td>
<td></td>
</tr>
<tr class="odd">
<td>Secondary DNS (optional)</td>
<td></td>
</tr>
<tr class="even">
<td>Domain</td>
<td></td>
</tr>
<tr class="odd">
<td colspan="2">Time Zone</td>
</tr>
<tr class="even">
<td>Region</td>
<td></td>
</tr>
<tr class="odd">
<td>Time Zone</td>
<td></td>
</tr>
<tr class="even">
<td colspan="2">Network Time Protocol</td>
</tr>
<tr class="odd">
<td>NTP Server 1</td>
<td></td>
</tr>
<tr class="even">
<td>Repeat as needed for additional NTP Servers (NTP servers should
Stratum 3 or better)</td>
<td></td>
</tr>
<tr class="odd">
<td colspan="2">Dynamic Cluster Configuration</td>
</tr>
<tr class="even">
<td>Dynamic Cluster Config Enable</td>
<td>Checked</td>
</tr>
<tr class="odd">
<td><p>Dynamic Cluster Config Timer</p>
<p>The default of 24 hours is left but can be changed based on network
requirements.</p></td>
<td>24</td>
</tr>
</tbody>
</table>

<span id="_Toc533088260" class="anchor"></span>Figure 2 Add Secondary
Node to Answer File Generator

Lastly the Cisco IM&P node will have it’s configuration specified in the
aptly named Cisco Unified Communications Manager IM and Presence Node
Configuration.

<table>
<caption><p><span id="_Toc533088261" class="anchor"></span>Figure 3
Answer File Generator Steps to Download Files</p></caption>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th colspan="2">NIC Interface Settings</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Use Auto Negotiation*</p>
<p>*Virtual Machines do not use this setting</p></td>
<td>Checked (greyed out)</td>
</tr>
<tr class="even">
<td>NIC Speed</td>
<td>100 (greyed out)</td>
</tr>
<tr class="odd">
<td>NIC Duplex</td>
<td>Full (greyed out)</td>
</tr>
<tr class="even">
<td>Change MTU Size</td>
<td>Not checked</td>
</tr>
<tr class="odd">
<td>MTU Size</td>
<td></td>
</tr>
<tr class="even">
<td colspan="2">Network Information</td>
</tr>
<tr class="odd">
<td>Use DHCP for IP Address Resolution</td>
<td>Not Checked</td>
</tr>
<tr class="even">
<td>Host Name</td>
<td></td>
</tr>
<tr class="odd">
<td>IP Address</td>
<td></td>
</tr>
<tr class="even">
<td>IP Mask</td>
<td></td>
</tr>
<tr class="odd">
<td>Gateway Address</td>
<td></td>
</tr>
<tr class="even">
<td colspan="2">IM &amp; P Domain Name</td>
</tr>
<tr class="odd">
<td>IM &amp; P Domain Name</td>
<td></td>
</tr>
<tr class="even">
<td colspan="2">DNS</td>
</tr>
<tr class="odd">
<td>Configure Client DNS</td>
<td>Checked</td>
</tr>
<tr class="even">
<td>Use Primary Node DNS settings</td>
<td>Checked</td>
</tr>
<tr class="odd">
<td colspan="2">Time Zone</td>
</tr>
<tr class="even">
<td>Use Primary Node Time Zone Settings</td>
<td>Checked</td>
</tr>
<tr class="odd">
<td colspan="2">Network Time Protocol</td>
</tr>
<tr class="even">
<td>NTP Server 1</td>
<td></td>
</tr>
</tbody>
</table>

<span id="_Toc533088261" class="anchor"></span>Figure 3 Answer File
Generator Steps to Download Files

Follow the steps in the Section titled Download the Answer Files to
download the platformConfig.xml and the clusterConfig.xml for the Cisco
Unified IM&P node.

### Edit the clusterConfig.xml

In order to support adding the IM&P node at the same time as the rest of
the cluster the CUCM clusterConfig.xml file will need to be updated to
include the information for the IM&P node.

The process to do this involves opening the CUCM clusterConfig.xml and
inserting the IM&P node information in to it.

First both the CUCM clusterConfig.xml and IM&P clusterConfig.xml files.
(you may need to rename one file to a different name in order to open
them in the same application like notepad++).

Within the clusterConfig.xml file for IM&P locate the section delineated
with &lt;Subscriber&gt; &lt;/Subscriber&gt; as seen below in .

&lt;/Publisher&gt;

&lt;Subscriber&gt;

&lt;Hostname&gt;

&lt;ParamNameText&gt;Host Name for this machine&lt;/ParamNameText&gt;

&lt;ParamDefaultValue&gt;none&lt;/ParamDefaultValue&gt;

&lt;ParamValue&gt;hq-imp&lt;/ParamValue&gt;

&lt;/Hostname&gt;

&lt;IpAddress&gt;

&lt;ParamNameText&gt;Node Ip Address&lt;/ParamNameText&gt;

&lt;ParamDefaultValue&gt;none&lt;/ParamDefaultValue&gt;

&lt;ParamValue&gt;10.100.64.17&lt;/ParamValue&gt;

&lt;/IpAddress&gt;

&lt;ImpDomainName&gt;

&lt;ParamNameText&gt;Domain Name&lt;/ParamNameText&gt;

&lt;ParamDefaultValue&gt;none&lt;/ParamDefaultValue&gt;

&lt;ParamValue&gt;cciecollab.internal&lt;/ParamValue&gt;

&lt;/ImpDomainName&gt;

&lt;Role&gt;

&lt;ParamNameText&gt;Node role&lt;/ParamNameText&gt;

&lt;ParamDefaultValue&gt;none&lt;/ParamDefaultValue&gt;

&lt;ParamValue&gt;2&lt;/ParamValue&gt;

&lt;/Role&gt;

&lt;Usage&gt;

&lt;ParamNameText&gt;Node usage&lt;/ParamNameText&gt;

&lt;ParamDefaultValue&gt;none&lt;/ParamDefaultValue&gt;

&lt;ParamValue&gt;0&lt;/ParamValue&gt;

&lt;/Usage&gt;

&lt;/Subscriber&gt;

This section will be copied in to the CUCM clusterConfig.xml just
between the last

&lt;/Subscriber&gt;&lt;/ClusterData&gt; sections. See the below
clusterConfig.xml as a reference.

&lt;?xml version="1.0"?&gt;

&lt;ClusterData&gt;

&lt;Version&gt;12.0.1&lt;/Version&gt;

&lt;Publisher&gt;

&lt;Hostname&gt;

&lt;ParamNameText&gt;Host Name for this machine&lt;/ParamNameText&gt;

&lt;ParamDefaultValue&gt;none&lt;/ParamDefaultValue&gt;

&lt;ParamValue&gt;hq-pub&lt;/ParamValue&gt;

&lt;/Hostname&gt;

&lt;IpAddress&gt;

&lt;ParamNameText&gt;Node Ip Address&lt;/ParamNameText&gt;

&lt;ParamDefaultValue&gt;none&lt;/ParamDefaultValue&gt;

&lt;ParamValue&gt;10.100.64.11&lt;/ParamValue&gt;

&lt;/IpAddress&gt;

&lt;Role&gt;

&lt;ParamNameText&gt;Node role&lt;/ParamNameText&gt;

&lt;ParamDefaultValue&gt;none&lt;/ParamDefaultValue&gt;

&lt;ParamValue&gt;1&lt;/ParamValue&gt;

&lt;/Role&gt;

&lt;Usage&gt;

&lt;ParamNameText&gt;Node usage&lt;/ParamNameText&gt;

&lt;ParamDefaultValue&gt;none&lt;/ParamDefaultValue&gt;

&lt;ParamValue&gt;0&lt;/ParamValue&gt;

&lt;/Usage&gt;

&lt;/Publisher&gt;

&lt;Subscriber&gt;

&lt;Hostname&gt;

&lt;ParamNameText&gt;Host Name for this machine&lt;/ParamNameText&gt;

&lt;ParamDefaultValue&gt;none&lt;/ParamDefaultValue&gt;

&lt;ParamValue&gt;hq-sub&lt;/ParamValue&gt;

&lt;/Hostname&gt;

&lt;IpAddress&gt;

&lt;ParamNameText&gt;Node Ip Address&lt;/ParamNameText&gt;

&lt;ParamDefaultValue&gt;none&lt;/ParamDefaultValue&gt;

&lt;ParamValue&gt;10.100.64.12&lt;/ParamValue&gt;

&lt;/IpAddress&gt;

&lt;Role&gt;

&lt;ParamNameText&gt;Node role&lt;/ParamNameText&gt;

&lt;ParamDefaultValue&gt;none&lt;/ParamDefaultValue&gt;

&lt;ParamValue&gt;1&lt;/ParamValue&gt;

&lt;/Role&gt;

&lt;Usage&gt;

&lt;ParamNameText&gt;Node usage&lt;/ParamNameText&gt;

&lt;ParamDefaultValue&gt;none&lt;/ParamDefaultValue&gt;

&lt;ParamValue&gt;1&lt;/ParamValue&gt;

&lt;/Usage&gt;

&lt;/Subscriber&gt;

&lt;Subscriber&gt;

&lt;Hostname&gt;

&lt;ParamNameText&gt;Host Name for this machine&lt;/ParamNameText&gt;

&lt;ParamDefaultValue&gt;none&lt;/ParamDefaultValue&gt;

&lt;ParamValue&gt;hq-imp&lt;/ParamValue&gt;

&lt;/Hostname&gt;

&lt;IpAddress&gt;

&lt;ParamNameText&gt;Node Ip Address&lt;/ParamNameText&gt;

&lt;ParamDefaultValue&gt;none&lt;/ParamDefaultValue&gt;

&lt;ParamValue&gt;10.100.64.17&lt;/ParamValue&gt;

&lt;/IpAddress&gt;

&lt;ImpDomainName&gt;

&lt;ParamNameText&gt;Domain Name&lt;/ParamNameText&gt;

&lt;ParamDefaultValue&gt;none&lt;/ParamDefaultValue&gt;

&lt;ParamValue&gt;cciecollab.internal&lt;/ParamValue&gt;

&lt;/ImpDomainName&gt;

&lt;Role&gt;

&lt;ParamNameText&gt;Node role&lt;/ParamNameText&gt;

&lt;ParamDefaultValue&gt;none&lt;/ParamDefaultValue&gt;

&lt;ParamValue&gt;2&lt;/ParamValue&gt;

&lt;/Role&gt;

&lt;Usage&gt;

&lt;ParamNameText&gt;Node usage&lt;/ParamNameText&gt;

&lt;ParamDefaultValue&gt;none&lt;/ParamDefaultValue&gt;

&lt;ParamValue&gt;0&lt;/ParamValue&gt;

&lt;/Usage&gt;

&lt;/Subscriber&gt;

&lt;/ClusterData&gt;

The final clusterConfig.xml file that includes the CUCM nodes and IM&P
nodes should be saved as it will be included with the floppy for the
CUCM Publisher node.

Once complete the files for each virtual floppy should look like those
contained in Table 4.

<table>
<caption><p><span id="_Toc533088262" class="anchor"></span>Figure 4
Example of View Page Source</p></caption>
<colgroup>
<col style="width: 24%" />
<col style="width: 25%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Node</th>
<th></th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>HQ-Pub</td>
<td>CUCM Publisher</td>
<td><p>platformConfig.xml</p>
<p>clusterConfig.xml</p>
<p>SKIP_VERSION_SCREEN</p></td>
</tr>
<tr class="even">
<td>HQ-Sub</td>
<td>CUCM Subscrbier</td>
<td><p>platformConfig.xml</p>
<p>SKIP_VERSION_SCREEN</p></td>
</tr>
<tr class="odd">
<td>HQ-IMP</td>
<td>IM&amp;P Primary</td>
<td><p>platformConfig.xml</p>
<p>SKIP_VERSION_SCREEN</p></td>
</tr>
</tbody>
</table>

<span id="_Toc533088262" class="anchor"></span>Figure 4 Example of View
Page Source

### Create The Virtual Floppies for Touchless Install

Virtual floppies will be created using an existing window’s virtual
machine rather than an application like Virtual Floppy drive or
WinImage. To perform this task an empty file will be created and named
for each node that it will be assigned to.

-   hq-pub.flp

-   hq-sub.flp

-   hq-imp.flp

The files will then be uploaded via vSphere Client or the vCenter
vSphere Web Client to the datastore that will be used to store the
installation media for the CUCM and IM&P. Once uploaded to the datastore
they will be sequentially mounted to the Windows 2012 r2 server. As they
are mounted on the server the files that were created in the Create the
Answer Files section will be copied over to the virtual floppy for each
node.

NOTE: once you initially access the new floppy disks in the VM image a
prompt may be present asking to format the floppy. This is expected and
needed to make the file readable as a floppy image. Once the format is
complete copy the files need for that particular node.

Create a text file without anything inside it. Name the file hq-pub.flp
(note the extension is .flp and not .txt). Repeat this for each node
that you are deploying to the cluster.

Upload the files with the .flp extension to the datastore where your
install media is located.

Open ESXi and navigate to the windows VM that will be used to create the
floppies containing the answer files.

Edit the settings for the VM

<img
src=".\attachments\CUCM 12.0 Installation - touchless/media/image7.png"
style="width:6.22917in;height:6.52083in" />

> Select the floppy and expand the dropdown. Select Use existing floppy
> image.
>
> <img
> src=".\attachments\CUCM 12.0 Installation - touchless/media/image8.png"
> style="width:6.21875in;height:6.46875in" />
>
> Select Browse followed by navigating to the location where you save
> the files.
>
> <img
> src=".\attachments\CUCM 12.0 Installation - touchless/media/image9.png"
> style="width:6.5in;height:4.89028in" />
>
> Select the file for the publisher then OK
>
> Verify that the options for the floppy being “Connected” and “Connect
> At Power On” are selected.
>
> <img
> src=".\attachments\CUCM 12.0 Installation - touchless/media/image10.png"
> style="width:6.22917in;height:6.45833in" />
>
> Select OK to save the changes that were made
>
> Repeat the process for the remaining Sub and IMP Pub
>
> Verify the software for CUCM on Pub &gt; Sub &gt; IMP
>
> <img
> src=".\attachments\CUCM 12.0 Installation - touchless/media/image11.png"
> style="width:6.5in;height:3.61042in" />
>
> <img
> src=".\attachments\CUCM 12.0 Installation - touchless/media/image12.png"
> style="width:6.5in;height:3.61806in" />
>
> <img
> src=".\attachments\CUCM 12.0 Installation - touchless/media/image13.png"
> style="width:6.5in;height:3.68056in" />
>
> <img
> src=".\attachments\CUCM 12.0 Installation - touchless/media/image14.png"
> style="width:6.5in;height:3.63194in" />
>
> <img
> src=".\attachments\CUCM 12.0 Installation - touchless/media/image15.png"
> style="width:6.5in;height:3.63403in" />
>
> <img
> src=".\attachments\CUCM 12.0 Installation - touchless/media/image16.png"
> style="width:6.5in;height:3.61944in" />
>
> <img
> src=".\attachments\CUCM 12.0 Installation - touchless/media/image17.png"
> style="width:6.5in;height:3.61806in" />
>
> <img
> src=".\attachments\CUCM 12.0 Installation - touchless/media/image18.png"
> style="width:6.5in;height:3.62431in" />
>
> <img
> src=".\attachments\CUCM 12.0 Installation - touchless/media/image19.png"
> style="width:6.5in;height:3.59097in" />
>
> <img
> src=".\attachments\CUCM 12.0 Installation - touchless/media/image20.png"
> style="width:6.5in;height:3.63542in" />

<img
src=".\attachments\CUCM 12.0 Installation - touchless/media/image21.png"
style="width:6.5in;height:3.65139in" />

<img
src=".\attachments\CUCM 12.0 Installation - touchless/media/image22.png"
style="width:6.5in;height:3.65069in" />

<img
src=".\attachments\CUCM 12.0 Installation - touchless/media/image23.png"
style="width:6.5in;height:3.60486in" />

<img
src=".\attachments\CUCM 12.0 Installation - touchless/media/image24.png"
style="width:6.5in;height:3.62292in" />

<img
src=".\attachments\CUCM 12.0 Installation - touchless/media/image25.png"
style="width:6.5in;height:3.67917in" />

<img
src=".\attachments\CUCM 12.0 Installation - touchless/media/image26.png"
style="width:6.5in;height:3.43403in" />
