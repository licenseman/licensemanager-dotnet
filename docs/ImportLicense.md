# LicenseManager.Model.ImportLicense

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**Email** | **string** | Email of the customer the license belongs to. The product&#39;s customer with this email, compared regardless of case, or a new one when there&#39;s none. | 
**Key** | **string** | The license&#39;s current key, kept as is. Case sensitive. Starts with &#x60;TEST-&#x60; in test products, which is added when missing, and removed in live products. | 
**PolicyId** | **string** | Policy of the product the license follows. Defaults to the product&#39;s default policy. | [optional] 
**ExpiresAt** | **DateTime?** | &#x60;null&#x60; makes the license never expire. Defaults to the creation date plus the duration of the policy, or &#x60;null&#x60; when the policy has none. | [optional] 
**Meta** | **Dictionary&lt;string, Object&gt;** | Free-form JSON object. | [optional] 
**MaxMachines** | **int?** | Maximum number of active machines the license can be used on. &#x60;null&#x60; for no limit. Defaults to the one of the policy. | [optional] 
**MaxOfflineDurationSeconds** | **int** | Longest the applications can run offline with the license, in seconds. At least one hour (&#x60;3600&#x60;). Defaults to the one of the policy. | [optional] 
**Price** | [**PriceInput**](PriceInput.md) |  | [optional] 
**MaxVersion** | [**LicenseMaxVersionInput**](LicenseMaxVersionInput.md) |  | [optional] 
**CancellableUntil** | **DateTime?** | End of the money back guarantee: until then, the customer can cancel the license from the customer portal, or with a token. &#x60;null&#x60; to not let them. Defaults to the creation date plus the policy&#39;s &#x60;moneyBackGuaranteeDays&#x60;, or &#x60;null&#x60; when it has none. | [optional] 
**Name** | **string** | Name of the customer, given to it when it has none yet. | [optional] 
**Subscription** | [**ImportLicenseSubscription**](ImportLicenseSubscription.md) |  | [optional] 

[[Back to Model list]](../README.md#documentation-for-models) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to README]](../README.md)

