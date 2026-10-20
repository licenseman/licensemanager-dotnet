# LicenseManager.Model.LockMaxVersionMinorAfter
Time after the creation of a license its minor version is locked, in seconds or calendar months: it then only gets the bug fixes of the minor version released by then. Never shorter than `majorAfter`, whatever the length of the months: 1 month is longer than 28 days but may be shorter than 31. `0` locks it when the license is created. `null` to never lock it.

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**Value** | **int** |  | 
**Unit** | **string** | Calendar months: a license created on January 31 with a 1 month duration expires on the last day of February. | 

[[Back to Model list]](../README.md#documentation-for-models) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to README]](../README.md)

