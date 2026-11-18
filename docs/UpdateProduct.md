# LicenseManager.Model.UpdateProduct

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**Name** | **string** |  | [optional] 
**Slug** | **string** | Unique within the organization. Defaults to the name, lower cased, without accents and special characters. Starts with &#x60;test_&#x60; in test products, which is added when missing, and removed in live products. | [optional] 
**WebsiteUrl** | **string** | The product&#39;s website, linked from the customer portal, when its URL has no allowed &#x60;return_url&#x60;, and from the emails sent to customers. &#x60;null&#x60; for no link. | [optional] 
**DownloadUrl** | **string** | Where customers download the product, linked from the email sending their license keys. &#x60;null&#x60; for no link. | [optional] 
**Portal** | [**UpdateProductPortal**](UpdateProductPortal.md) |  | [optional] 
**AutoMachineChange** | **bool** | Whether a new machine validating a license already on its max machines takes the place of the license&#39;s machine validated the longest ago, rather than being refused with &#x60;machine_limit_reached&#x60;. When the replaced machine is validated again, it takes its place back and the machine that replaced it is locked. See &#x60;validateKey&#x60;. | [optional] 

[[Back to Model list]](../README.md#documentation-for-models) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to README]](../README.md)

