# LicenseManager.Model.SlackConnection

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**Id** | **string** |  | 
**TeamId** | **string** |  | 
**TeamName** | **string** |  | 
**ChannelId** | **string** |  | 
**ChannelName** | **string** | Name of the channel when it was connected, with its &#x60;#&#x60;. | 
**ConfigurationUrl** | **string** | Page of the installation in Slack. | 
**Events** | **List&lt;SlackConnection.EventsEnum&gt;** | Notifications the channel gets: &#x60;purchased&#x60; (a license bought through Stripe), &#x60;renewed&#x60; (a subscription renewal paid), &#x60;payment_failed&#x60; (a subscription payment failed) and &#x60;canceled&#x60; (a license canceled, or its subscription ended). | 
**Status** | **string** | &#x60;revoked&#x60; once Slack refuses the messages, like when the app was removed from the workspace or the channel deleted: remove it and add it again. | 
**StatusReason** | **string** |  | 
**LastSentAt** | **DateTime?** |  | 
**CreatedAt** | **DateTime** |  | 

[[Back to Model list]](../README.md#documentation-for-models) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to README]](../README.md)

