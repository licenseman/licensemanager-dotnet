# LicenseManager.Model.Policy

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**Id** | **string** |  | 
**ProductId** | **string** |  | 
**Slug** | **string** |  | 
**Name** | **string** |  | 
**IsDefault** | **bool** | Whether this is the product&#39;s default policy. Each product has exactly one. | 
**Duration** | [**PolicyDuration**](PolicyDuration.md) |  | 
**MaxMachines** | **int?** | Maximum number of active machines of the licenses created with this policy. &#x60;null&#x60; when there&#39;s no limit. | 
**MaxOfflineDurationSeconds** | **int** | Longest the applications can run offline with the licenses created with this policy, in seconds. | 
**MaxVersion** | [**PolicyMaxVersion**](PolicyMaxVersion.md) |  | 
**LicenseCount** | **int** | Number of licenses following this policy. | 
**CreatedAt** | **DateTime** |  | 
**UpdatedAt** | **DateTime** |  | 

[[Back to Model list]](../README.md#documentation-for-models) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to README]](../README.md)

