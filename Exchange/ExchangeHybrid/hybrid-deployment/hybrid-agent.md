---
title: Microsoft Hybrid agent – Preview
---

# Microsoft Hybrid agent – Preview

The Hybrid agent removes some of the challenges you might face when configuring an Exchange Hybrid environment. The agent, which is built on the same technology as the Azure Application Proxy, helps you set up external DNS entries, update certificates, allow inbound network connections through your firewall, and more, so you can use enhanced Exchange hybrid features. These features include Free/Busy synchronization, online mailbox moves, enhanced mail flow, directory synchronization, and so on.

## Agent Install Location & Requirements

The agent install and subsequent run of configuring Hybrid via the Hybrid Configuration Wizard is supported on either a standalone computer designed as your "agent server", or an Exchange 2010, 2013, 2016 or 2019 server with the Client Access role. 

## System requirements

The Hybrid agent has the following requirements:

- The computer it'll be installed on needs to be:
  - Running Windows Server 2012 R2 or 2016 with .NET Framework 4.6.2 (or later, as supported by the Exchange version you are installing on)
  - Joined to an Active Directory domain
  - TLS 1.2 enabled
    - Azure Application Proxy documentation: https://docs.microsoft.com/en-us/azure/active-directory/manage-apps/application-proxy-add-on-premises-application  
  - Capable of establishing outbound HTTPS connections to the Internet
  - Capable of establishing HTTPS and remote PowerShell connections to the CAS chosen for hybrid configuration.
- You need to use a browser, like Microsoft Edge, that supports ClickOnce technology.
- The on-premises Active Directory account you're logged into must:
  - Be a member of the Organization Management role group in your on-premises Exchange organization
  - Be a member of the local Administrators group on the computer where you're installing the Hybrid agent.
- The account you use to connect to your Office 365 tenant must be a Global Administrator.
  
## Port and protocol requirements

- Outbound ports HTTPS (TCP) 443 and 80 must be open between the computer that has the Hybrid agent installed and the Internet, as shown here: https://docs.microsoft.com/en-us/azure/active-directory/manage-apps/application-proxy-enable. 
- Ports HTTPS (TCP) 443, 80, 5985 and 5986 must be open between the computer that has the Hybrid agent installed an the Client Access Server (CAS) that's selected in the Hybrid Configuration wizard.

    > [!IMPORTANT]
    > All Client Access Servers must be able to reach outbound to Office 365 endpoints via HTTPS (TCP) 443 as free/busy request from on-premises users to Office 365 users do not traverse the Hybrid agent. These requests still require your Exchange servers have outbound connectivity to Office 365 end points. Office 365 URLs and IP address ranges describes the required (and hybrid) ports and IPs outbound from on-prem to the service here: https://docs.microsoft.com/en-us/office365/enterprise/urls-and-ip-address-ranges. 

### Proxy server considerations

If your network environment uses outbound proxy servers, additional configuration and requirements come into play. This list may not be exhaustive.

#### Agent

The agent supports outbound proxy servers but requires additional configuration after installation. 

> [!IMPORTANT]
> A proxy server that prevents registration will result in the connector failing to install. It is recommended to install allowing the connectors to bypass the proxy until app config changes can be made.

#### Client Access Server

The HCW establishes connections from your Client Access Server to domains.live.com to exchange metadata and establish trusts. Because connections originate from your CAS server, the proxy settings on that server (from `Get-ExchangeServer | Format-List InternetWebProxy`) must be set correctly or outbound free/busy may fail. In addition to this, the HCW may not be able to configure delegated authentication if this setting is incorrect.

## Preview Constraints

Please keep the following issues in mind before installing the Hybrid agent:

