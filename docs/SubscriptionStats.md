# LicenseManager.Model.SubscriptionStats
Subscriptions to recurring Stripe prices, each with its subscription license.

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**ActiveCount** | **int** | Number of ongoing subscriptions: &#x60;active&#x60;, &#x60;trialing&#x60; or &#x60;past_due&#x60;. | 
**TrialingCount** | **int** |  | 
**PastDueCount** | **int** | Number of them whose renewal failed, as Stripe retries it: their licenses stay valid for the integration&#39;s grace days. | 
**CancelingCount** | **int** | Number of them set to end at the end of their period. | 
**NewCount** | **int** | Number of subscriptions started in the last 30 days. | 
**EndedCount** | **int** | Number of subscriptions that ended in the last 30 days. | 
**ChurnRate** | **decimal** | Share of the subscriptions ongoing 30 days ago that ended since, from 0 to 1. | 
**NewByMonth** | **List&lt;int&gt;** | Number of subscriptions started each month, aligned on &#x60;months&#x60;. | 
**EndedByMonth** | **List&lt;int&gt;** | Number of subscriptions that ended each month, aligned on &#x60;months&#x60;. | 
**ActiveByMonth** | **List&lt;int&gt;** | Number of ongoing subscriptions at the end of each month, aligned on &#x60;months&#x60;, today for this month. | 
**Mrr** | [**List&lt;Mrr&gt;**](Mrr.md) | MRR in each currency, from the highest number of subscriptions. Amounts aren&#39;t converted between currencies. | 

[[Back to Model list]](../README.md#documentation-for-models) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to README]](../README.md)

