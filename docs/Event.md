# LicenseManager.Model.Event

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**Id** | **string** |  | 
**Type** | **EventType** |  | 
**CreatedAt** | **DateTime** |  | 
**Payload** | **Dictionary&lt;string, Object&gt;** | Details of the event, depending on its &#x60;type&#x60;. | 
**PolicyId** | **string** |  | 
**LicenseId** | **string** |  | 
**MachineId** | **string** |  | 
**Machine** | [**EventMachine**](EventMachine.md) |  | 
**Actor** | [**EventActor**](EventActor.md) |  | 
**Country** | **string** | ISO 3166-1 alpha-2 code of the country of the IP address the request came from, for &#x60;license.validated&#x60; and &#x60;license.validation_failed&#x60; events. &#x60;null&#x60; until it&#39;s looked up, shortly after, or when it can&#39;t be. | 
**Latitude** | **decimal?** | Approximate latitude of the IP address the request came from, for &#x60;license.validated&#x60; and &#x60;license.validation_failed&#x60; events. &#x60;null&#x60; until it&#39;s looked up, shortly after, or when it can&#39;t be. | 
**Longitude** | **decimal?** | Approximate longitude of the IP address the request came from, for &#x60;license.validated&#x60; and &#x60;license.validation_failed&#x60; events. &#x60;null&#x60; until it&#39;s looked up, shortly after, or when it can&#39;t be. | 

[[Back to Model list]](../README.md#documentation-for-models) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to README]](../README.md)

