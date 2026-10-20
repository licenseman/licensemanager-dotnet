# LicenseManager.Model.ProductStats

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**LicenseCount** | **int** | Number of licenses of the product. | 
**ActiveLicenseCount** | **int** | Number of licenses that haven&#39;t expired, and that a machine validated in the last 90 days. | 
**NewLicenseCount** | **int** | Number of licenses created in the last 30 days, today included, in UTC. | 
**ExpiringLicenseCount** | **int** | Number of licenses expiring in the next 30 days. | 
**ExpiredLicenseCount** | **int** | Number of licenses that expired in the last 30 days. | 
**ActiveMachineCount** | **int** | Number of active machines of the licenses of the product. | 
**InUseLicenseCount** | **int** | Number of licenses with at least one active machine. | 
**SeatCount** | **int** | Sum of the maximum numbers of machines of the licenses that haven&#39;t expired. Licenses without a maximum are left out. | 
**UsedSeatCount** | **int** | Number of active machines of the licenses counted in &#x60;seatCount&#x60;, at most their maximum number of machines each. | 
**FullLicenseCount** | **int** | Number of licenses counted in &#x60;seatCount&#x60; active on their maximum number of machines. | 
**Days** | **List&lt;DateTime&gt;** | The 30 days covered by the daily stats, from the oldest one, in UTC. | 
**Months** | **List&lt;string&gt;** | The 12 months covered by the monthly stats, from the oldest one, in UTC. | 
**NewLicensesByDay** | **List&lt;int&gt;** | Number of licenses created each day, aligned on &#x60;days&#x60;. | 
**NewLicensesByMonth** | **List&lt;int&gt;** | Number of licenses created each month, aligned on &#x60;months&#x60;. | 
**NewLicensesByPolicy** | [**List&lt;ProductStatsNewLicensesByPolicyInner&gt;**](ProductStatsNewLicensesByPolicyInner.md) | Number of licenses of each policy created each day and each month, for the policies with licenses created over the covered months. | 
**Revenue** | [**List&lt;Revenue&gt;**](Revenue.md) | Revenue in each currency licenses were sold in, from the one with the most licenses sold. Amounts aren&#39;t converted between currencies. | 
**ActivationsByVersion** | [**List&lt;ProductStatsActivationsByVersionInner&gt;**](ProductStatsActivationsByVersionInner.md) | Successful activations of the licenses of the product each day, per version of the application, from the most recent one. | 
**ActiveMachinesByVersion** | [**List&lt;ProductStatsActiveMachinesByVersionInner&gt;**](ProductStatsActiveMachinesByVersionInner.md) | Number of active machines running each version of the application, from the most recent one. | 
**ActiveMachinesByPlatform** | [**List&lt;ProductStatsActiveMachinesByPlatformInner&gt;**](ProductStatsActiveMachinesByPlatformInner.md) | Number of active machines on each platform, from the one with the most machines. | 

[[Back to Model list]](../README.md#documentation-for-models) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to README]](../README.md)

