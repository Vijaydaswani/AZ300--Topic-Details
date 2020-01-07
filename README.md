# AZ300--Topic-Details

Analyze resource utilization and consumption
Configure diagnostic settings on resources
https://docs.microsoft.com/en-us/azure/azure-monitor/platform/diagnostic-logs-overview#diagnostic-settings
Resource logs - these logs come from Azure services that deploy resources within an Azure subscription, such as Network Security Groups or Storage Accounts.
Resource diagnostic logs are configured using resource diagnostic settings. Tenant diagnostic logs are configured using a tenant diagnostic setting.
Where diagnostic logs and metrics are sent (Storage Account, Event Hubs, and/or Log Analytics).
Which log categories are sent and whether metric data is also sent.
How long each log category should be retained in a storage account. A retention of zero days means logs are kept forever. Otherwise, the value can be any number of days.
Collection of diagnostic logs can be enabled as part of creating a resource in a Resource Manager template or after a resource is created from that resource's page in the portal. You can also enable collection at any point using Azure PowerShell or CLI commands, or using the Azure Monitor REST API.
Create baseline for resources
https://docs.microsoft.com/en-us/azure/azure-monitor/platform/alerts-dynamic-thresholds
Azure portal -> Monitor -> Alerts -> New alert rule
Metric Alert with Dynamic Thresholds detection uses ML to learn metrics' historical behavior, identify patterns and anomalies.
Threshold setting - sensitivity controls the amount of deviation from metric behavior for alert. Sensitivity (High/Medium/Low)
Operator setting - trigger when Lower than lower threshold; Greater than upper threshold; Greater than the upper threshold or lower than the lower threshold (default)
Create and raise alerts
https://docs.microsoft.com/en-us/azure/azure-monitor/platform/alerts-metric
Azure portal -> Monitor -> Alerts -> New alert rule
Metric alerts in Azure Monitor provide a way to get notified when one of your metrics cross a threshold. Metric alerts work on a range of multi-dimensional platform metrics, custom metrics, Application Insights standard and custom metrics.
az monitor metrics alert create -n {nameofthealert} -g {ResourceGroup} --scopes {VirtualMachineResourceID} --condition "avg Percentage CPU > 90" --description {descriptionofthealert}
https://docs.microsoft.com/en-us/azure/azure-monitor/platform/alerts-classic-portal
Classic metric alerts in Azure Monitor provide a way to get notified when one of your metrics cross a threshold. Classic metric alerts is an older functionality that allows for alerting only on non-dimensional metrics. There is an existing newer functionality called Metric alerts which has improved functionality over classic metric alerts.
In the portal, locate the resource that you want to monitor, and then select it. In the MONITORING section, select Alerts (Classic).
az monitor alert create --name <alert name> --resource-group <group name> --action email <email1 email2 ...> --action webhook <URI> --target <target object ID> --condition "<METRIC> {>,>=,<,<=} <THRESHOLD> {avg,min,max,total,last} ##h##m##s"
After you create an alert, you can select it and do one of the following tasks:
View a graph that shows the metric threshold and the actual values from the previous day.
Edit or delete it.
Disable or Enable it if you want to temporarily stop or resume receiving notifications for that alert.
Analyze alerts across subscription
https://docs.microsoft.com/en-us/azure/azure-monitor/platform/alerts-metric
In the Manage rules blade, you can view all your alert rules across subscriptions. You can further filter the rules using Resource group, Resource type and Resource. If you want to see only metric alerts, select Signal type as Metrics.
Analyze metrics across subscription
https://docs.microsoft.com/en-us/azure/azure-monitor/platform/metrics-charts
If you have more than one Azure subscription, Metrics Explorer pulls out the resources across all subscriptions that are selected in the Portal Settings -> Filter by subscriptions list.
Create action groups
https://docs.microsoft.com/en-us/azure/azure-monitor/platform/action-groups
An action group is a collection of notification preferences defined by the owner of an Azure subscription. Azure Monitor and Service Health alerts use action groups to notify users that an alert has been triggered. Various alerts may use the same action group or different action groups depending on the user's requirements.
Email / SMS / Push / Voice / Function / LogicApp / Webhook / ITSM / Runbook
Monitor for unused resources
https://docs.microsoft.com/en-us/azure/advisor/advisor-overview
Azure Advisor is a service that, among other things, identifies virtual machines with low utilization from a CPU or network usage standpoint. From there, you can decide to either shut down or resize the machine based on the estimated cost to continue running the machines. Advisor also provides recommendations for reserved instance purchases. The recommendations are based on your last 30 days of virtual machine usage. When acted on, the recommendations can help you reduce your spending.
Monitor spend
https://docs.microsoft.com/en-us/azure/billing/billing-getting-started#ways-to-monitor-your-costs-when-using-azure-services
You can use tags to group billing data for supported services. The tags show up throughout different cost reporting views.
Use billing API to programmatically get usage data. Use the RateCard API and the Usage API together to get your billed usage.
https://docs.microsoft.com/en-us/azure/billing/billing-getting-started#costs
You can see the current spend and burn rate in Azure portal.
Azure Portal -> Subscriptions -> see the cost breakdown and burn rate -> Cost analysis see the cost breakdown by resource. Wait 24 hours for the data to populate.
You can filter by different properties like tags, resource type, resource group, and timespan. You can download csv.
Report on spend
https://docs.microsoft.com/en-us/azure/billing/billing-download-azure-invoice-daily-usage-date#download-usage
Download usage as an EA customer, Azure portal -> Cost Management + Billing -> Usage + charges
https://docs.microsoft.com/en-us/azure/billing/billing-understand-your-bill-ea#review-charges
You must be an Enterprise Administrator, Enterprise portal -> Reports -> Usage Summary
Utilize Log Search query functions
https://docs.microsoft.com/en-us/azure/azure-monitor/log-query/log-query-overview
https://docs.microsoft.com/en-us/azure/azure-monitor/log-query/functions
https://docs.microsoft.com/en-us/azure/azure-monitor/log-query/portals
Azure portal -> Monitor -> Logs -> Log Analytics
Demo environment - https://portal.loganalytics.io/demo
Log data collected by Azure Monitor is stored in a Log Analytics workspace, which is based on Azure Data Explorer.
To use an query with another query you can save it as a function. This allows you to simplify complex queries by breaking them into parts and allows you to reuse common code with multiple queries.
Azure portal -> Save -> Save as Function
MyFunction | where Title contains "SQL"
View alerts in Log Analytics
https://docs.microsoft.com/en-us/azure/azure-monitor/platform/alerts-overview#all-alerts-page
Notify you when important conditions are found in your monitoring data. Azure Monitor, which now includes Log Analytics and Application Insights. Not classic alerts.
Alert Rule -> Target+Metric+Treshold calls action-group+actions and monitor-condition+alert-state
Create and configure storage accounts
Configure network access to the storage account
https://docs.microsoft.com/en-us/azure/storage/common/storage-network-security
Configure storage accounts to deny access to traffic from all networks (including internet traffic) by default. Then grant access to traffic from specific VNets. This configuration enables you to build a secure network boundary for your applications. You can also grant access to public internet IP address ranges, enabling connections from specific internet or on-premises clients.
When network rules are configured, only applications requesting data from over the specified set of networks can access a storage account.
Network rules are enforced on all network protocols to Azure storage, including REST and SMB. To access the data with tools like Azure portal, Storage Explorer, and AZCopy, explicit network rules are required.
Virtual machine disk traffic (including mount and unmount operations, and disk IO) is not affected by network rules.
There are some cases where exceptions must be granted to enable full functionality. You can configure storage accounts with exceptions for trusted Microsoft services, and for access to storage analytics data.
az storage account update --resource-group "myresourcegroup" --name "mystorageaccount" --bypass Logging Metrics AzureServices
https://azure.microsoft.com/en-us/blog/virtual-network-service-endpoints-and-firewalls-for-azure-storage-now-generally-available/
To enable VNet protection, first enable service endpoints for storage in the VNet. Virtual Network Service Endpoints allow you to secure your critical Azure service resource to only your virtual network. Service endpoints also provide optimal routing for Azure traffic over the Azure backbone in scenarios where Internet traffic is routed through virtual appliances or on-premises.
On the storage account you can select to allow access to one or more VNets. You may also configure to allow access to one or more public IP ranges.
Create and configure storage account
https://docs.microsoft.com/en-us/azure/storage/common/storage-quickstart-create-account?tabs=azure-portal
az storage account create --name storagequickstart --resource-group storage-quickstart-resource-group --location westus --sku Standard_LRS --kind StorageV2
New-AzStorageAccount -ResourceGroupName $resourceGroup -Name "storagequickstart" -Location $location -SkuName Standard_LRS -Kind StorageV2
Generate shared access signature
https://docs.microsoft.com/en-us/azure/vs-azure-tools-storage-explorer-blobs#get-the-sas-for-a-blob-container
Right-click the desired blob container, and - from the context menu - select Get Shared Access Signature.
Install and use Azure Storage Explorer
https://azure.microsoft.com/en-us/features/storage-explorer/
https://docs.microsoft.com/en-us/azure/vs-azure-tools-storage-manage-with-storage-explorer?tabs=windows
Easily manage Storage anywhere from Windows, macOS, and Linux
Access multiple accounts and subscriptions across Azure, Azure Stack, and the sovereign Cloud
Create, delete, view, and edit storage resources
View and edit Blob, Queue, Table, File, Cosmos DB storage and Data Lake Storage
Obtain shared access signature (SAS) keys
Available for Windows, Mac, and Linux
Gain easy access to manage your virtual machine disks
Work with either Azure Resource Manager or classic storage accounts, plus manage and configure cross-origin resource sharing (CORS) rules.
Manage access keys
https://docs.microsoft.com/en-us/azure/storage/common/storage-dotnet-shared-access-signature-part-1
Account key and Shared access signatures (SAS). Your storage account includes both a primary and secondary access key, both of which grant administrative access to your account, and all resources within it. Exposing either of these keys opens your account to the possibility of malicious or negligent use. Shared access signatures provide a safe alternative that allows clients to read, write, and delete data in your storage account according to the permissions you've explicitly granted, and without need for an account key.
A shared access signature provides delegated access to resources in your storage account. With a SAS, you can grant clients access to resources in your storage account, without sharing your account keys. This is the key point of using shared access signatures in your applications--a SAS is a secure way to share your storage resources without compromising your account keys.
Your storage account key is similar to the root password for your storage account. Always be careful to protect your account key. Avoid distributing it to other users, hard-coding it, or saving it anywhere in plaintext that is accessible to others. Regenerate your account key using the Azure portal if you believe it may have been compromised.
A SAS gives you granular control over the type of access you grant to clients who have the SAS, including:
The interval over which the SAS is valid, including the start time and the expiry time.
The permissions granted by the SAS. For example, a SAS for a blob might grant read and write permissions to that blob, but not delete permissions.
An optional IP address or range of IP addresses from which Azure Storage will accept the SAS. For example, you might specify a range of IP addresses belonging to your organization.
The protocol over which Azure Storage will accept the SAS. You can use this optional parameter to restrict access to clients using HTTPS.
You can create two types of shared access signatures:
Service SAS. The service SAS delegates access to a resource in just one of the storage services: the Blob, Queue, Table, or File service.
Account SAS. The account SAS delegates access to resources in one or more of the storage services. All of the operations available via a service SAS are also available via an account SAS. Additionally, with the account SAS, you can delegate access to operations that apply to a given service, such as Get/Set Service Properties and Get Service Stats. You can also delegate access to read, write, and delete operations on blob containers, tables, queues, and file shares that are not permitted with a service SAS.
Monitor activity log by using Log Analytics
https://docs.microsoft.com/en-us/azure/azure-monitor/platform/collect-activity-logs
Activity Log is a log that offers insights into the operations performed on resources in your subscriptions
Activity Log, you can determine the what, who, and when for any write operations (PUT, POST, DELETE) made for the resources in your subscription.
https://docs.microsoft.com/en-us/rest/api/storageservices/enabling-storage-logging-and-accessing-log-data
Storage Logging and Accessing Log - record details for both successful and failed requests in your storage account. These logs enable you to see details of read, write, and delete operations against your Azure tables, queues, and blobs. Enable you to see the reasons for failed requests such as timeouts, throttling, and authorization errors.
Implement Azure storage replication
https://docs.microsoft.com/en-us/azure/storage/common/storage-redundancy
LRS, ZRS, GRS, RA-GRS, Paired regions
RPO, RTO - https://docs.microsoft.com/en-us/azure/storage/common/storage-redundancy-grs#what-is-the-rpo-and-rto-with-grs
Create and configure a Virtual Machine (VM) for Windows and Linux
Configure high availability
https://docs.microsoft.com/en-us/azure/virtual-machines/linux/manage-availability
Protects against: Unplanned Hardware Maintenance Event (Live Migration pauses for short time), An Unexpected Downtime (reboot, loss of the temporary drive), Planned Maintenance events (performed without any impact - sometimes updates require a planned reboot of VM in the suitable time window)
Recommended high availability best practices
Configure multiple virtual machines in an availability set for redundancy Group two or more virtual machines in an availability set. -> ensures that at least one virtual machine is available and meets the 99.95% SLA. Avoid leaving a single instance virtual machine in an availability set by itself. Each VM in availability set is assigned an update domain (five by default) and a fault domain (2-3). The order of update domains being rebooted may not proceed sequentially during planned maintenance, but only one update domain is rebooted at a time. Fault domains define the group of virtual machines that share a common power source and network switch. Default, the virtual machines from availability set are separated across up to 2-3 fault domains.
Use managed disks for VMs in an availability set Managed disks better reliability for Availability Sets. Ensuring that the disks of VMs in an Availability Set are isolated from each other. Automatically placing the disks in different storage fault domains (storage clusters) and aligning them with the VM fault domain.
For unmanaged disks
Keep all disks (OS and data) associated with a VM in the same storage account.
Review the limits on the number of unmanaged disks in a Storage account (performance reasons).
Use separate storage account for each VM in an Availability Set
Use scheduled events to proactively respond to VM impacting events VM is notified about upcoming maintenance events that can impact VM (requires subscription of events from inside of VM). Customers can use the event to perform tasks prior to the maintenance, such as saving state, failing over to the secondary, and so on. After you complete your logic for gracefully handling the maintenance event, you can approve the outstanding scheduled event to allow the platform to proceed with maintenance.
Configure each application tier into separate availability sets If you place two different tiers in the same availability set, all virtual machines in the same application tier can be rebooted at once. By configuring at least two virtual machines in an availability set for each tier, you guarantee that at least one virtual machine in each tier is available.
Combine a load balancer with availability sets Placing multiple virtual machines of the same tier under the same load balancer and availability set enables traffic to be continuously served by at least one instance.
Use availability zones to protect from datacenter level failures Availability zones, are alternative to availability sets. An Availability Zone is a physically separate zone within an Azure region. Three Availability Zones per supported region. Each Availability Zone has a distinct power source, network, and cooling. By architecting your solutions to use replicated VMs in zones, you can protect your apps and data from the loss of a datacenter. If one zone is compromised, then replicated apps and data are instantly available in another zone. There is no additional cost for virtual machines deployed in an Availability Zone. 99.99% VM uptime SLA is offered when two or more VMs are deployed across two or more Availability Zones within an Azure region. for i in `seq 1 3`; do az vm create --resource-group myResourceGroupSLB --name myVM$i --nics myNic$i --image UbuntuLTS --generate-ssh-keys --zone $i --custom-data cloud-init.txt az storage account create -n <accountname> -g <resourcegroup> -l <region> –sku Standard_ZRS –kind StorageV2
Configure monitoring, networking, storage, and virtual machine size
https://docs.microsoft.com/en-us/azure/virtual-machines/linux/tutorial-monitoring
You can enable boot diagnostics, performance metrics and manage package updates
Boot diagnostic captures boot output and stores it in Azure storage - troubleshoot VM boot issues
View boot diagnostic az vm boot-diagnostics get-boot-log --resource-group myResourceGroupMonitor --name myVM
VM Metrics are automatically collected for the host and can be viewed in the Azure portal.
To see more granular and VM-specific metrics, you need to install the Azure diagnostics extension on the VM. Enable guest-level monitoring in Azure portal. You can view these performance metrics and create alerts based on how the VM performs.
Update management allows you to manage updates and patches for your Azure VMs. Directly from your VM, you can quickly assess the status of available updates, schedule installation of required updates, and review deployment results to verify updates were applied successfully to the VM.
You can collect and view inventory for software, files, Linux daemons, Windows Services, and Windows registry keys on your computers. Tracking the configurations of your machines can help you pinpoint operational issues across your environment and better understand the state of your machines.
You can do more advanced monitoring of your VM by using a solution like Azure Monitor for VMs.
https://docs.microsoft.com/en-us/azure/virtual-machines/linux/network-overview
VM can have multiple NICs, and can be added or removed through the lifecycle of a VM.
Public / Private IP Address / Static / Dynamic
VNET / Subnet / NSG / LB
https://docs.microsoft.com/en-us/azure/virtual-machines/linux/tutorial-manage-disks
Operating system disk - Disk caching configuration optimized for OS performance. Because of this the OS disk should not be used for applications or data.
Temporary disk - SSD of the VM host. Highly performant may be used for temporary data processing. Data can be lost.
Datadisk can be added
Standard disk and Premium disk
az vm create --resource-group myResourceGroupDisk --name myVM --image UbuntuLTS --size Standard_DS2_v2 --generate-ssh-keys --data-disk-sizes-gb 128 128
The operating system needs to be configured to use additional disks
You can take a disk snapshot. Read only, point-in-time copy of the disk to quickly save the state of a VM before configuration changes. VM can be restored using a snapshot. Snapshot is taken of each disk independently.
az snapshot create --resource-group myResourceGroupDisk --source "$osdiskid" --name osDisk-backup
https://docs.microsoft.com/en-us/azure/virtual-machines/linux/tutorial-manage-vm#understand-vm-sizes
az vm list-sizes --location eastus
az vm create --resource-group myResourceGroupVM --name myVM3 --image UbuntuLTS --size Standard_F4s --generate-ssh-keys
Deploy and configure scale sets
https://docs.microsoft.com/en-us/azure/virtual-machine-scale-sets/
Let you create and manage a group of identical, load balanced, and autoscaling VMs.
Can scale VMs in the scale set manually, or rules to autoscale on resource usage like CPU, memory or network traffic.
https://docs.microsoft.com/en-us/azure/virtual-machine-scale-sets/quick-create-portal
Azure portal -> Create Virtual machine scale set -> Name; OS Type; Resource Group; User Name and Credentials or SSH Keys; Location; Instances count and VM size
Load balancer is created. NAT rules are used for remote connectivity such as RDP or SSH. E.g. VM1 104.42.1.19:50001, VM2 104.42.1.19:50002
az vmss create --resource-group myResourceGroup --name myScaleSol tcp
az monitor autoscale create --resource-group myResourceGroup --resource myScaleSet --resource-type Microsoft.Compute/virtualMachineScaleSets --name autoscale --min-count 2 --max-count 10 --count 2
az monitor autoscale rule create --resource-group myResourceGroup --autoscale-name autoscale --condition "Percentage CPU > 70 avg 5m" --scale out 3
az monitor autoscale rule create --resource-group myResourceGroup --autoscale-name autoscale --condition "Percentage CPU < 30 avg 5m" --scale in 1
Zone-redundant scale set az vmss create --resource-group myResourceGroup --name myScaleSet --image UbuntuLTS --upgrade-policy-mode automatic --admin-username azureuser --generate-ssh-keys --zones 1 2 3
For PowerShell use cmdlets New-AzVmss, Add-AzVmssExtension
Automate deployment of Virtual Machines (VMs)
Modify Azure Resource Manager (ARM) template
https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-manager-export-template
https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-template-deploy-portal#deploy-resources-from-custom-template
https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-authoring-templates
Configure location of new VMs
https://docs.microsoft.com/en-us/azure/virtual-machines/windows/quick-create-cli#create-virtual-machine - az vm create --resource-group myResourceGroup --name myVM --image win2016datacenter --admin-username azureuser --admin-password myPassword12 --location EastUS
New-AzVm -ResourceGroupName "myResourceGroupVM" -Name "myVM" -Location "EastUS" -VirtualNetworkName "myVnet" -SubnetName "mySubnet" -SecurityGroupName "myNetworkSecurityGroup" -PublicIpAddressName "myPublicIpAddress" -Credential $cred
In the ARM template you can use "location": "EastUS"
Configure VHD template
TODO
Deploy from template
TODO
Save a deployment as an ARM template
TODO
Deploy Windows and Linux VMs
TODO
Create connectivity between virtual networks
Create and configure VNET peering
TODO
Create and configure VNET to VNET
TODO
Verify virtual network connectivity
TODO
Create virtual network gateway
TODO
Implement and manage virtual networking
Configure private and public IP addresses, network routes, network interface, subnets, and virtual network
TODO
Manage Azure Active Directory (AD)
Add custom domains
https://docs.microsoft.com/en-us/azure/active-directory/fundamentals/add-custom-domain
Initial domain name, domainname.onmicrosoft.com. You can't change or delete
You must create your domain name with a domain registrar. You must include .com, .net, or any other top-level extension
Azure Portal -> AAD -> Custom domain names -> Add custom domain -> Add domain
Unverified domain is added and the page showing you your DNS info
You must return to your domain registrar and add the Azure AD DNS information from your copied TXT file. Creating this TXT record for your domain "verifies" ownership of your domain name
Set the TTL (time to live) to 3600 seconds (60 minutes), and then save the information
On the page, select Verify to make sure your custom domain is properly registered and is valid for Azure AD
Configure Azure AD Identity Protection
https://docs.microsoft.com/en-us/azure/active-directory/identity-protection/overview
Azure Portal -> Marketplace -> Azure AD Identity Protection -> Create
Feature of the Azure AD Premium P2 edition
https://docs.microsoft.com/en-us/azure/active-directory/identity-protection/enable
Get a consolidated view of flagged users and risk events detected using machine learning algorithms
Set risk-based Conditional Access policies to automatically protect your users
Improve security posture by acting on vulnerabilities
Configure Azure AD Join
https://docs.microsoft.com/en-us/azure/active-directory/devices/hybrid-azuread-join-managed-domains
https://aadguide.azurewebsites.net/aadjoin/
Seamless SSO + ( Azure AD join, Hybrid Azure AD join (Azure AD Connect), Azure AD registration )
Azure AD Connect -> Configure -> Configure device options -> Hybrid Azure AD join
To register Windows down-level devices, you need to download and install the Windows Installer package (.msi) from Download Center on the Microsoft Workplace Join for non-Windows 10 computers page.
Configure Azure AD Enterprise State Roaming
https://docs.microsoft.com/en-us/azure/active-directory/devices/enterprise-state-roaming-enable
Enterprise State Roaming is available to any organization with an Azure AD Premium or Enterprise Mobility + Security (EMS) license.
Azure Portal -> AAD -> Devices -> Enterprise State Roaming -> Select Users may sync settings and app data across devices
For a Windows 10 device to use the Enterprise State Roaming service, the device must authenticate using an Azure AD identity. For devices that are joined to Azure AD, the user’s primary sign-in identity is their Azure AD identity, so no additional configuration is required. For devices that use on-premises Active Directory, the IT admin must Configure hybrid Azure Active Directory joined devices.
Configure self-service password reset
https://docs.microsoft.com/en-us/azure/active-directory/authentication/tutorial-sspr-pilot
https://docs.microsoft.com/en-us/azure/active-directory/authentication/howto-sspr-deployment
https://docs.microsoft.com/en-us/azure/active-directory/authentication/concept-sspr-howitworks
Self-Service Password Reset/Change/Unlock with on-premises writeback is a premium feature of Azure AD.
Standalone Office 365 licensing plans don't support "Self-Service Password Reset/Change/Unlock with on-premises writeback"
Self-service password reset portal located at https://aka.ms/ssprsetup
Self-service password reset portal https://aka.ms/sspr
Azure Portal -> AAD -> Password reset -> Properties -> Self Service Password Reset Enabled
Azure Portal -> AAD -> Password reset -> Authentication methods -> Number of methods required to reset to 2
Azure Portal -> AAD -> Password reset -> Notifications (Notify users on password resets, Notify all admins when other admins reset their password), Registration (Require users to register when signing in), Customization (Customize helpdesk link)
Implement conditional access policies
https://docs.microsoft.com/en-gb/azure/active-directory/conditional-access/app-based-mfa#create-your-conditional-access-policy
Azure Portal -> AAD -> Security section -> Conditional Access -> New policy -> Select user/groups; select app; Grant access/Require multi-factor authentication -> Enable policy
Manage multiple directories
https://docs.microsoft.com/en-us/azure/active-directory/fundamentals/active-directory-access-create-new-tenant#create-a-new-tenant-for-your-organization
Azure Portal -> Create Azure Active Directory (Organization name, domain name, region)
Perform an access review
https://docs.microsoft.com/en-gb/azure/active-directory/governance/access-reviews-overview
To use access reviews, you must have one of the following licenses:
Azure AD Premium P2
Enterprise Mobility + Security (EMS) E5 license
Azure Portal -> Create Access Reviews -> Onboard -> Create (select directory)
https://docs.microsoft.com/en-gb/azure/active-directory/governance/create-access-review
Access to groups and applications for employees and guests changes over time. To reduce the risk associated with stale access assignments, administrators can use Azure Active Directory (Azure AD) to create access reviews for group members or application access. If you need to routinely review access, you can also create recurring access reviews.
https://docs.microsoft.com/en-gb/azure/active-directory/governance/perform-access-review
Decide whether to have each user review their own access or to have one or more users review everyone's access.
When the access review starts, ask the reviewers to give input. By default, they each receive an email from Azure AD with a link to the access panel, where they review access to groups or applications.
Implement and manage hybrid identities
Install and configure Azure AD Connect
https://docs.microsoft.com/en-gb/azure/active-directory/hybrid/how-to-connect-install-custom
Configure federation and single sign-on
https://docs.microsoft.com/en-gb/azure/active-directory/hybrid/how-to-connect-fed-management#addfeddomain
https://docs.microsoft.com/en-gb/azure/active-directory/hybrid/whatis-fed
Federation is a collection of domains that have established trust. The level of trust may vary, but typically includes authentication and almost always includes authorization.
You can federate your on-premises environment with Azure AD and use this federation for authentication and authorization. This sign-in method ensures that all user authentication occurs on-premises.
Azure Active Directory (Azure AD) Connect lets you configure federation with on-premises Active Directory Federation Services (AD FS) and Azure AD. With federation sign-in, you can enable users to sign in to Azure AD-based services with their on-premises passwords and, while on the corporate network, without having to enter their passwords again.
Add a domain to be federated with Azure AD by using Azure AD Connect. Azure AD Connect adds the domain for federation and modifies the claim rules to correctly reflect the issuer when you have multiple domains federated with Azure AD.
https://docs.microsoft.com/en-gb/azure/active-directory/hybrid/how-to-connect-sso-quick-start
https://docs.microsoft.com/en-gb/azure/active-directory/hybrid/how-to-connect-sso
https://docs.microsoft.com/en-gb/azure/active-directory/hybrid/how-to-connect-pta
Azure Active Directory Seamless Single Sign-On (Azure AD Seamless SSO) automatically signs users in when they are on their corporate devices connected to your corporate network. When enabled, users don't need to type in their passwords to sign in to Azure AD, and usually, even type in their usernames.
Seamless SSO can be combined with either the Password Hash Synchronization or Pass-through Authentication sign-in methods. Seamless SSO is not applicable to Active Directory Federation Services (ADFS). Seamless SSO needs the user's device to be domain-joined, but doesn't need for the device to be Azure AD Joined.
At the User sign-in page (AD Connect), select the Enable single sign on option. Only if the Sign On method is Password Hash Synchronization or Pass-through Authentication.
Verify that the Seamless single sign-on feature appears as Enabled. Azure Portal -> Azure Active Directory -> Azure AD Connect -> Seamless single sign-on is Enabled
You start by adding the following Azure AD URL to all or selected users' Intranet zone settings by using Group Policy in Active Directory: https://autologon.microsoftazuread-sso.com
You need to enable an Intranet zone policy setting called Allow updates to status bar via script through Group Policy.
Manage Azure AD Connect
https://docs.microsoft.com/en-gb/azure/active-directory/hybrid/how-to-connect-configure-ad-ds-connector-account
https://docs.microsoft.com/en-gb/azure/active-directory/hybrid/concept-azure-ad-connect-sync-architecture
Manage password sync and writeback
https://docs.microsoft.com/en-us/azure/active-directory/authentication/concept-sspr-writeback
https://docs.microsoft.com/en-us/azure/active-directory/authentication/howto-sspr-writeback
Self-Service Password Reset/Change/Unlock with on-premises writeback is a premium feature of Azure AD.
Standalone Office 365 licensing plans don't support "Self-Service Password Reset/Change/Unlock with on-premises writeback"
https://docs.microsoft.com/en-us/azure/active-directory/authentication/concept-sspr-howitworks#write-back-passwords-to-your-on-premises-directory
If the switch is set to Yes, then writeback is enabled, and federated, pass-through authentication, or password hash synchronized users are able to reset their passwords.
Implement Workloads and Security (20-25%)
Migrate servers to Azure
Migrate by using Azure Site Recovery (ASR)
https://docs.microsoft.com/en-us/azure/site-recovery/migrate-tutorial-on-premises-azure#migrate-to-azure
Run a failover for the machines you want to migrate. Azure Portal -> ASR -> In Settings -> Replicated items click the machine -> Failover -> Select the latest recovery point.
Select Shut down machine before beginning failover.
Check that the Azure VM appears in Azure as expected
Azure Portal -> ASR -> In Settings -> Replicated items click the machine -> Complete Migration (stops Site Recovery billing for the VM)
Post-migration steps: Change connection strings and redirect onPrem communication, if not installed install Azure VM agent, Manually remove any Site Recovery provider/agent from the VM, change NSG, Add monitoring agent
Migrate using Physical to Virtual
https://docs.microsoft.com/en-us/azure/site-recovery/physical-azure-architecture
https://docs.microsoft.com/en-us/azure/site-recovery/physical-azure-disaster-recovery
Configuration server, Process server (part of Configuration server), Master target server (part of Configuration server), Mobility service (on source Physical machine)
Configure storage
https://azure.microsoft.com/es-es/blog/managed-disks-with-azure-site-recovery/
https://docs.microsoft.com/en-us/azure/site-recovery/vmware-azure-exclude-disk
By default, all disks on a machine are replicated. To exclude a disk from replication, you must manually install the Mobility service on the machine before you enable replication if you are replicating from VMware to Azure.
Create a backup vault
https://docs.microsoft.com/en-us/azure/site-recovery/tutorial-prepare-azure#create-a-recovery-services-vault
Prepare source and target environments
https://docs.microsoft.com/en-us/azure/site-recovery/physical-azure-set-up-source
Protection goal, Unified setup, use proxy if needed, ASR Key, install Configuration server, Process server, Master target server, set accounts
https://docs.microsoft.com/en-us/azure/site-recovery/vmware-azure-set-up-target
Select Subscription, Resource Manager model, ensure that you have at least one virtual network in the target subscription to replicate and failover your virtual machine or physical server to.
Backup and restore data
https://docs.microsoft.com/en-us/azure/backup/backup-azure-recovery-services-vault-overview
https://docs.microsoft.com/en-us/azure/backup/backup-azure-vms-first-look-arm
VM, Recovery Services vault, backup policy, Enable Backup
https://docs.microsoft.com/en-us/azure/backup/backup-azure-arm-restore-vms
Number of ways to restore a VM: Create a new VM (New VM name), Restore disk, Replace existing (replace a disk), Recover files
https://docs.microsoft.com/en-us/azure/backup/backup-azure-restore-files-from-vm
https://docs.microsoft.com/en-us/azure/backup/backup-instant-restore-capability
Using Recovery Services vaults, you can restore files and folders from an IaaS VM without restoring the entire VM, which enables faster restore times. Instant restore for IaaS VMs is available for both Windows and Linux VMs.
Deploy Azure Site Recovery (ASR) agent
https://docs.microsoft.com/en-us/azure/site-recovery/vmware-physical-mobility-service-overview
You install the Site Recovery Mobility service on each on-premises VMware VM and physical server. The Mobility service captures data writes on the machine, and forwards them to the Site Recovery process server.
Push installation (requires account for installing the service), Install manually (UI or command prompt), Automated deployment - E.g. System Center Configuration Manager.
Prepare virtual network
https://docs.microsoft.com/en-us/azure/site-recovery/tutorial-prepare-azure#set-up-an-azure-network
https://docs.microsoft.com/en-us/azure/site-recovery/site-recovery-manage-network-interfaces-on-premises-to-azure
Create standard VNET. It should not overlap with any existing network range.
Configure serverless computing
Create and manage objects
TODO
Manage a Logic App resource
https://docs.microsoft.com/en-us/azure/logic-apps/logic-apps-overview
Helps automate and orchestrate tasks, business processes, and workflows when you need to integrate apps, data, systems, and services
Scalable solutions for app integration, data integration, system integration, enterprise application integration (EAI), and business-to-business (B2B) communication, whether in the cloud, on premises, or both.
https://docs.microsoft.com/en-us/azure/logic-apps/quickstart-create-first-logic-app-workflow
Manage Azure Function app settings
https://docs.microsoft.com/en-us/azure/azure-functions/functions-how-to-use-azure-function-app-settings#settings
Settings blade where you configure and manage framework versions, remote debugging, app settings, and connection strings
Manage Event Grid
https://docs.microsoft.com/en-us/azure/event-grid/overview
Event Grid allows you to build applications with event-based architectures
Reactive programming / Event distribution (discrete) / React to status changes - The event data has information about what happened but doesn't have the data that triggered the event.
Select the Azure resource you would like to subscribe to, and then give the event handler or WebHook endpoint to send the event to
Event Grid has built-in support for events coming from Azure services
Also support for your own events, using custom topics.
Can use filters to route specific events to different endpoints, multicast to multiple endpoints, and make sure events are reliably delivered.
Events, Event sources, Topics, Event subscriptions, Event handlers
https://docs.microsoft.com/en-us/azure/event-grid/blob-event-quickstart-portal
Manage Service Bus
https://docs.microsoft.com/en-gb/azure/service-bus-messaging/service-bus-messaging-overview
High-value enterprise messaging / Message / Order processing and financial transactions
Service Bus is intended for traditional enterprise applications. These enterprise applications require transactions, ordering, duplicate detection, and instantaneous consistency.
When handling high-value messages that cannot be lost or duplicated, use Azure Service Bus.
reliable asynchronous message delivery, advanced messaging features like FIFO, batching/sessions, transactions, dead-lettering, temporal control, routing and filtering, and duplicate detection, at least once delivery, optional in-order delivery
https://docs.microsoft.com/en-gb/azure/service-bus-messaging/service-bus-create-namespace-portal
Implement application load balancing
Configure application gateway and load balancing rules
https://docs.microsoft.com/en-us/azure/application-gateway/overview
Web traffic load balancer, OSI L7, you can route traffic, Autoscaling, Zone redundancy, Static VIP, SSL offload, Connection draining, Custom error pages, Web application firewall, Redirection, Session affinity, Websocket and HTTP/2 traffic, Rewrite HTTP headers
https://docs.microsoft.com/en-us/azure/load-balancer/tutorial-load-balancer-port-forwarding-portal#create-a-load-balancer-rule
https://docs.microsoft.com/en-us/azure/load-balancer/load-balancer-overview
Load balancing, Port forwarding, Health probes, Outbound connections (SNAT)
Front-end IP configuration for incoming traffic, the back-end IP pool to receive the traffic, and the required source and destination ports.
Inbound network address translation (NAT) rule to forward traffic from a specific port of the front-end IP address to a specific port of a back-end VM.
az network lb create --resource-group myResourceGroupILB --name myLoadBalancer --frontend-ip-name myFrontEnd --private-ip-address 10.0.0.7 --backend-pool-name myBackEndPool --vnet-name myVnet --subnet
az network lb probe create --resource-group myResourceGroupILB --lb-name myLoadBalancer --name myHealthProbe --protocol tcp --port 80
az network lb rule create --resource-group myResourceGroupILB --lb-name myLoadBalancer --name myHTTPRule --protocol tcp --frontend-port 80 --backend-port 80 --frontend-ip-name myFrontEnd --backend-pool-name myBackEndPool --probe-name myHealthProbe
for i in `seq 1 2`; do az network nic create --resource-group myResourceGroupILB --name myNic$i --vnet-name myVnet --subnet mySubnet --lb-name myLoadBalancer --lb-address-pools myBackEndPool done
https://docs.microsoft.com/en-us/azure/load-balancer/load-balancer-outbound-rules-overview
https://docs.microsoft.com/bs-latn-ba/azure/load-balancer/configure-load-balancer-outbound-cli#create-outbound-rule
Outbound rules allow you to control which virtual machines should be translated to which public IP addresses.
az network lb outbound-rule create --resource-group myresourcegroupoutbound --lb-name lb --name outboundrule --frontend-ip-configs myfrontendoutbound --protocol All --idle-timeout 15 --outbound-ports 10000 --address-pool bepool
Implement front end IP configurations
az network lb frontend-ip create -g MyResourceGroup -n MyFrontendIp --lb-name MyLb --private-ip-address 10.10.10.100 --subnet MySubnet --vnet-name MyVnet
Manage application load balancing
https://dzone.com/articles/understanding-azure-load-balancing-solutions
Azure Load Balancer (External, Internal), Azure Application Gateway (External, Internal), Azure Traffic Manager (Global selector)
Integrate on premises network with Azure virtual network
Create and configure Azure VPN Gateway
https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-about-vpngateways
To send encrypted traffic between an Azure virtual network and an on-premises location over the public Internet. You can also use a VPN gateway to send encrypted traffic between Azure virtual networks over the Microsoft network. Each virtual network can have only one VPN gateway. However, you can create multiple connections to the same VPN gateway (Multisite/Route Based/Dynamic GW). When you create multiple connections to the same VPN gateway, all VPN tunnels share the available gateway bandwidth.
Type: Point-to-Site, Site-to-Site, VNet-to-VNet, VNet peering, ExpressRoute
SKU: Basic(Legacy), VpnGw1(650Mbps), VpnGw2(1Gbps), VpnGw3(1.25Gbps)
https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-tutorial-create-gateway-powershell
Public IP, Gateway Subnet, Gateway Ip Config + SKU/Type -> Creates GW
Create also Local network gateway (refers to on-premises location) -> My Public IP, My Addr onPrem space
S2S Connection -> GW + Local network gateway + Shared key PSK
In the Azure portal, you can view the connection status of a Resource Manager VPN Gateway by navigating to the connection
Create and configure site to site VPN
https://blogs.technet.microsoft.com/canitpro/2017/06/28/step-by-step-configuring-a-site-to-site-vpn-gateway-between-azure-and-on-premise/
https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal
Configure Express Route
https://docs.microsoft.com/en-us/azure/expressroute/expressroute-introduction/
Connect on-premises networks into the Microsoft cloud over a private connection facilitated by a connectivity provider (Azure, Office 365, and Dynamics 365)
More reliability, faster speeds, lower latencies, and higher security than typical connections over the Internet
Dynamic routing via BGP (to exchange routes), Built-in redundancy, Global connectivity or Region connectivity
Unlimited data, Metered data, ExpressRoute premium add-on
https://docs.microsoft.com/en-us/azure/expressroute/expressroute-howto-circuit-portal-resource-manager
ExpressRoute circuit is billed from the moment a service key is issued. Ensure that connectivity provider is ready to provision the circuit.
Provider, Peering location, Bandwidth, SKU, Billing model -> pass service key down to the service provider to complete the provisioning process
These instructions only for service providers that offer layer 2 connectivity services. For managed layer 3 (MPLS), your connectivity provider configures and manages routing for you.
Verify on premises connectivity
https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal#VerifyConnection
Azure portal -> virtual network gateway -> Connections -> Status is 'Succeeded' and 'Connected'
Manage on-premise connectivity with Azure
TODO
Manage role-based access control (RBAC)
Create a custom role
https://docs.microsoft.com/en-us/azure/role-based-access-control/custom-roles
Custom roles are stored in an Azure Active Directory (Azure AD) directory and can be shared across subscriptions
Create a custom role with a JSON template, add changes, and create a new role
AssignableScopes, Actions, NotActions
az role definition create --role-definition ~/roles/vmoperator.json
Configure access to Azure resources by assigning roles
https://docs.microsoft.com/en-us/azure/role-based-access-control/role-assignments-portal
Configure management access to Azure
TODO
Troubleshoot RBAC
https://docs.microsoft.com/en-us/azure/role-based-access-control/troubleshooting
Implement RBAC policies
https://docs.microsoft.com/en-us/azure/governance/policy/overview
Policy focuses on resources during deployment and for already existing resources. Policy controls properties such as the types or locations of resources. Unlike RBAC, Policy is a default allow and explicit deny system.
Creating and implementing a policy begins with policy definition. Policy definition has conditions under which it's enforced. And, it has a defined effect that takes place if the conditions are met.
A policy assignment is a policy definition that has been assigned to specific scope. This scope could range from a management group to a resource group.
Scope refers to resource groups, subscriptions, or management groups.
Policy assignments are inherited by all child resources to resources in resource group. You can exclude a subscope from the policy assignment.
For example, at the subscription scope, you can assign a policy that prevents the creation of networking resources. You could exclude a resource group in that subscription that is intended for networking infrastructure. You then grant access to this networking resource group to users that you trust with creating networking resources.
https://docs.microsoft.com/en-us/azure/governance/policy/assign-policy-portal
Assign RBAC roles
https://docs.microsoft.com/en-us/azure/role-based-access-control/role-assignments-portal
Implement Multi-Factor Authentication (MFA)
Enable MFA for an Azure tenant
https://docs.microsoft.com/en-us/azure/active-directory/authentication/howto-mfa-getstarted
Requires global administrator account in Azure AD tenant.
Correct licenses assigned to usershe most flexible way to enable two-step verification for your users
Enabled by Azure AD Identity Protection - uses the Azure AD Identity Protection risk policy to require two-step verification based only on sign-in risk for all cloud applications
Enabled by changing user state - requires users to perform two-step verification every time they sign in and overrides conditional access policies
Enable at least one authentication method (best is Microsoft Authenticator)
Ask users to enroll https://aka.ms/mfasetup (ask users to register authentication methods beforehand)
Step 1: Azure Portal -> AAD -> Users -> Multi-Factor Authentication -> service settings -> verification options, check all of the boxes for methods available to users -> save
Step 2: Azure Portal -> AAD -> Conditional access -> New policy -> Include/Exclude users/groups, choose optionally conditions -> Grant Require multi-factor authentication -> Enable policy -> Create
Configure user accounts for MFA
See above.
Configure fraud alerts
https://docs.microsoft.com/en-us/azure/active-directory/authentication/howto-mfa-mfasettings#fraud-alert
Users can report fraudulent attempts to access their resources. Users can report fraud attempts by using the mobile app or through their phone. This feature is specific to MFA Server (on-premises).
Azure Portal -> AAD -> MFA -> Fraud alert -> Set the Allow users to submit fraud alerts setting to On -> Save
Options
Block user when fraud is reported (for 90 days or unblocked by Administrator)
Code to report fraud during initial greeting - phone call to perform two-step verification. To report fraud, the user enters a code before pressing #
View fraud reports: Azure Portal -> AAD -> Sign-ins
Configure bypass options
https://docs.microsoft.com/en-us/azure/active-directory/authentication/howto-mfa-mfasettings#one-time-bypass
One-time bypass - Allows a user to authenticate a single time without performing two-step verification. (temporary and expires after a specified number of seconds). The user needs to sign in before the one-time bypass expires.
Azure Active Directory -> MFA -> One-time bypass -> Add, username as username@domain.com enter the number of seconds and reason.
View one-time bypass reports: Azure Portal -> AAD -> MFA -> One-time bypass
Configure trusted IPs
https://docs.microsoft.com/en-us/azure/active-directory/authentication/howto-mfa-mfasettings#trusted-ipss
Select -> For requests from a specific range of public IPs -> enter CIDR
Or Select -> For requests from federated users originating from my intranet (All federated users who sign in from the corporate network bypass two-step verification by using a claim that is issued by AD FS)
Save
Step 3: Azure Portal -> AAD -> MFA -> service settings -> Configure MFA trusted IPs
Select -> For requests from a specific range of public IPs -> enter CIDR
Or Select -> For requests from federated users originating from my intranet (All federated users who sign in from the corporate network bypass two-step verification by using a claim that is issued by AD FS)
Save
Configure verification methods
https://docs.microsoft.com/en-us/azure/active-directory/authentication/howto-mfa-mfasettings#verification-methods
When your users enroll for MFA, they choose their preferred verification method from enabled options.
Call to phone - user answers the call and presses #
Text message to phone - Sends a text message that contains a verification code.
Notification through mobile Microsoft Authenticator app - Sends a push notification to your device. The user views the notification and selects Verify to complete verification.
Verification code from mobile app or hardware token - Microsoft Authenticator app generates a new OATH verification code every 30 seconds
Azure Portal -> AAD -> Users and groups -> All users -> Multi-Factor Authentication -> service settings -> verification options -> select/unselect the methods -> Save
Create and Deploy Apps (5-10%)
Create web apps by using PaaS
Create an Azure App Service Web App
https://www.c-sharpcorner.com/blogs/stepbystep-guide-to-creating-a-web-app-on-azure-portal
Create documentation for the API
https://docs.microsoft.com/en-us/azure/azure-functions/functions-openapi-definition#generate-the-openapi-definition
https://blogs.msdn.microsoft.com/appserviceteam/2017/03/30/announcing-functions-swagger-support/
https://lightbuzz.com/swagger-azure-step-by-step/
https://www.hakantuncer.com/2018/09/16/api-versioning-with-swagger-azure-api-management-services-and-asp-net-core-a-frictionless-devops-experience/
https://developers.de/blogs/damir_dobric/archive/2015/04/10/how-to-activate-swagger-in-your-api-app.aspx
Create an App Service Web App for containers
https://dzone.com/articles/why-azure-web-app-on-linux-is-huge
https://azure.microsoft.com/en-us/blog/general-availability-of-app-service-on-linux-and-web-app-for-containers/
https://docs.microsoft.com/en-us/azure/app-service/containers/app-service-linux-ci-cd
Windows (Windows Server Container, docker hub, ACR, private registry, no docker compose support, no Kubernetes support)
Linux (same as above + docker compose support, Kubernetes support)
Application Insights
Create an App Service background task by using WebJobs
https://docs.microsoft.com/en-us/azure/app-service/webjobs-create#CreateContinuous
No additional cost to use WebJobs, not yet supported for App Service on Linux
Continuous, Triggered (manual, scheduled)
If your app runs continuous or scheduled WebJobs, enable Always On to ensure that the WebJobs run reliably (time out after 20 minutes of inactivity)
exe, cmd, PowerShell, Bash, PHP, Python, Node, Java
Enable diagnostics logging
https://docs.microsoft.com/en-us/azure/app-service/troubleshoot-diagnostic-logs#enablediag
Settings -> Diagnostics logs -> Level (Disabled, Error, Warning, Information, Verbose)
File system option temporarily for debugging purposes. This option turns off automatically in 12 hours.
Design and develop apps that run in containers
Configure diagnostic settings on resources
TODO
Create a container image by using a Docker file
TODO
Create an Azure Container Service (ACS/AKS)
https://stackify.com/azure-container-service-kubernetes/
Publish an image to the Azure Container Registry
https://docs.microsoft.com/en-us/azure/container-registry/container-registry-get-started-docker-cli
An Azure container registry stores and manages private Docker container images, similar to the way Docker Hub stores public Docker images. You can use the Docker command-line interface (Docker CLI) for login, push, pull, and other operations on your container registry.
az acr login --name myregistry (preffered) or docker login myregistry.azurecr.io
docker pull nginx
docker run -it --rm -p 8080:80 nginx
docker tag nginx myregistry.azurecr.io/samples/nginx
docker push myregistry.azurecr.io/samples/nginx
docker pull myregistry.azurecr.io/samples/nginx
docker run -it --rm -p 8080:80 myregistry.azurecr.io/samples/nginx
Implement an application that runs on an Azure Container Instance
https://docs.microsoft.com/en-us/azure/container-instances/container-instances-quickstart-portal
Manage container settings by using code
https://mikepfeiffer.io/azure-docker-containers.html
Implement Authentication and Secure Data (5-10%)
Implement authentication
Implement authentication by using certificates, forms-based authentication, tokens, or Windows-integrated authentication
https://docs.microsoft.com/en-us/azure/app-service/app-service-web-configure-tls-mutual-auth
az webapp update --set clientCertEnabled=true --name <app_name> --resource-group <group_name>
App Service injects an X-ARR-ClientCert request header with the client certificate
https://docs.microsoft.com/en-us/dotnet/framework/security/how-to-build-claims-aware-aspnet-web-forms-app-using-wif
https://docs.microsoft.com/en-us/dotnet/framework/security/claims-aware-aspnet-app-forms-authentication
https://docs.microsoft.com/en-us/azure/app-service/overview-authentication-authorization
authentication and authorization module: Authenticates users with the specified provider; Validates, stores, and refreshes tokens; Manages the authenticated session; Injects identity information into request headers
App Service uses federated identity, in which a third-party identity provider manages the user identities and authentication flow for you.
Azure Active Directory | Microsoft Account | Facebook | Google | Twitter
User claims - For all language frameworks, App Service makes the user's claims available to your code by injecting them into the request headers. For ASP.NET 4.6 apps, App Service populates ClaimsPrincipal.Current with the authenticated user's claims,
Token store - App Service provides a built-in token store, which is a repository of tokens that are associated with the users of your web apps, APIs, or native mobile apps. When you enable authentication with any provider, this token store is immediately available to your app. If your application code needs to access data from these providers on the user's behalf,
https://docs.microsoft.com/en-us/dotnet/framework/security/how-to-build-claims-aware-aspnet-app-using-windows-authentication
<authentication mode="Windows" />
Implement multi-factor authentication by using Azure AD
https://docs.microsoft.com/en-us/azure/active-directory/conditional-access/app-based-mfa
Implement OAuth2 authentication
https://docs.microsoft.com/en-us/azure/api-management/api-management-howto-protect-backend-with-aad
https://docs.microsoft.com/en-us/azure/app-service/configure-authentication-provider-aad
Register an application (backend-app) in Azure AD to represent the API.
Register another application (client-app) in Azure AD to represent a client application that needs to call the API.
In Azure AD, grant permissions to allow the client-app to call the backend-app.
Configure the Developer Console to use OAuth 2.0 user authorization.
Add the validate-jwt policy to validate the OAuth token for every incoming request.
Implement Managed Service Identity (MSI) Service Principal authentication
https://blogs.msdn.microsoft.com/benjaminperkins/2018/06/13/using-managed-service-identity-msi-with-and-azure-app-service-or-an-azure-function/
Implement secure data solutions
Encrypt and decrypt data at rest and in transit
https://cloudacademy.com/blog/how-does-azure-encrypt-data/
Data written to Azure Blob storage is encrypted when placed on disk, TDE, KeyVault, Azure Key Vault managed encryption is enabled by default on managed disks
All sessions with Azure services and data centers are secured using the Transport Layer Security (TLS) cryptographic protocol and Forward Secrecy (also known as Perfect Forward Secrecy or PFS), a key agreement protocol
Encrypt data with Always Encrypted
https://azure.microsoft.com/en-us/blog/transparent-data-encryption-or-always-encrypted/
https://docs.microsoft.com/en-us/azure/sql-database/sql-database-always-encrypted-azure-key-vault#encrypt-columns-configure-always-encrypted
TDE is intended to add a layer of security to protect data at rest from offline access to raw files or backups, common scenarios include datacenter theft or unsecured disposal of hardware or media such as disk drives and backup tapes.
Always Encrypted is a feature designed to protect sensitive data, stored in Azure SQL Database or SQL Server databases from access by database administrators. Always Encrypted leverages client-side encryption: a database driver inside an application transparently encrypts data, before sending the data to the database. Similarly, the driver decrypts encrypted data retrieved in query results.
Column encryption keys are used to encrypt data in the database. These keys are stored in the database in the encrypted form (never in plaintext).
Column master keys are used to encrypt column encryption keys. These keys are stored in an external key store, such as Windows Certificate Store, Azure Key Vault or hardware security modules. For keys stored in Azure Key Vault, only the client application has access to the keys, but not the database, unlike TDE.
It is often advised to use Always Encrypted, TDE, and TLS together
Implement Azure Confidential Compute and SSL/TLS communications
https://azure.microsoft.com/cs-cz/blog/introducing-azure-confidential-computing/
Trusted Execution Environment (TEE - also known as an enclave), TEEs ensure there is no way to view data or the operations inside from the outside, even with a debugger.
Virtual Secure Mode and Intel SGX. VSM and SGX-enabled virtual machines.
All sessions with Azure services and data centers are secured using the Transport Layer Security (TLS) cryptographic protocol and Forward Secrecy (also known as Perfect Forward Secrecy or PFS), a key agreement protocol
Create, read, update, and delete keys, secrets, and certificates by using the KeyVault API
https://docs.microsoft.com/en-us/rest/api/keyvault/
Develop for the Cloud (20-25%)
Configure a message-based integration architecture
Configure an app or service to send emails, Event Grid, and the Azure Relay Service
https://docs.microsoft.com/en-us/azure/event-grid/monitor-virtual-machine-changes-event-grid-logic-app#send-email-when-your-virtual-machine-changes
E.g. Office 365 Outlook connector, Outlook.com connector, Gmail connector
https://docs.microsoft.com/en-us/azure/event-grid/monitor-virtual-machine-changes-event-grid-logic-app#create-a-logic-app-that-monitors-events-from-an-event-grid
https://docs.microsoft.com/en-us/azure/service-bus-relay/relay-what-is-it
https://docs.microsoft.com/en-us/azure/app-service/app-service-hybrid-connections#add-and-create-hybrid-connections-in-your-app
Hybrid Connections - Uses the open standard web sockets enabling multi-platform scenarios.
WCF Relays - .NET Only. Uses Windows Communication Foundation (WCF) to enable remote procedure calls. WCF Relay is the legacy relay offering.
Create and configure Notification Hub, Event Hub, and Service Bus
https://docs.microsoft.com/en-gb/azure/event-grid/compare-messaging-services