- MailTips, Message Tracking, and Multi-mailbox search do not traverse the Hybrid agent. These Hybrid features require the classic connectivity model where Exchange Web Services (EWS) and Autodiscover are published on-premises and are externally available to Office 365.
- The public preview only supports a single Hybrid agent install for the Exchange organization. We are working to support multiple agent installs for redundancy, but this is not available yet. If the server running the Hybrid agent goes offline, free/busy lookups from your tenant to your on-premises organization and mailbox migrations to or from your tenant won't work. If the server hosting the agent is permanently offline, was rebuilt, or the agent was uninstalled, you can re-run the Hybrid Configuration wizard to reinstall the Hybrid agent directly on the new server. 

    > [!WARNING]
    > Don't attempt to install multiple active Hybrid agents in your environment with this preview build, this could cause unexpected issues.

- The Hybrid agent registers the internal fully qualified domain name (FQDN) of the CAS server selected when running Hybrid Configuration wizard in Azure Application Proxy. If the registered CAS is offline, free/busy look ups from your tenant to on-premises and mailbox migrations to/from your tenant won't work. If the selected CAS is permanently offline, a new CAS server must be registered. This can be done by re-running the Hybrid Configuration wizard. 
- The Hybrid agent preview comes with some support limitations which are called out in the Terms document you must agree to before installing the feature.

    > [!NOTE]
    > SMTP doesn't traverse the Hybrid agent and still requires a public certificate for mail flow between Office 365 and your  on-premises organization. SMTP traffic is out of scope for the Hybrid agent, both now and through General Availability.

## Running Setup

