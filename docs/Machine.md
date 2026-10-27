# LicenseManager.Model.Machine

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**Id** | **string** |  | 
**LicenseId** | **string** |  | 
**Fingerprint** | **string** | Identifies the machine. Unique within the license. | 
**Platform** | **string** |  | 
**Name** | **string** |  | 
**Status** | **string** | Whether the machine counts as using the license. A &#x60;locked&#x60; machine doesn&#39;t, and its validations are refused with &#x60;machine_locked&#x60;: it overrode a machine that came back. See &#x60;validateKey&#x60;. | 
**VarVersion** | **string** | Version of the application last validated on the machine. | 
**OverriddenByMachineId** | **string** | For a machine deactivated or locked by automatic machine changes, the machine that took its place. Validating the key on a deactivated machine that has one takes its place back. &#x60;null&#x60; otherwise. | 
**LastValidatedAt** | **DateTime?** | When the license was last validated on the machine. | 
**CreatedAt** | **DateTime** |  | 
**UpdatedAt** | **DateTime** |  | 

[[Back to Model list]](../README.md#documentation-for-models) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to README]](../README.md)

