# LicenseManager.Model.Mrr

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**Currency** | **string** |  | 
**VarMrr** | **decimal** | Monthly recurring revenue: the price of every ongoing subscription in the currency, times its quantity, brought to one month (a year counts for a twelfth), before taxes and discounts. | 
**ByInterval** | [**List&lt;MrrByIntervalInner&gt;**](MrrByIntervalInner.md) | Ongoing subscriptions and MRR of each billing period, like monthly and yearly, from the highest MRR. | 
**ByPolicy** | [**List&lt;MrrByPolicyInner&gt;**](MrrByPolicyInner.md) | MRR of each policy, from the highest. | 
**ByMonth** | **List&lt;decimal&gt;** | MRR at the end of each month, aligned on &#x60;months&#x60;, today for this month, at the current prices of the subscriptions. | 

[[Back to Model list]](../README.md#documentation-for-models) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to README]](../README.md)

