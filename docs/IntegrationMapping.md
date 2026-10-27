# LicenseManager.Model.IntegrationMapping

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**Id** | **string** |  | 
**IntegrationId** | **string** |  | 
**ProductId** | **string** |  | 
**PolicyId** | **string** |  | 
**StripeProductId** | **string** |  | 
**StripePriceId** | **string** |  | 
**ProductName** | **string** | Name of the Stripe product when it was mapped. | 
**Price** | [**Price**](Price.md) |  | 
**Recurring** | [**IntegrationMappingRecurring**](IntegrationMappingRecurring.md) |  | 
**Status** | **string** | &#x60;error&#x60; when the price can no longer be paid, explained by &#x60;statusReason&#x60;. | 
**StatusReason** | **string** |  | 
**CreatedAt** | **DateTime** |  | 

[[Back to Model list]](../README.md#documentation-for-models) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to README]](../README.md)

