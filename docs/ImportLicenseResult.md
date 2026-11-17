# LicenseManager.Model.ImportLicenseResult

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**Index** | **int** | Position of the license in &#x60;licenses&#x60;, from 0. | 
**Key** | **string** |  | 
**Status** | **string** | &#x60;created&#x60;: imported. &#x60;skipped&#x60;: a license of the product already uses the key, like one imported before: it&#39;s left as is. &#x60;failed&#x60;: not imported, see &#x60;error&#x60;. | 
**LicenseId** | **string** | Id of the license created, or of the one using the key. | 
**Error** | [**ImportLicenseResultError**](ImportLicenseResultError.md) |  | 

[[Back to Model list]](../README.md#documentation-for-models) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to README]](../README.md)

