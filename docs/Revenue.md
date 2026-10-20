# LicenseManager.Model.Revenue
Revenue of the licenses sold in one currency, each license counting on the day it was created. Licenses without a price are left out.

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**Currency** | **string** | ISO 4217 code of the currency of the revenue. | 
**LicenseCount** | **int** | Number of licenses sold in the currency, free ones included. | 
**Total** | **decimal** | Sum of the prices of the licenses sold in the currency, in major units. | 
**ThisMonth** | **decimal** | Revenue of the current month, in UTC. | 
**LastMonth** | **decimal** | Revenue of the previous month, in UTC. | 
**Last30Days** | **decimal** | Revenue of the last 30 days, today included, in UTC. | 
**ByDay** | **List&lt;decimal&gt;** | Revenue each day, aligned on &#x60;days&#x60;. | 
**ByMonth** | **List&lt;decimal&gt;** | Revenue each month, aligned on &#x60;months&#x60;. | 
**ByPolicy** | [**List&lt;ProductStatsNewLicensesByPolicyInner&gt;**](ProductStatsNewLicensesByPolicyInner.md) | Revenue of the licenses of each policy, for the policies with licenses sold in the currency over the covered months. | 

[[Back to Model list]](../README.md#documentation-for-models) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to README]](../README.md)

