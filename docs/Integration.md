# LicenseManager.Model.Integration

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**Id** | **string** |  | 
**Provider** | **string** |  | 
**Livemode** | **bool** | Whether it&#39;s connected in live mode, for the live products, or in test mode, for the test products. | 
**AccountName** | **string** | Name of the Stripe account, &#x60;null&#x60; when the API key can&#39;t read it, and for Paddle, whose API doesn&#39;t give it. | 
**ApiKeyHint** | **string** | Start and end of the API key, to recognize it. | 
**WebhookUrl** | **string** | URL of the webhook endpoint created on the Stripe account, or of the notification destination created on the Paddle account. | 
**Status** | **IntegrationStatus** |  | 
**StatusReason** | **string** | Why the integration isn&#39;t &#x60;active&#x60;, &#x60;null&#x60; when it is. | 
**LastCheckedAt** | **DateTime?** | Last time its health was checked, done every day. | 
**LastEventAt** | **DateTime?** | Last time it received an event from the provider. | 
**AutoRefund** | **bool** | Whether canceling a license bought through the integration refunds its payment. On by default, always off when &#x60;canRefund&#x60; is false. | 
**CanRefund** | **bool** | Whether the API key has the optional refund permission (Stripe: Refunds: Write, Paddle: Adjustments: Write), checked when connecting and every day. Without it, canceled licenses aren&#39;t refunded: refund their payments from the provider. | 
**CanManageSubscriptions** | **bool** | Whether the API key has the optional Subscriptions: Write permission, checked when connecting and every day. Without it, subscription licenses can&#39;t be canceled from the app: cancel their subscriptions from the provider. | 
**CanBillingPortal** | **bool** | Whether the API key has the optional customer portal permission (Stripe: Customer portal: Write, Paddle: Customer portal sessions: Write), checked when connecting and every day. Without it, the license portal doesn&#39;t link to the provider&#39;s customer portal. | 
**SubscriptionGraceDays** | **int** | Days a subscription license stays valid after its period ends while its renewal is unpaid, as the provider retries the payment. 7 by default. | 
**CreatedAt** | **DateTime** |  | 

[[Back to Model list]](../README.md#documentation-for-models) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to README]](../README.md)

