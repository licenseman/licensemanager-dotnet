# LicenseManager.Model.UpdateLicense

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**ExpiresAt** | **DateTime?** | &#x60;null&#x60; makes the license never expire. | [optional] 
**Meta** | **Dictionary&lt;string, Object&gt;** | Free-form JSON object. | [optional] 
**MaxMachines** | **int?** | Maximum number of active machines the license can be used on. &#x60;null&#x60; for no limit. | [optional] 
**MaxOfflineDurationSeconds** | **int** | Longest the applications can run offline with the license, in seconds. At least one hour (&#x60;3600&#x60;). | [optional] 
**MaxVersion** | [**LicenseMaxVersionInput**](LicenseMaxVersionInput.md) | Latest version of the product the license can use. The values left out are kept. | [optional] 
**Price** | [**PriceInput**](PriceInput.md) |  | [optional] 

[[Back to Model list]](../README.md#documentation-for-models) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to README]](../README.md)

