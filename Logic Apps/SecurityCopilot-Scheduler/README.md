<div align="center">

<img src="https://avatars.githubusercontent.com/u/34251619?v=4" align="center" width="144px" height="144px"/>

 ### ![alt text](../../_images/securitycopilot-icon.png) Security Copilot - Logic App - Security Copilot Scheduler

</div>

---

## 📖 Overview

These are a set of Logic Apps you can use to schedule changes to Security Copilot capacities to meet you different usage requirements, and manage your overall Security Copilot spend.

- ![ ](../../_images/azure_logicapp_icon.png ) **BASIC LOGIC APP**
The Baseline Logic App can be used to set (or delete) the Security Copilot capacity based on a schedule. The defaults provided with this logic app are set to run everyday at 7AM (7:00) and 6PM (18:00) and remove the Security Copilot capacity.
>[!Note]
> I set the recurrance (or Schedule) for the Baseline app to run twice a day for my own environment this was to ensure my baseline SCU requirements was being enforced twice daily no matter what day of the week, or if it was a public holiday.

- ![ ](../../_images/azure_logicapp_icon.png) **ADVANCED LOGIC APP**
The Advanced logic App can be used to set (or delete) the Security Copilot capacity also based on a schedule. But provides additional functionality to detect the day its running, for example you may want to use this app if you want to set specific Security Copilot capacity for weekdays, weekends or public holidays. The logic app has logic cases for each of these use cases. The defaults provided with this logic app are set to run everyday at 8AM (8:00) and create / update the Security Copilot capacity to 1 Provisioned SCU and allow upto 10 Overage SCU per hour on weekdays (excluding public holidays) only.

    ![alt text](../../_images/Workdays-LogicApp-Designer.png)

<br>

>[!Note]
>You could either manage the logic for weekdays, weekends etc using the recurrence of the logic app, or the logic cases. I choose to include the logic cases to allow for scenarios where you may want to have a single logic app that applies different capacities over weekdays, and weekends for example. 

<br>

- ![ ](../../_images/azure_logicapp_icon.png) **"FOR *X* TIME" LOGIC APP**
This logic App can be used to provision Security Copilot capacity for a given amount of time, at which point it will then be deleted. This could be used for example for quickly generating some reports via Security Copilot, or testing.


### Schedule Scenarios

<br>

You can create different scheduling scenarios for your Security Copilot capacity using both the Basic and Advanced logic apps if you wanted, for example:

#### Example 1: Baseline with different weekday capacity
- Deploy the Basic Logic App, with it set to Provision 2 SCU and 3 Overage SCU that runs at 7AM and 6PM as your Baseline capacity configuration
- Deploy several copies of the Advanced Logic App
    - A Workdays Morning version, set to Provision 4 SCU and 10 Overage SCU that uses the weekday logic case to run on Weekdays (excluding Public Holidays) at 8AM
    - A Workdays Afternoon version, set to Provision 2 SCU and 7 Overage SCU that uses the weekday logic case to run on Weekdays (excluding Public Holidays at 1PM)

    ![alt text](../../_images/SecurityCopilot-Schedule-Example.png)

#### Example 2: Baseline with different weekday, weekend and public holiday capacities
- Deploy the Basic Logic App, with it set to Provision 2 SCU and 3 Overage SCU that runs at 7AM and 6PM as your Baseline capacity configuration
- Deploy two copies of the Advanced Logic App
    - A Workdays version, set to Provision 4 SCU and 10 Overage SCU that uses the weekday logic case to run on Weekdays (excluding Public Holidays) at 8AM
    - A Weekend version, set to Provision 1 SCU and 10 Overage SCU that uses the weekend logic case to run on Weekends (excluding Public Holidays at 1PM)
    - A Public Holiday version, set to Provision 1 SCU and 10 Overage SCU that uses the public holiday logic case to run on Weekends (excluding Public Holidays at 1PM)

#### Example 3: Testing / Lab capacity for *x* amount of time
- Deploy the "For X Time" Logic App, with it set to Provision 2 SCU and 10 Overage SCU for 2 hours.


<br>

## 💾 Installation

To install this custom plugin within your Security Copilot instance follow the below instructions:

