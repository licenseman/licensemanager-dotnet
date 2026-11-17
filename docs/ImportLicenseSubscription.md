# LicenseManager.Model.ImportLicenseSubscription
Subscription of the provider keeping the license valid, like one moved to Stripe by Lemon Squeezy's migration: its renewals then extend this license rather than creating one with a new key. Its price must be mapped to a policy of the product, which the license follows instead of `policyId`, and the license's expiration, version and money back guarantee follow the subscription like the ones it creates. Read from the provider of the product's mode, through the integration.

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**Provider** | **string** | Provider of the subscription. | 
**ExternalId** | **string** | Id of the subscription in the provider: &#x60;sub_…&#x60; in Stripe and in Paddle. | 

[[Back to Model list]](../README.md#documentation-for-models) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to README]](../README.md)

