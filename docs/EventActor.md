# LicenseManager.Model.EventActor
Who caused the event: a user of the app, an API key, a token, `automation` for the changes the app makes on its own, like applying the version locks, or `integration` for the changes of an integration, like the licenses a Stripe payment creates. `null` for requests that don't authenticate, like validating a license key.

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**Type** | **string** |  | 
**Id** | **string** | &#x60;null&#x60; when the integration has been disconnected. | 
**Name** | **string** |  | 
**Email** | **string** |  | 
**Image** | **string** | URL of the user&#39;s profile picture. | 
**Start** | **string** | First characters of the key, to recognize it. | 
**TokenType** | **string** | Type of resource the token is scoped to. | 
**SubjectId** | **string** | Id of the resource the token is scoped to. | 
**Provider** | **string** | Service the integration connects to. | 

[[Back to Model list]](../README.md#documentation-for-models) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to README]](../README.md)

