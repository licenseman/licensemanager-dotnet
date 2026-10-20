# LicenseManager.Model.StripeIntegration

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**Livemode** | **bool** | Mode of the Stripe connection the product uses: live for live products, test for test products. | 
**WebhookUrlReachable** | **bool** | Whether Stripe can reach the API&#39;s webhook URL. A local URL can&#39;t be: set &#x60;WEBHOOK_URL&#x60; on the server, like to a tunnel in development. | 
**RequiredPermissions** | [**List&lt;StripePermission&gt;**](StripePermission.md) | Permissions the restricted API key needs, and why. Every other permission can stay &#x60;None&#x60;. | 
**Integration** | [**Integration**](Integration.md) | The organization&#39;s Stripe connection in this mode, &#x60;null&#x60; when there&#39;s none. | 
**Mappings** | [**List&lt;IntegrationMapping&gt;**](IntegrationMapping.md) | Stripe prices creating licenses of the product. | 

[[Back to Model list]](../README.md#documentation-for-models) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to README]](../README.md)