The HCW is the application responsible for both installing and configuring the Hybrid agent and setting the required configuration both in your on-premises organization and in your Office 365 tenant. You must run the HCW from the computer where you want the agent installed. After the Agent is installed and configured, the HCW will locate a preferred server to connect to and run the standard hybrid configuration steps. You do not have to run the HCW from the Exchange server directly, but as stated above, the computer where the HCW is run must be able to connect to the CAS server using the ports specified in the [Ports and protocols](#port-and-protocol-requirements) section.

> [!NOTE]
> The Modern Hybrid option will only be presented if you have never run the Hybrid Configuration wizard. If you have successfully established Hybrid in either Minimal or Full in our "classic config" for your tenant, this new option won't be presented to you.

### Installation Prerequisites

1. To allow installation of the Hybrid agent and perform mailbox migrations to and from your Office 365 tenant, enable the Mailbox Replication service (MRS) proxy on the EWS virtual directory using the following command.

    ```PowerShell
    Set-WebServicesVirtualDirectory -Identity "EWS (Default Web Site)" -MRSProxyEnabled $true
    ```

2. Go to **Programs and Features** and verify a previous version of the **Microsoft Office 365 Hybrid Configuration Wizard** is not already installed. If it is, uninstall it.
3. Install .NET Framework version 4.6.2 (or later, as supported by the version of Exchange you're running) on the computer where the HCW is being run. Alternatively, if this version isn't installed, the HCW will prompt you to install it or upgrade the version already installed on your computer.

### Installation steps

1. Run the HCW by logging into your on-premises Exchange Admin Center (EAC), navigating to the **Hybrid** node, and then clicking **Configure**. 
2. Select the Exchange server where the traditional hybrid setup should be run. Either select the default server provided by the HCW or specify a specific server in the second radio button. Select **Next**.
3. Enter your on-premises Exchange credentials and your Office 365 Global Administrator credentials. Select **Next**.
4. Wait while the HCW gathers information and configuration about your environments. When it’s completed, select **Next**.
5. Select either **Minimal** or **Full Hybrid Configuration**. You can also choose **Organization Configuration Transfer**. For more information, see [Hybrid Organization Configuration Transfer](https://blogs.technet.microsoft.com/exchange/2018/06/18/hybrid-organization-configuration-transfer/). Select **Next**.
6. Select **Use Exchange Modern Hybrid**

    ![Hybrid Topology page](../media/08b9b1933233cf4348506a629d1a6f22.png)

    Select **Next**.
7. The HCW will install the Hybrid agent. There are four basic phases:
    1. Downloading the agent install package
    2. Installation of the agent on the local computer (note: this will prompt for your Office 365 Global Administrator credentials again)
    3. Registration of the agent in Azure, including creation of the URL used to proxy requests. The URL has the format `uniqueGUID.resource.mailboxmigration.his.msappproxy.net`.
    4. Testing migration viability from your Office 365 tenant to your on-premises Exchange organzation via the agent.

    > [!NOTE]
    > The Hybrid agent installation process could take up to 10 minutes to complete.

The rest of the HCW steps are the same as a traditional Hybrid deployment. During the final configuration application phase of the HCW, the HCW creates a new migration endpoint with the custom URL and sets the `TargetSharingEPR` value on the Organization Relationship and/or the IntraOrganization Connector. Both the new migration endpoint value and the `TargetSharingEPR` value are set on Office 365 side only. The new URL is used to send requests from your Office 365 tenant to your on-premises Exchange organization for free busy and migrations. On-premises free/busy requests for Office 365 mailboxes are sent from your on-premises CAS servers to Office 365. You can view the specific values configured for each of these by running `Get-MigrationEndpoint` and `Get-OrganizationRelationship` from a remote PowerShell session connected to your Office 365 tenant. The following shows example output that you might see when running the `Get-MigrationEndpoint` cmdlet.

```PowerShell
PS C:\Users\Hybrid\> Get-MigrationEndpoint | fl Identity,RemoteServerIdentity : Hybrid Migration Endpoint - EWS (Default Web Site)

RemoteServer :
087f1c2e-8711-4176-ab4f-4b1c1777a350.resource.mailboxmigration.his.msappproxy.net

PS C:\Users\Hybrid\> Get-OrganizationRelationship | fl Name,TargetSharingEpr

Name : O365 to On-premises - c6d22e11-2340-4432-9122-19097bacf0c1

TargetSharingEpr :
https://087f1c2e-8711-4176-ab4f-4b1c1777a350.resource.mailboxmigration.his.msappproxy.net/EWS/Exchange.asmx
```

## Additional Information

Installation details of the Hybrid agent can be viewed in the following locations on the server where it is installed. E.g.:

![](../media/183c42b7f780c0f11399ad84d5b794ca.png)

`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Hybrid Service:`

![](../media/3d0ea73be12c78a759c3e6947dbfcea6.png)

![](../media/cc0348c42c337d0dd313272aed0bfd89.png)

Add/Remove programs:

![](../media/f06cc90d380e6f23cedc43d38a7fc075.png)

## Testing & validation of the Hybrid agent

After successful deployment of the Hybrid agent and hybrid configuration, the following are two simple tests to validate free/busy and mailbox migration flow via the Agent.

On the server where the Hybrid agent is installed, open **Performance Monitor**. Add the object **Microsoft AD App Proxy Connector** and the **\# requests** counter to your view.

![](../media/d67d36919447785a56ab2b3759e12e74.png)

### Migration

Open an remote PowerShell session to your Office 365 tenant and run the following test cmdlet:

```PowerShell
Test-MigrationServerAvailability -ExchangeRemoteMove: $true -RemoteServer '<your customguid>.resource.mailboxmigration.his.msappproxy.net' -Credentials (Get-Credential)
```

Enter your on-premises credentials in the dialog that appears. After the test returns the success result, switch back to **Performance Monitor** and you can see the number of requests will have incremented up.

Performing a test mailbox move from your on-premises Exchange organization to your Office 365 tenant is also an option.

### Free/Busy

The same validation can be performed by logging into an Office 365 mailbox in your tenant and requesting free/busy via a test meeting request sent to an on-premises mailbox.

## Uninstalling the Hybrid agent

To uninstall the Hybrid agent, re-run Hybrid Configuration Wizard from the same computer you performed the installation against and select **Classic Connectivity**. This will uninstall and unregister the Hybrid agent from the computer and Azure. After unregistering the Hybrid agent you can resume setup and configure hybrid in classic mode.
