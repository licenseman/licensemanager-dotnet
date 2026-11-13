# LicenseManager.Model.PaddleIntegration

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**Livemode** | **bool** | Environment of the Paddle connection the product uses: live for live products, sandbox for test products. | 
**WebhookUrlReachable** | **bool** | Whether Paddle can reach the API&#39;s webhook URL. A local URL can&#39;t be: set &#x60;WEBHOOK_URL&#x60; on the server, like to a tunnel in development. | 
**RequiredPermissions** | [**List&lt;PaddlePermission&gt;**](PaddlePermission.md) | Permissions the API key needs, and why, the &#x60;optional&#x60; ones included. Every other permission can stay off. | 
**Integration** | [**Integration**](Integration.md) | The organization&#39;s Paddle connection in this environment, &#x60;null&#x60; when there&#39;s none. | 
**Mappings** | [**List&lt;IntegrationMapping&gt;**](IntegrationMapping.md) | Paddle prices creating licenses of the product. | 

[[Back to Model list]](../README.md#documentation-for-models) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to README]](../README.md)

