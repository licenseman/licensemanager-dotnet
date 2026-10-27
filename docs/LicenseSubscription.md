# LicenseManager.Model.LicenseSubscription
The Stripe subscription keeping the license valid, `null` when it isn't a subscription license. The license expires when it stops being paid, includes every update, and can't be canceled during a money back guarantee.

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**StripeSubscriptionId** | **string** |  | 
**Status** | **string** | Status of the subscription in Stripe: &#x60;active&#x60;, &#x60;trialing&#x60;, &#x60;past_due&#x60; while a failed payment is retried, &#x60;canceled&#x60;, &#x60;unpaid&#x60;, &#x60;paused&#x60;, &#x60;incomplete&#x60; or &#x60;incomplete_expired&#x60;. | 
**Interval** | **string** |  | 
**IntervalCount** | **int** | Number of intervals between payments. | 
**Quantity** | **int** | Units subscribed, multiplying the policy&#39;s machines. | 
**Price** | [**Price**](Price.md) | Price of one unit for one period, before taxes. | 
**CurrentPeriodEnd** | **DateTime** | End of the paid period, when the subscription renews or ends. | 
**CancelAtPeriodEnd** | **bool** | Whether the subscription ends at the end of the period. | 
**EndedAt** | **DateTime?** |  | 

[[Back to Model list]](../README.md#documentation-for-models) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to README]](../README.md)

