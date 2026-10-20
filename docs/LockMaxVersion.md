# LicenseManager.Model.LockMaxVersion
The licenses can use every version released after their creation, until their major version locks `majorAfter` it, then the updates of their major version until their minor version locks `minorAfter` it, if ever. Bug fixes are never locked.

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**Type** | **string** |  | 
**MajorAfter** | [**LockMaxVersionMajorAfter**](LockMaxVersionMajorAfter.md) |  | 
**MinorAfter** | [**LockMaxVersionMinorAfter**](LockMaxVersionMinorAfter.md) |  | 

[[Back to Model list]](../README.md#documentation-for-models) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to README]](../README.md)

