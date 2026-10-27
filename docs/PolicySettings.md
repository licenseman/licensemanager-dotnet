# LicenseManager.Model.PolicySettings

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**Duration** | [**PolicySettingsDuration**](PolicySettingsDuration.md) |  | [optional] 
**MaxMachines** | **int?** | Maximum number of active machines of the licenses created with this policy, copied to each of them. &#x60;null&#x60; for no limit. Defaults to &#x60;null&#x60;. | [optional] 
**MaxOfflineDurationSeconds** | **int** | Longest the applications can run offline with the licenses created with this policy, in seconds, copied to each of them. At least one hour (&#x60;3600&#x60;). Defaults to one week. | [optional] 
**MaxVersion** | [**PolicySettingsMaxVersion**](PolicySettingsMaxVersion.md) |  | [optional] 
**MoneyBackGuaranteeDays** | **int?** | Number of days after their creation during which customers can cancel the licenses created with this policy, from the customer portal or with &#x60;cancelLicense&#x60;, which refunds their Stripe payment. Each license keeps the end of its own period as &#x60;cancellableUntil&#x60;. &#x60;null&#x60; for no money back guarantee. Defaults to &#x60;null&#x60;. | [optional] 

[[Back to Model list]](../README.md#documentation-for-models) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to README]](../README.md)

