# LicenseManager.Model.UpdatePolicy

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**Name** | **string** |  | [optional] 
**Slug** | **string** | Unique within the product. Defaults to the name, lower cased, without accents and special characters. Starts with &#x60;test_&#x60; in test products, which is added when missing, and removed in live products. | [optional] 
**IsDefault** | **bool** | &#x60;true&#x60; makes this policy the product&#39;s default, in place of the current one. | [optional] 
**Duration** | [**PolicySettingsDuration**](PolicySettingsDuration.md) |  | [optional] 
**MaxMachines** | **int?** | Maximum number of active machines of the licenses created with this policy, copied to each of them. &#x60;null&#x60; for no limit. Defaults to &#x60;null&#x60;. | [optional] 
**MaxOfflineDurationSeconds** | **int** | Longest the applications can run offline with the licenses created with this policy, in seconds, copied to each of them. At least one hour (&#x60;3600&#x60;). Defaults to one week. | [optional] 
**MaxVersion** | [**PolicySettingsMaxVersion**](PolicySettingsMaxVersion.md) |  | [optional] 

[[Back to Model list]](../README.md#documentation-for-models) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to README]](../README.md)

