# LicenseManager.Model.CancellationStats
Cancellations of the licenses with a money back guarantee. Licenses canceled without one are left out.

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**LicenseCount** | **int** | Number of licenses with a money back guarantee: a &#x60;cancellableUntil&#x60;. | 
**CanceledLicenseCount** | **int** | Number of them that were canceled. | 
**CancellableLicenseCount** | **int** | Number of them whose money back guarantee hasn&#39;t ended, and that weren&#39;t canceled: they can still be. | 
**Rate** | **decimal** | Share of them that were canceled, from 0 to 1: &#x60;canceledLicenseCount&#x60; over &#x60;licenseCount&#x60;. | 
**CanceledByDay** | **List&lt;int&gt;** | Number of them canceled each day, aligned on &#x60;days&#x60;, on the day of their cancellation. | 
**CanceledByMonth** | **List&lt;int&gt;** | Number of them canceled each month, aligned on &#x60;months&#x60;, on the month of their cancellation. | 
**ByReason** | [**List&lt;CancellationStatsByReasonInner&gt;**](CancellationStatsByReasonInner.md) | Number of them canceled for each reason, from the most given one. Reasons never given are left out. | 

[[Back to Model list]](../README.md#documentation-for-models) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to README]](../README.md)

