# LicenseManager.Model.PolicySettings

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**Duration** | [**PolicySettingsDuration**](PolicySettingsDuration.md) |  | [optional] 
**MaxMachines** | **int?** | Maximum number of active machines of the licenses created with this policy, copied to each of them. &#x60;null&#x60; for no limit. Defaults to &#x60;null&#x60;. | [optional] 
**MaxOfflineDurationSeconds** | **int** | Longest the applications can run offline with the licenses created with this policy, in seconds, copied to each of them. At least one hour (&#x60;3600&#x60;). Defaults to one week. | [optional] 
**MaxVersion** | [**PolicySettingsMaxVersion**](PolicySettingsMaxVersion.md) |  | [optional] 

[[Back to Model list]](../README.md#documentation-for-models) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to README]](../README.md)

