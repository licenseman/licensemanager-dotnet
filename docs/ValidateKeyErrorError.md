# LicenseManager.Model.ValidateKeyErrorError

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**Code** | **string** |  | 
**Message** | **string** |  | 
**Issues** | [**List&lt;ErrorErrorIssuesInner&gt;**](ErrorErrorIssuesInner.md) | Present on &#x60;validation_error&#x60; errors. | [optional] 
**LatestAllowedVersion** | **string** | On &#x60;version_not_allowed&#x60; errors: version of the latest stable release of the product the license allows, among the ones already released. &#x60;null&#x60; when it allows none of them. | [optional] 

[[Back to Model list]](../README.md#documentation-for-models) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to README]](../README.md)

