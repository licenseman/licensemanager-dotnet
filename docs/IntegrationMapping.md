# LicenseManager.Model.IntegrationMapping

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**Id** | **string** |  | 
**IntegrationId** | **string** |  | 
**Provider** | **string** |  | 
**ProductId** | **string** |  | 
**PolicyId** | **string** |  | 
**ExternalProductId** | **string** | Id of the product in the provider: &#x60;prod_…&#x60; in Stripe, &#x60;pro_…&#x60; in Paddle. | 
**ExternalPriceId** | **string** | Id of the price in the provider: &#x60;price_…&#x60; in Stripe, &#x60;pri_…&#x60; in Paddle. | 
**StripeProductId** | **string** | Deprecated: use &#x60;externalProductId&#x60;, which it equals. | 
**StripePriceId** | **string** | Deprecated: use &#x60;externalPriceId&#x60;, which it equals. | 
**ProductName** | **string** | Name of the provider&#39;s product when it was mapped. | 
**Price** | [**Price**](Price.md) |  | 
**Recurring** | [**IntegrationMappingRecurring**](IntegrationMappingRecurring.md) |  | 
**Status** | **string** | &#x60;error&#x60; when the price can no longer be paid, explained by &#x60;statusReason&#x60;. | 
**StatusReason** | **string** |  | 
**CreatedAt** | **DateTime** |  | 

[[Back to Model list]](../README.md#documentation-for-models) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to README]](../README.md)

