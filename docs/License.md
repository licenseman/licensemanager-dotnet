# LicenseManager.Model.License

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**Id** | **string** |  | 
**ProductId** | **string** |  | 
**PolicyId** | **string** |  | 
**CustomerId** | **string** |  | 
**Key** | **string** | Unique within the product. Case sensitive: &#x60;validateKey&#x60; compares keys exactly. | 
**CreatedAt** | **DateTime** |  | 
**ExpiresAt** | **DateTime?** | &#x60;null&#x60; when the license never expires. | 
**Meta** | **Dictionary&lt;string, Object&gt;** | Free-form JSON object. | 
**StripePaymentIntentId** | **string** | Id of the Stripe payment intent that paid the license, when it was bought through the Stripe integration. &#x60;null&#x60; otherwise, or when nothing was paid. | 
**MaxMachines** | **int?** | Maximum number of active machines the license can be used on. &#x60;null&#x60; when there&#39;s no limit. Can be lower than &#x60;activeMachineCount&#x60; after it was lowered: machines aren&#39;t deactivated to match it. | 
**MaxOfflineDurationSeconds** | **int** | Longest the applications can run offline with the license: the license tokens returned by &#x60;validateKey&#x60; expire this long after they&#39;re issued, unless the license expires sooner. | 
**ActiveMachineCount** | **int** | Number of active machines the license is used on. | 
**LastActivatedAt** | **DateTime?** | Last time a machine validated the license key. &#x60;null&#x60; when it was never validated. | 
**MaxVersion** | [**LicenseMaxVersion**](LicenseMaxVersion.md) |  | 
**Price** | [**Price**](Price.md) |  | 
**Status** | **LicenseStatus** |  | 
**UpdatedAt** | **DateTime** | Last time the license&#39;s settings were edited, not when its key was validated. | 

[[Back to Model list]](../README.md#documentation-for-models) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to README]](../README.md)

