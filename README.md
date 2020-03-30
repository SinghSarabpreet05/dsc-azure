## dsc-azure

This repo contains sample ARM templates to automate onboarding of VMs to Azure Automation Account State Configuration.

### Powershell DSC

Official Powershell DSC [documentation from Microsoft](https://docs.microsoft.com/en-us/powershell/scripting/dsc/overview/overview?view=powershell-7).

### Powershell DSC using Azure Automation Account

Official Azure Automation Account State Configuration [documentation from Microsoft](https://docs.microsoft.com/en-us/azure/automation/automation-dsc-overview).

### VM onboarding to Automation Account State Configuration

1. In an Automation Account, choose **State Configuration** from the Menu Blade
  - **Nodes:** These are the VMs that have been onboarded.
  - **Configurations:** These are the dsc ps1 scripts that have been uploaded.
  - **Compiled Configurations:** These are the .mof files of the configurations that have been compiled.
  
2. Add a **Node** by clicking on **+Add** and choosing the VM on which the configuration will be pushed.
3. Add a **Configuration** by clicking on **+Add** and uploading the ps1 script file.
4. Compile the configuration and it'll start showing in **Compiled Configurations**.
5. To assign a node configuration: Select a node, select assign configuration and choose from the compiled configurations.
6. Azure Automation also provides features to compose a configuration on the portal itself.

### Automating VM Onboarding

1. **Services used:**
  - Azure Policy
  - Automation Account State Configuration
  - ARM templates
  
2. **Azure Policy** comes with multiple effects that can be performed on Azure resources. One of that effects is **deployIfNotExists**.  A policy with this action can deploy an ARM template as remediation when an existence conition fails. [Read more about Azure Policy](https://docs.microsoft.com/en-us/azure/governance/policy/overview). 
3. When onboarding a VM to **State Configuration**, an extension is added to the VM. The publisher of extension is Microsoft.Powershell.DSC for Windows and Microsoft.OSTCExtensions for Linux. This extension can be deployed to VMs using **ARM templates**.

**TL;DR** Use Azure policy with deployIfNotExists effect to deploy ARM template whenever a new VM is created in azure subscription. This ARM template should deploy a VM extension to ensure onboarding to State Configuration.
