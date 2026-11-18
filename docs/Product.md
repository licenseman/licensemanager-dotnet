# LicenseManager.Model.Product

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**Id** | **string** |  | 
**Slug** | **string** |  | 
**Name** | **string** |  | 
**IsTestFromProductId** | **string** | For test products, id of the live product they&#39;re a sandbox of. &#x60;null&#x60; for live products. | 
**LogoUrl** | **string** | Public URL of the product&#39;s logo, shown in the web app and the customer portal. &#x60;null&#x60; without a logo. | 
**WebsiteUrl** | **string** | The product&#39;s website, linked from the customer portal, when its URL has no allowed &#x60;return_url&#x60;, and from the emails sent to customers. &#x60;null&#x60; for no link. | 
**DownloadUrl** | **string** | Where customers download the product, linked from the email sending their license keys. &#x60;null&#x60; for no link. | 
**Portal** | [**PortalSettings**](PortalSettings.md) |  | 
**AutoMachineChange** | **bool** | Whether a new machine validating a license already on its max machines takes the place of the license&#39;s machine validated the longest ago, rather than being refused with &#x60;machine_limit_reached&#x60;. When the replaced machine is validated again, it takes its place back and the machine that replaced it is locked. See &#x60;validateKey&#x60;. | 
**CreatedAt** | **DateTime** |  | 
**UpdatedAt** | **DateTime** |  | 

[[Back to Model list]](../README.md#documentation-for-models) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to README]](../README.md)

