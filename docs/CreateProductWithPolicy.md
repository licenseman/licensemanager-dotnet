# LicenseManager.Model.CreateProductWithPolicy

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**Name** | **string** |  | 
**Slug** | **string** | Unique within the organization. Defaults to the name, lower cased, without accents and special characters. Starts with &#x60;test_&#x60; in test products, which is added when missing, and removed in live products. | [optional] 
**DefaultPolicy** | [**PolicySettings**](PolicySettings.md) |  | [optional] 
**IsTestFromProductId** | **string** | Creates a test product: a sandbox of this live product of the organization, starting with copies of its policies, releases, portal settings and &#x60;autoMachineChange&#x60;. | [optional] 

[[Back to Model list]](../README.md#documentation-for-models) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to README]](../README.md)

