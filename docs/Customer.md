# LicenseManager.Model.Customer

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**Id** | **string** |  | 
**ProductId** | **string** |  | 
**Email** | **string** |  | 
**Name** | **string** | Display name of the customer. &#x60;null&#x60; when unknown. | 
**LicenseCount** | **int** | Number of licenses of this customer. | 
**StripeCustomerId** | **string** | Id of the Stripe customer, when the customer bought licenses through the Stripe integration as a Stripe customer. &#x60;null&#x60; otherwise, e.g. for a guest checkout. | 
**CreatedAt** | **DateTime** |  | 

[[Back to Model list]](../README.md#documentation-for-models) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to README]](../README.md)

