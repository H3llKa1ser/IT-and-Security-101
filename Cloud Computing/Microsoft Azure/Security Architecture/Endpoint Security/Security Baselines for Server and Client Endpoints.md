# Specify security baselines for server and client endpoints

This unit will explore using security baselines to configure Windows devices in Intune.

Intune makes it easy to deploy Windows security baselines to help you secure and protect your users and devices.

Even though Windows and Windows Server are designed to be secure out-of-the-box, many organizations still want more granular control over their security configurations. To navigate the large number of controls, organizations often seek guidance on configuring various security features. Microsoft provides this guidance in the form of security baselines.

Security baselines are groups of pre-configured Windows settings that help you apply and enforce granular security settings that are recommended by the relevant security teams. You can also customize each baseline you deploy to enforce only those settings and values you require. When you create a security baseline profile in Intune, you're creating a template that consists of multiple device configuration profiles.

To learn more about why and when you might want to deploy security baselines, see Windows security baselines in the Windows security documentation.

This feature applies to:

1) Windows 10 version 1809 and later

2) Windows 11

You deploy security baselines to groups of users or devices in Intune, and the settings apply to devices that run Windows 10/11. For example, the MDM Security Baseline automatically enables BitLocker for removable drives, automatically requires a password to unlock a device, automatically disables basic authentication, and more. When a default value doesn't work for your environment, customize the baseline to apply the settings you need.

Separate baseline types can include the same settings and use different default values for those settings. It's important to understand the defaults in the baselines you choose to use, and to then modify each baseline to fit your organizational needs.

In almost all scenarios, the default settings in the security baselines are the most restrictive. You should confirm that these settings don't conflict with other policy settings or features in your environment.

For example, the default settings for firewall configuration might not merge connection security rules and local policy rules with MDM rules. So, if you're using delivery optimization, then you should validate these configurations before assigning the security baseline.

Security baselines can help you to have an end-to-end secure workflow when working with Microsoft 365. Some of the benefits include:

1) A security baseline includes the best practices and recommendations on settings that impact security. Intune partners with the same Windows security team that creates group policy security baselines. These recommendations are based on guidance and extensive experience.

2) If you're new to Intune, and not sure where to start, then security baselines gives you an advantage. You can quickly create and deploy a secure profile, knowing that you're helping protect your organization's resources and data.

3) If you currently use group policy, migrating to Intune for management is much easier with these baselines. These baselines are natively built in to Intune, and include a modern management experience.

## Available security baselines

The following security baseline instances are available for use with Intune. Use the links to view the settings for recent instances of each baseline.

Security Baseline for Windows 10 and later

Version 23H2
November 2021
December 2020
August 2020

Microsoft Defender for Endpoint baseline
(To use this baseline your environment must meet the prerequisites for using Microsoft Defender for Endpoint).

Version 24H1
Version 6
Version 5
Version 4
Version 3

Microsoft Edge Baseline

Microsoft Edge version 117 - November 2023

Microsoft Edge version 112 and later - May 2023

Microsoft Edge version 85 and later - September 2020

Microsoft Edge version 80 and later - April 2020

Preview: Microsoft Edge version 77 and later - October 2019

Windows 365 Security Baseline

Version 24H1

November 2021

After a new version for a profile releases, settings in profiles based on the older versions become read-only. You can continue using those older profiles, including editing their name, description, and assignments, but you won't be able to edit settings for them or create new profiles based on the older versions.

When you're ready to use the more recent version of a baseline, you can create new profiles or update your existing profiles to the new version. See Change the baseline version for a profile in the Manage security baseline profiles article.

## About baseline versions and instances

Each new version instance of a baseline can add or remove settings or introduce other changes. For example, as new Windows settings become available with new versions of Windows 10/11, the MDM Security Baseline might receive a new version instance that includes the newest settings.

In the Microsoft Intune admin center, under Endpoint security > Security baselines you'll see a list of the available baselines. The list includes:

1) The baseline template name.

2) How many profiles you have that use that type of baseline.

3) How many separate instances (versions) of the baseline type are available.

4) A Last Published date that identifies when the latest version of the baseline template became available.

To view more information about the baseline versions you use, select a baseline type, like MDM Security Baseline to open its Profiles pane, and then select Versions. Intune displays details about the versions of that baseline that are in use by your profiles. The details include the most recent and current baseline version. You can select a single version to view deeper details about the profiles that use that version.

You can choose to change of the version of a baseline that's in use with a given profile. When you change the version, you don't have to create a new baseline profile to take advantage of updated versions. Instead you can select a baseline profile and use the built-in option to change the instance version for that profile to a new one.

