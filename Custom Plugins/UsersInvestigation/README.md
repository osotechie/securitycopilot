<div align="center">

<img src="https://avatars.githubusercontent.com/u/34251619?v=4" align="center" width="144px" height="144px"/>

### Security Copilot - Custom Plugin (KQL) - User Investigation

</div>

---

## 📖 Overview

This is a Security Copilot Custom Plugin (using KQL) to help optimise user investigation activities within Security Copilot. The plugin includes several skills:

|Skill|Description|
|-|-|
|GetSigninEventLocationsSummary|Get the number of signins events by location for all users|
|GetSigninEventLocationsSummaryByUsers|Get the number of signins events by location for the specified users with minimal info in output|
|GetSigninEventDetailsSummaryByUsers|Get the number of signins events summarized by different details for the specified users|
|GetInactiveUsers|Get a list of inactive users based on having no signins for a given period of days|

The following are some explains of how you can invoke the diffent skills within the Security Copilot standalone experience:

- */GetSigninEventLocationsSummary List me the signin locations of yesterday. Ignore the signins from the locations NZ and AU*

- */GetSigninEventLocationsSummaryByUsers List me the signin locations of yesterday for the users john@contoso.com and rick@contoso.com*

- */GetSigninEventDetailsSummaryByUsers List me the signin locations of yesterday for the users john@contoso.com and rick@contoso.com. Explain the results*

- */GetInactiveUsers based on the last 90 days*

<br>

## 💾 Installation

To install this custom plugin within your Security Copilot instance follow the below instructions:

1. **Download** the [UserInvestigations.yaml](https://raw.githubusercontent.com/osotechie/securitycopilot/refs/heads/main/Custom%20Plugins/UsersInvestigation/UsersInvestigation.yaml)

2. **Browse** to [Security Copilot](securitycopilot.microsoft.com) standalone experience portal

3. **Click** the **Sources** button in the prompt section

4. **Scroll down** to the **Custom Plugin** section, and **click** the **Add Plugin** button

5. **Select** who can use the Plugin, either *Just you* or *Anyone in my organization*

6. **Click** the **Security Copilot plugin** button as the upload format type

7. **Click** the **Upload file** button, and browse to the downloaded **UserInvestigations.yaml** file from step 1.

8. **Click** the **Add** button to complete adding the custom plugin

<br>

> [!NOTE]
> You can keep your custom plugin files in a source control platform like GitHub, and link the Custom Plugin within Security Copilot directly to the file in source control. This means any future changes to the custom plugin files will be reflected automatically in Security Copilot.
>
>During step 7, instead of uploading the file, simple **toggle** the **upload as a link** option.
>
>Then enter a publically accessible link to the **UserInvestigations.yaml** file from your source control repo, and set the file type to .yaml
>
> ***example:*** *https://raw.githubusercontent.com/osotechie/securitycopilot/refs/heads/main/Custom%20Plugins/UsersInvestigation/UsersInvestigation.yaml*

<br>

## 🙌 Acknowledgements

This custom plugin is a fork of the amazing work done by [stefanpems](https://github.com/stefanpems), and has been adapted / extended to fit my own requirements. Make sure to check out more of [stefanpems](https://github.com/stefanpems) work, including:

- [LinkedIn Posts](https://www.linkedin.com/in/stefanopescosolido/)
- [Stefanpe's Blog](https://stefanpems.github.io/)
