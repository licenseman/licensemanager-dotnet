# LicenseManager.Model.Integration

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**Id** | **string** |  | 
**Provider** | **string** |  | 
**Livemode** | **bool** | Whether it&#39;s connected in live mode, for the live products, or in test mode, for the test products. | 
**AccountName** | **string** | Name of the Stripe account, &#x60;null&#x60; when the API key can&#39;t read it. | 
**ApiKeyHint** | **string** | Start and end of the API key, to recognize it. | 
**WebhookUrl** | **string** | URL of the webhook endpoint created on the Stripe account. | 
**Status** | **IntegrationStatus** |  | 
**StatusReason** | **string** | Why the integration isn&#39;t &#x60;active&#x60;, &#x60;null&#x60; when it is. | 
**LastCheckedAt** | **DateTime?** | Last time its health was checked, done every day. | 
**LastEventAt** | **DateTime?** | Last time it received an event from the provider. | 
**AutoRefund** | **bool** | Whether canceling a license bought through Stripe refunds its payment. On by default, always off when &#x60;canRefund&#x60; is false. | 
**CanRefund** | **bool** | Whether the API key has the optional Refunds: Write permission, checked when connecting and every day. Without it, canceled licenses aren&#39;t refunded: refund their payments from Stripe. | 
**CreatedAt** | **DateTime** |  | 

[[Back to Model list]](../README.md#documentation-for-models) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to README]](../README.md)

