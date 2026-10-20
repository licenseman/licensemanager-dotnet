# LicenseManager.Model.Pagination
Where the returned page stands among all the items matching the filters. Pages are numbered from 1.

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**Page** | **int** | Number of the returned page, as requested. Pages are numbered from 1: &#x60;1&#x60; is the first page. | 
**PageSize** | **int** | Maximum number of items per page, as requested. &#x60;data&#x60; holds fewer items on the last page, and none past it. | 
**Total** | **int** | Number of items matching the filters, across all pages. &#x60;0&#x60; when nothing matches. | 
**TotalPages** | **int** | Number of pages, which is also the number of the last page. &#x60;0&#x60; when nothing matches. There&#39;s a next page while &#x60;page&#x60; is lower than &#x60;totalPages&#x60;. | 

[[Back to Model list]](../README.md#documentation-for-models) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to README]](../README.md)

