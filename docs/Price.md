# LicenseManager.Model.Price
Price paid for a license. Licenses have `null` instead when it's unknown, which leaves them out of the revenue stats.

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**Amount** | **decimal** | Amount in major units of the currency: &#x60;49.99&#x60; for $49.99, &#x60;5000&#x60; for ¥5,000. &#x60;0&#x60; for a free license. | 
**Currency** | **string** | ISO 4217 code of the currency, in upper case. | 

[[Back to Model list]](../README.md#documentation-for-models) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to README]](../README.md)