![ ](../../_images/azure_logicapp_icon.png) **BASIC LOGIC APP**

1. **Deploy** the Basic Logic App template to your tenant

    [![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fosotechie%2Fsecuritycopilot%2Frefs%2Fheads%2Fmain%2FLogic%20Apps%2FSecurityCopilot-Scheduler%2Ftemplate-basic.json)

2. Provide the required information to complete deployment of the template

    |Paramater|Description|
    |--------|-----------|
    |Region | The Azure Region where you will deploy the Logic App to|
    |Logic App Name | The name you want to call the Logic App in your environment|
    |Subscription ID | The Subscription ID where the Logic App and Security Copilot capacity will be deployed|
    |Resource Group | The Resource Group where the Logic App and Security Copilot capacity will be deployed|
    |Capacity Name | The Name of the Security Copilot Capacity that will be managed by the Logic App (e.g. Created, Updated or Deleted)|
    |Geography | Select from one of the valid Security Copilot geographies|
    |Location | Select the location within the chosen Security Copilot geopgrahy|
    |Cross Geography Compute | Select if you want to allow Security Copilot to process prompts outside the chosen Geography if its busy|
    |Provisioned SCU | Set the number of Provisioned SCU per hour you want.
    |Overage | Select if you want to allow / limit Overage SCUs for the Security Copilot capacity. Note you will only be charged for these if you consume more than the Provisioned SCUs in a given hour, these SCUs will be charged at 1.5x the cost of a Provisioned SCU|
    |Overage Amount | If you limit Overage set the number you want to be the limit|
    |Schedule | Update the Schedule for the Logic App|
    |Timezone | Set the Timezone that will be used by the Logic App. This is based on [Timezone IDs](https://learn.microsoft.com/en-us/previous-versions/windows/embedded/gg154758(v=winembedded.80)?redirectedfrom=MSDN)|


3. Grant the Managed Identity for the Logic App, Contributor rights on the Resource Group where you will deploy the Secuirty Copilot capacity to

    a. **Browse** to the Logic App in the Azure Portal
    
    b. **Select** Settings > Identity

    c. **Click** Azure Role Assignments

    d. **Select** + Add role assignments (Preview) from the menubar

    |Item|Description|
    |--------|-----------|
    |Scope | Resource Group|
    |Subscription | *The Subscription where you will deploy the Security Copilot capacity to*|
    |Resource Group | *The Resource Group where you will deploy the Security Copilot capacity to*|
    |Role | Contributor|

4. Enable the Logic App

    a. **Browse** to the Logic App in the Azure Portal

    b. **Click** Enable in the menubar of the overview screen

<br>
<br>

![ ](../../_images/azure_logicapp_icon.png) **ADVANCED LOGIC APP**

1. **Deploy** the Advanced Logic App template to your tenant

    [![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fosotechie%2Fsecuritycopilot%2Frefs%2Fheads%2Fmain%2FLogic%20Apps%2FSecurityCopilot-Scheduler%2Ftemplate-advanced.json)

2. Provide the required information to complete deployment of the template

    |Paramater|Description|
    |--------|-----------|
    |Region | The Azure Region where you will deploy the Logic App to|
    |Logic App Name | The name you want to call the Logic App in your environment|
    |Subscription ID | The Subscription ID where the Logic App and Security Copilot capacity will be deployed|
    |Resource Group | The Resource Group where the Logic App and Security Copilot capacity will be deployed|
    |Capacity Name | The Name of the Security Copilot Capacity that will be managed by the Logic App (e.g. Created, Updated or Deleted)|
    |Geography | Select from one of the valid Security Copilot geographies|
    |Location | Select the location within the chosen Security Copilot geopgrahy|
    |Cross Geography Compute | Select if you want to allow Security Copilot to process prompts outside the chosen Geography if its busy|
    |Provisioned SCU | Set the number of Provisioned SCU per hour you want.
    |Overage | Select if you want to allow / limit Overage SCUs for the Security Copilot capacity. Note you will only be charged for these if you consume more than the Provisioned SCUs in a given hour, these SCUs will be charged at 1.5x the cost of a Provisioned SCU|
    |Overage Amount | If you limit Overage set the number you want to be the limit|
    |Public Holiday Country Code | Set the Country Code to check for Public Holidays. A valid country code such as GB and UA|
    |Schedule | Update the Schedule for the Logic App|
    |Timezone | Set the Timezone that will be used by the Logic App. This is based on [Timezone IDs](https://learn.microsoft.com/en-us/previous-versions/windows/embedded/gg154758(v=winembedded.80)?redirectedfrom=MSDN)|

3. Grant the Managed Identity for the Logic App, Contributor rights on the Resource Group where you will deploy the Secuirty Copilot capacity to

    a. **Browse** to the Logic App in the Azure Portal
    
    b. **Select** Settings > Identity

    c. **Click** Azure Role Assignments

    d. **Select** + Add role assignments (Preview) from the menubar

    |Item|Description|
    |--------|-----------|
    |Scope | Resource Group|
    |Subscription | *The Subscription where you will deploy the Security Copilot capacity to*|
    |Resource Group | *The Resource Group where you will deploy the Security Copilot capacity to*|
    |Role | Contributor|

4. **Edit** the Logic App using the Design to meet your requirements.

5. **Enable** the Logic App

    a. **Browse** to the Logic App in the Azure Portal

    b. **Click** Enable in the menubar of the overview screen

<br>
<br>

![ ](../../_images/azure_logicapp_icon.png) **"For *X* Time" APP**

1. **Deploy** the "Fox *x* Time" Logic App template to your tenant

    [![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fosotechie%2Fsecuritycopilot%2Frefs%2Fheads%2Fmain%2FLogic%20Apps%2FSecurityCopilot-Scheduler%2Ftemplate-forxtime.json)

2. Provide the required information to complete deployment of the template

    |Paramater|Description|
    |--------|-----------|
    |Region | The Azure Region where you will deploy the Logic App to|
    |Logic App Name | The name you want to call the Logic App in your environment|
    |Subscription ID | The Subscription ID where the Logic App and Security Copilot capacity will be deployed|
    |Resource Group | The Resource Group where the Logic App and Security Copilot capacity will be deployed|
    |Capacity Name | The Name of the Security Copilot Capacity that will be managed by the Logic App (e.g. Created, Updated or Deleted)|
    |Geography | Select from one of the valid Security Copilot geographies|
    |Location | Select the location within the chosen Security Copilot geopgrahy|
    |Cross Geography Compute | Select if you want to allow Security Copilot to process prompts outside the chosen Geography if its busy|
    |Provisioned SCU | Set the number of Provisioned SCU per hour you want.
    |Overage | Select if you want to allow / limit Overage SCUs for the Security Copilot capacity. Note you will only be charged for these if you consume more than the Provisioned SCUs in a given hour, these SCUs will be charged at 1.5x the cost of a Provisioned SCU|
    |Overage Amount | If you limit Overage set the number you want to be the limit|
    |Hours to Provision | Set the number of hours your want to provision the Security Copilot capacity for|


3. Grant the Managed Identity for the Logic App, Contributor rights on the Resource Group where you will deploy the Secuirty Copilot capacity to

    a. **Browse** to the Logic App in the Azure Portal
    
    b. **Select** Settings > Identity

    c. **Click** Azure Role Assignments

    d. **Select** + Add role assignments (Preview) from the menubar

    |Item|Description|
    |--------|-----------|
    |Scope | Resource Group|
    |Subscription | *The Subscription where you will deploy the Security Copilot capacity to*|
    |Resource Group | *The Resource Group where you will deploy the Security Copilot capacity to*|
    |Role | Contributor|

4. Enable the Logic App

    a. **Browse** to the Logic App in the Azure Portal

    b. **Click** Enable in the menubar of the overview screen

5. Run the Logic App when you need to the Capacity

<br>
<br>

<br>

## 🙌 Acknowledgements

This Logic App is a fork of the amazing work done by [stefanpems](https://github.com/stefanpems), and has been adapted / extended to fit my own requirements. Make sure to check out more of [stefanpems](https://github.com/stefanpems) work, including:

- [LinkedIn Posts](https://www.linkedin.com/in/stefanopescosolido/)
- [Stefanpe's Blog](https://stefanpems.github.io/)
