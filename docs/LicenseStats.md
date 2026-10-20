# LicenseManager.Model.LicenseStats

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**From** | **DateTime** | First day covered, in UTC. | 
**To** | **DateTime** | Last day covered, in UTC: today. | 
**Days** | **List&lt;DateTime&gt;** | The 90 days covered, from the oldest one, in UTC. | 
**ActivationsByMachine** | [**List&lt;LicenseStatsActivationsByMachineInner&gt;**](LicenseStatsActivationsByMachineInner.md) | Machines that activated the license in the period, from the one with the most activations. | 
**ActivationsByVersion** | [**List&lt;LicenseStatsActivationsByVersionInner&gt;**](LicenseStatsActivationsByVersionInner.md) | Versions of the application that activated the license in the period, from the most recent one. | 

[[Back to Model list]](../README.md#documentation-for-models) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to README]](../README.md)