https://docs.microsoft.com/en-us/azure/notification-hubs/create-notification-hub-portal

Easy-to-use and scaled-out push engine that allows you to send notifications to any platform (iOS, Android, Windows, Kindle, Baidu, etc.) from backend

Push notifications is a form of app-to-user communication

Create a Notification Hubs namespace and a hub in that namespace

Create Hub: Name for the notification hub, name for the namespace, location, pricing tier

https://docs.microsoft.com/en-us/azure/notification-hubs/configure-notification-hub-portal-pns-settings

https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create

Big Data streaming platform and event ingestion service

An Event Hubs namespace provides a unique scoping container (FQDN), in which you create one or more event hubs.

Create Namespace: Namespace name, pricing tier, Kafka option, zone redundancy, location, throughput, auto inflate option

Create Event hub: Event hub name inside namespace, # of partitions, message retention, capture option

https://docs.microsoft.com/en-gb/azure/service-bus-messaging/service-bus-create-namespace-portal

Namespace with a name that must be unique across Azure, pricing tier (Basic, Standard, or Premium), zone redundancy, Shared Access Signature (SAS), Shared access policies Manage, Send, Listen.

Topics/subscriptions are not supported in the Basic pricing tier

A namespace is a scoping container for all messaging components. Multiple queues and topics can reside within a single namespace, and namespaces often serve as application containers.

