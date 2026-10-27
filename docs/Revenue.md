# LicenseManager.Model.Revenue
Revenue in one currency: the licenses sold once, each counting on the day it was created, and the payments of the subscription licenses, each counting on the day it was paid, with the license's policy. Licenses without a price are left out, and so are canceled ones, but in `canceledLicenseCount` and `canceledTotal`.

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**Currency** | **string** | ISO 4217 code of the currency of the revenue. | 
**LicenseCount** | **int** | Number of licenses sold once in the currency, free ones included, canceled ones and subscription licenses left out. | 
**Total** | **decimal** | Revenue in the currency, in major units: the prices of the licenses sold once, canceled ones left out, plus the payments of the subscriptions, &#x60;subscriptionTotal&#x60;. | 
**SubscriptionTotal** | **decimal** | Sum of the payments of the subscription licenses in the currency, before taxes, in major units. | 
**PaymentCount** | **int** | Number of payments of the subscription licenses in the currency. | 
**CanceledLicenseCount** | **int** | Number of canceled licenses sold once in the currency. | 
**CanceledTotal** | **decimal** | Sum of the prices of the canceled licenses sold once in the currency, in major units: revenue lost to cancellations. | 
**ThisMonth** | **decimal** | Revenue of the current month, in UTC. | 
**LastMonth** | **decimal** | Revenue of the previous month, in UTC. | 
**Last30Days** | **decimal** | Revenue of the last 30 days, today included, in UTC. | 
**ByDay** | **List&lt;decimal&gt;** | Revenue each day, aligned on &#x60;days&#x60;. | 
**ByMonth** | **List&lt;decimal&gt;** | Revenue each month, aligned on &#x60;months&#x60;. | 
**ByPolicy** | [**List&lt;ProductStatsNewLicensesByPolicyInner&gt;**](ProductStatsNewLicensesByPolicyInner.md) | Revenue of the licenses of each policy, for the policies with licenses sold in the currency over the covered months. | 

[[Back to Model list]](../README.md#documentation-for-models) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to README]](../README.md)

