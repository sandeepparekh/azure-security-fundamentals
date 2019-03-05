# Azure Security Center Labs

The following labs are designed to deploy a non-secure environment with three VNET's, each with a Windows VM in your subscription.



#
### Step 1 : Sign into the Azure Portal

Jump into a Browser and sign into http://portal.azure.com

Click on the Cloud Shell icon in the top right corner of the browser.

If this is the first time you are using the Cloud Shell you will be prompted to create and attach a storage account. Do so and continue to open the Cloud Shell session.

#
### Step 2 : Clone the environment template

Copy and paste the following Powershell code into the Cloud Shell session and press enter. (The deployment will take around 15 minutes to complete)

```
#######################
## Deploy Environment##
#######################

cd ~

git clone https://github.com/sympa18/azure-security-fundamentals-lab-template.git

cd ~/azure-security-fundamentals-lab-template

.\Deploy.ps1

###############################################

```

You should now see two new Resource Groups. RGMELCONTOSO and RGSYDCONTOSO. Take a minute to browse through the resources.

#

### Step 3 : Start configuring Azure Security Center 

- Under **Favourites** or in **All Services** find and click on **Security Center**

- Select **Security Policy** then **Edit Settings** next to your subscription in the **Policy Management** Blade

- Select **Pricing tier** choose **Standard** then click **Save**

- Select **Data Collection** and ensure the following settings
  - **Auto Provisioning** set to **ON**
  - leave **Workspace Configuration** at **default**
  - Under **Windows Security Events** select **All Events** and click **Save**

Feel free to browse the other sections under settings

#

###  Step 4 : Set off an Alert (Requires RDP access)
#
If you have RDP access follow the artice below to invoke an Alert in Azure Security Center and then after around 15 to 20 minutes come back to check on the Alert as per the article
### Alerts Validation in Azure Security Center (Requires RDP)

https://docs.microsoft.com/en-us/azure/security-center/security-center-alert-validation

#
### Step 5 : Resource Security Hygiene

- Under **Resource Security Hygiene** click on **Recommendations**

Here you can see potential issues inside your subscription based on resource types. 

- Click on **Compute & apps**

- We should see common recommendations for our subscription. Click on **Install endpoint protection...** 

- Ensure all three of our VM's are selected VMMELDEV, VMMELPROD, VMSYDPROD and select **Install on 3 VMs**

- Select **Microsoft Antimalware** then **Create** accept the defaults and click **OK**

This will now kick off the installation of the Antimalware extension on these VMs.

Feel free to run through some of the other recommendations once this is complete. Come back after a few minutes to see that the warnings have now disappeared and your security score has increased.

- Go back a few blades and click on **Data & storage** 

We should see that we have a couple of issues with our storage accounts

- Click on **Require secure transfer to storage account**
- Select one of the two storage accounts we created earlier.
- Change **Secure transfer required** and click **Save**
- Do this for both storage accounts

Feel free to run through some of the other recommendations once this is complete. Come back after a few minutes to see that the warnings have now disappeared and your security score has increased.
#
### Step 6 : Enable JIT VM Access

- In the Azure Portal click on **All Services** and search for **Virtual Machines**
- For each of the VMS VMMELDEV, VMMELPROD, VMSYDPROD do the following 
- Click on the VM, then click on **Configuration** and select Enable **just-in-time policy**
-once you have done that for all three go back into Azure Security Center
- Back in the Security Center Blade under **Advanced Cloud Defense** click on **Just in time VM access**

This will allow us to do is restrcit access to any public facing endpoints and make administrators request access for a short period of time before denying access again.

- Click on any of the VMs and select the elipsis and click **Edit** 

Here you can see existing ports that are available. Click Add to see your options for adding new ports and time ranges.
- Close the **edit blade**
- Choose one of the 3 VM's and click on **Request access**
- Toggle the RDP port to **On** and set the range to 1 hour then click **Open ports**
- You should see Last Access as Active now and your username as the Last User.
- Click on the Virtual Machines link under All Services
- Select the VM you just enabled  
- Click **Connect** and test out RDP access
#
### Step 7 : Enable File Integrity Monitoring
- Under **Advanced Cloud Defense** click on **File Integrity Monitoring** 
- click on the Default workspace and click **Enable File Integrity Monitoring**

Data may take a while to come through so come back to this area after some time to analyse any findings.
#
### Step 8 : Create a Playbook
- Run through the article below to create a Security Playbook

### Security Playbook in Azure Security Center (Preview)

https://docs.microsoft.com/en-us/azure/security-center/security-center-playbooks
#
### Step 9 : Security Policies 
### Working with security policies

https://docs.microsoft.com/en-us/azure/security-center/tutorial-security-policy

#
### Step 10 : Monitoring and processing security events in Azure Security Center

https://docs.microsoft.com/en-us/azure/security-center/security-center-events-dashboard

#
### Step 11 : Azure Security Center search
https://docs.microsoft.com/en-us/azure/security-center/security-center-search
#
### Further  Reading
### Integrate security solutions in Azure Security Center

https://docs.microsoft.com/en-us/azure/security-center/security-center-partner-integration

#

### Tutorial: Respond to security incidents
NOTE This requires the Alert from earlier to have appeared.

https://docs.microsoft.com/en-us/azure/security-center/tutorial-security-incident

#
### Azure Monitor Documentation
https://docs.microsoft.com/en-au/azure/azure-monitor/

# 

[Back to Labs](./AzureSeucrityLabs.MD)