Configure queries across multiple products
TODO
Develop for autoscaling
Implement autoscaling rules and patterns (schedule, operational/system metrics, code that addresses singleton application instances)
https://docs.microsoft.com/en-us/azure/azure-monitor/platform/autoscale-overview
https://docs.microsoft.com/en-us/azure/virtual-machines/windows/autoscale
Autoscale applies to Virtual Machine Scale Sets, Cloud Services, Web Apps, and API Management
Allows to add resources to handle increases in load and also save money by removing resources that are sitting idle. You specify a minimum and maximum number of instances to run and add or remove VMs automatically based on a set of rules.
When rule conditions are met, one or more autoscale actions are triggered. You can add and remove VMs, or perform other actions.
Resources emit metrics, these metrics are later processed by rules. Virtual machine scale sets use telemetry data from Azure diagnostics agents whereas telemetry for Web apps and Cloud services comes directly from the Azure Infrastructure. Some commonly used statistics include CPU Usage, memory usage, thread counts, queue length, and disk usage.
Schedule-based rules are based on UTC. You must set your time zone properly when setting up your rules.
Metric-based - For example, do this action when CPU usage is above 50%.
Time-based - For example, trigger a webhook every 8am on Saturday in a given time zone.
Metric-based rules measure application load and add or remove VMs based on that load. Schedule-based rules allow you to scale when you see time patterns in your load and want to scale before a possible load increase or decrease occurs.
Rules can trigger one or more types of actions.
Scale - Scale VMs in or out
Send email
Call webhooks, which can trigger multiple complex actions inside or outside Azure. (Azure Automation runbook, Azure Function, or Azure Logic App)
https://docs.microsoft.com/en-us/azure/azure-functions/durable/durable-functions-singletons
For background jobs you often need to ensure that only one instance of a particular orchestrator runs at a time. This can be done in Durable Functions by assigning a specific instance ID to an orchestrator when creating it.
Implement code that addresses transient state
https://docs.microsoft.com/en-us/aspnet/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/transient-fault-handling
You have to think about is how to handle temporary service interruptions, You can frequently get little glitches that are typically self-healing
Use smart retry/back-off logic to mitigate the effect of transient failures
You can recognize errors that are typically transient, and automatically retry the operation that resulted in the error, in hopes that before long you'll be successful. Most of the time the operation will succeed on the second try, and you'll recover from the error without the customer ever having been aware that there was a problem.
