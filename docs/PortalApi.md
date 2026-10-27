# LicenseManager.Api.PortalApi

All URIs are relative to *https://api.licensemanager.dev*

| Method | HTTP request | Description |
|--------|--------------|-------------|
| [**CreatePortalLink**](PortalApi.md#createportallink) | **POST** /v1/customers/{id}/portal-links | Create a link to the customer portal |
| [**GetPortal**](PortalApi.md#getportal) | **GET** /v1/portal/{productId} | Get the customer portal of a product |
| [**RequestPortalLink**](PortalApi.md#requestportallink) | **POST** /v1/portal/{productId}/request-link | Email a link to the customer portal |
| [**SendPortalLink**](PortalApi.md#sendportallink) | **POST** /v1/customers/{id}/portal-links/send | Email a link to the customer portal to the customer |

<a id="createportallink"></a>
# **CreatePortalLink**
> PortalLink CreatePortalLink (string id, CreatePortalLink createPortalLink)

Create a link to the customer portal

Link letting the customer see their licenses, cancel them during their money back guarantee, and deactivate their machines in the customer portal, without signing in. Anyone with the link can, until it expires or the customer is deleted: it can't be revoked otherwise. The token also works with the API endpoints that accept customer tokens.  Links can be created while the product's customer portal is disabled, but the portal answers `404` until it's enabled, and `sendPortalLink` refuses to email them.  **Required role permission**: `portalLink:create` when called with a session, granted by the member's role. API keys aren't limited by roles.

### Example
```csharp
using System.Collections.Generic;
using System.Diagnostics;
using System.Net.Http;
using LicenseManager.Api;
using LicenseManager.Client;
using LicenseManager.Model;

namespace Example
{
    public class CreatePortalLinkExample
    {
        public static void Main()
        {
            Configuration config = new Configuration();
            config.BasePath = "https://api.licensemanager.dev";
            // Configure API key authorization: apiKey
            config.AddApiKey("x-api-key", "YOUR_API_KEY");
            // Uncomment below to setup prefix (e.g. Bearer) for API key, if needed
            // config.AddApiKeyPrefix("x-api-key", "Bearer");

            // create instances of HttpClient, HttpClientHandler to be reused later with different Api classes
            HttpClient httpClient = new HttpClient();
            HttpClientHandler httpClientHandler = new HttpClientHandler();
            var apiInstance = new PortalApi(httpClient, config, httpClientHandler);
            var id = c9Wd3RtE;  // string | 
            var createPortalLink = new CreatePortalLink(); // CreatePortalLink | 

            try
            {
                // Create a link to the customer portal
                PortalLink result = apiInstance.CreatePortalLink(id, createPortalLink);
                Debug.WriteLine(result);
            }
            catch (ApiException  e)
            {
                Debug.Print("Exception when calling PortalApi.CreatePortalLink: " + e.Message);
                Debug.Print("Status Code: " + e.ErrorCode);
                Debug.Print(e.StackTrace);
            }
        }
    }
}
```

#### Using the CreatePortalLinkWithHttpInfo variant
This returns an ApiResponse object which contains the response data, status code and headers.

```csharp
try
{
    // Create a link to the customer portal
    ApiResponse<PortalLink> response = apiInstance.CreatePortalLinkWithHttpInfo(id, createPortalLink);
    Debug.Write("Status Code: " + response.StatusCode);
    Debug.Write("Response Headers: " + response.Headers);
    Debug.Write("Response Body: " + response.Data);
}
catch (ApiException e)
{
    Debug.Print("Exception when calling PortalApi.CreatePortalLinkWithHttpInfo: " + e.Message);
    Debug.Print("Status Code: " + e.ErrorCode);
    Debug.Print(e.StackTrace);
}
```

### Parameters

| Name | Type | Description | Notes |
|------|------|-------------|-------|
| **id** | **string** |  |  |
| **createPortalLink** | [**CreatePortalLink**](CreatePortalLink.md) |  |  |

### Return type

[**PortalLink**](PortalLink.md)

### Authorization

[apiKey](../README.md#apiKey)

### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: application/json


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **201** | Created link |  -  |
| **401** | &#x60;unauthorized&#x60;: no credentials. &#x60;invalid_api_key&#x60;: the API key doesn&#39;t exist, was revoked or has expired. &#x60;invalid_token&#x60;: the token&#39;s signature is invalid, it has expired, or the resource it&#39;s scoped to was deleted |  -  |
| **402** | &#x60;plan_limit_exceeded&#x60;: the organization stayed over its plan&#39;s limits after the grace period, its API is blocked until it upgrades. &#x60;plan_limit_reached&#x60;: creating the resource would go over the plan&#39;s limit |  -  |
| **403** | &#x60;token_not_allowed&#x60;: the endpoint doesn&#39;t accept tokens, or not of this type. &#x60;insufficient_scope&#x60;: the token lacks the permission. &#x60;no_active_organization&#x60; or &#x60;forbidden&#x60;: the session has no organization, or isn&#39;t a member of the one requested |  -  |
| **404** | Customer not found |  -  |
| **422** | &#x60;validation_error&#x60;: invalid path, query or body, with the &#x60;issues&#x60; |  -  |
| **429** | &#x60;rate_limited&#x60;: the API key made more than 10 requests in the last second. Wait for the &#x60;Retry-After&#x60; seconds |  -  |

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

<a id="getportal"></a>
# **GetPortal**
> Portal GetPortal (string productId, string returnUrl = null)

Get the customer portal of a product

Names of the product and of its organization, colors of the customer portal, and link back to the product's website. Answers `404` when the product's customer portal is disabled: with the `portal_disabled` code and the slugs of the product and its organization when signed in as a member of the organization, so they can enable it. Doesn't need authentication.

### Example
```csharp
using System.Collections.Generic;
using System.Diagnostics;
using System.Net.Http;
using LicenseManager.Api;
using LicenseManager.Client;
using LicenseManager.Model;

namespace Example
{
    public class GetPortalExample
    {
        public static void Main()
        {
            Configuration config = new Configuration();
            config.BasePath = "https://api.licensemanager.dev";
            // create instances of HttpClient, HttpClientHandler to be reused later with different Api classes
            HttpClient httpClient = new HttpClient();
            HttpClientHandler httpClientHandler = new HttpClientHandler();
            var apiInstance = new PortalApi(httpClient, config, httpClientHandler);
            var productId = x7Kp2QaZ;  // string | 
            var returnUrl = https://example.com/account;  // string | Link back to your website to show, used when its domain is one of the product's `returnDomains`. (optional) 

            try
            {
                // Get the customer portal of a product
                Portal result = apiInstance.GetPortal(productId, returnUrl);
                Debug.WriteLine(result);
            }
            catch (ApiException  e)
            {
                Debug.Print("Exception when calling PortalApi.GetPortal: " + e.Message);
                Debug.Print("Status Code: " + e.ErrorCode);
                Debug.Print(e.StackTrace);
            }
        }
    }
}
```

#### Using the GetPortalWithHttpInfo variant
This returns an ApiResponse object which contains the response data, status code and headers.

```csharp
try
{
    // Get the customer portal of a product
    ApiResponse<Portal> response = apiInstance.GetPortalWithHttpInfo(productId, returnUrl);
    Debug.Write("Status Code: " + response.StatusCode);
    Debug.Write("Response Headers: " + response.Headers);
    Debug.Write("Response Body: " + response.Data);
}
catch (ApiException e)
{
    Debug.Print("Exception when calling PortalApi.GetPortalWithHttpInfo: " + e.Message);
    Debug.Print("Status Code: " + e.ErrorCode);
    Debug.Print(e.StackTrace);
}
```

### Parameters

| Name | Type | Description | Notes |
|------|------|-------------|-------|
| **productId** | **string** |  |  |
| **returnUrl** | **string** | Link back to your website to show, used when its domain is one of the product&#39;s &#x60;returnDomains&#x60;. | [optional]  |

### Return type

[**Portal**](Portal.md)

### Authorization

No authorization required

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **200** | Customer portal |  -  |
| **404** | &#x60;not_found&#x60;: product not found, or its customer portal is disabled. &#x60;portal_disabled&#x60;: its customer portal is disabled, for members of its organization |  -  |

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

<a id="requestportallink"></a>
# **RequestPortalLink**
> void RequestPortalLink (string productId, RequestPortalLink requestPortalLink)

Email a link to the customer portal

Emails the customer of the product with this email a link to the customer portal, working for 1 hour. Answers `404` when the product's customer portal is disabled. Answers the same whether the customer exists or not, so the API doesn't tell which emails are customers. Test products only email the members of the organization: the link isn't sent to other customers, with the same answer. Doesn't need authentication.

### Example
```csharp
using System.Collections.Generic;
using System.Diagnostics;
using System.Net.Http;
using LicenseManager.Api;
using LicenseManager.Client;
using LicenseManager.Model;

namespace Example
{
    public class RequestPortalLinkExample
    {
        public static void Main()
        {
            Configuration config = new Configuration();
            config.BasePath = "https://api.licensemanager.dev";
            // create instances of HttpClient, HttpClientHandler to be reused later with different Api classes
            HttpClient httpClient = new HttpClient();
            HttpClientHandler httpClientHandler = new HttpClientHandler();
            var apiInstance = new PortalApi(httpClient, config, httpClientHandler);
            var productId = x7Kp2QaZ;  // string | 
            var requestPortalLink = new RequestPortalLink(); // RequestPortalLink | 

            try
            {
                // Email a link to the customer portal
                apiInstance.RequestPortalLink(productId, requestPortalLink);
            }
            catch (ApiException  e)
            {
                Debug.Print("Exception when calling PortalApi.RequestPortalLink: " + e.Message);
                Debug.Print("Status Code: " + e.ErrorCode);
                Debug.Print(e.StackTrace);
            }
        }
    }
}
```

#### Using the RequestPortalLinkWithHttpInfo variant
This returns an ApiResponse object which contains the response data, status code and headers.

```csharp
try
{
    // Email a link to the customer portal
    apiInstance.RequestPortalLinkWithHttpInfo(productId, requestPortalLink);
}
catch (ApiException e)
{
    Debug.Print("Exception when calling PortalApi.RequestPortalLinkWithHttpInfo: " + e.Message);
    Debug.Print("Status Code: " + e.ErrorCode);
    Debug.Print(e.StackTrace);
}
```

### Parameters

| Name | Type | Description | Notes |
|------|------|-------------|-------|
| **productId** | **string** |  |  |
| **requestPortalLink** | [**RequestPortalLink**](RequestPortalLink.md) |  |  |

### Return type

void (empty response body)

### Authorization

No authorization required

### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: application/json


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **204** | Link emailed, if the customer exists |  -  |
| **404** | &#x60;not_found&#x60;: product not found, or its customer portal is disabled |  -  |
| **422** | Validation error |  -  |

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

<a id="sendportallink"></a>
# **SendPortalLink**
> void SendPortalLink (string id, SendPortalLink sendPortalLink)

Email a link to the customer portal to the customer

Emails a link created with `createPortalLink` to the customer's email. Fails while the product's customer portal is disabled, and, in test products, when the customer's email isn't a member's of the organization: test products only email members, so testing never emails real customers.  **Required role permission**: `portalLink:create` when called with a session, granted by the member's role. API keys aren't limited by roles.

### Example
```csharp
using System.Collections.Generic;
using System.Diagnostics;
using System.Net.Http;
using LicenseManager.Api;
using LicenseManager.Client;
using LicenseManager.Model;

namespace Example
{
    public class SendPortalLinkExample
    {
        public static void Main()
        {
            Configuration config = new Configuration();
            config.BasePath = "https://api.licensemanager.dev";
            // Configure API key authorization: apiKey
            config.AddApiKey("x-api-key", "YOUR_API_KEY");
            // Uncomment below to setup prefix (e.g. Bearer) for API key, if needed
            // config.AddApiKeyPrefix("x-api-key", "Bearer");

            // create instances of HttpClient, HttpClientHandler to be reused later with different Api classes
            HttpClient httpClient = new HttpClient();
            HttpClientHandler httpClientHandler = new HttpClientHandler();
            var apiInstance = new PortalApi(httpClient, config, httpClientHandler);
            var id = c9Wd3RtE;  // string | 
            var sendPortalLink = new SendPortalLink(); // SendPortalLink | 

            try
            {
                // Email a link to the customer portal to the customer
                apiInstance.SendPortalLink(id, sendPortalLink);
            }
            catch (ApiException  e)
            {
                Debug.Print("Exception when calling PortalApi.SendPortalLink: " + e.Message);
                Debug.Print("Status Code: " + e.ErrorCode);
                Debug.Print(e.StackTrace);
            }
        }
    }
}
```

#### Using the SendPortalLinkWithHttpInfo variant
This returns an ApiResponse object which contains the response data, status code and headers.

```csharp
try
{
    // Email a link to the customer portal to the customer
    apiInstance.SendPortalLinkWithHttpInfo(id, sendPortalLink);
}
catch (ApiException e)
{
    Debug.Print("Exception when calling PortalApi.SendPortalLinkWithHttpInfo: " + e.Message);
    Debug.Print("Status Code: " + e.ErrorCode);
    Debug.Print(e.StackTrace);
}
```

### Parameters

| Name | Type | Description | Notes |
|------|------|-------------|-------|
| **id** | **string** |  |  |
| **sendPortalLink** | [**SendPortalLink**](SendPortalLink.md) |  |  |

### Return type

void (empty response body)

### Authorization

[apiKey](../README.md#apiKey)

### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: application/json


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **204** | Link emailed |  -  |
| **401** | &#x60;unauthorized&#x60;: no credentials. &#x60;invalid_api_key&#x60;: the API key doesn&#39;t exist, was revoked or has expired. &#x60;invalid_token&#x60;: the token&#39;s signature is invalid, it has expired, or the resource it&#39;s scoped to was deleted |  -  |
| **402** | &#x60;plan_limit_exceeded&#x60;: the organization stayed over its plan&#39;s limits after the grace period, its API is blocked until it upgrades. &#x60;plan_limit_reached&#x60;: creating the resource would go over the plan&#39;s limit |  -  |
| **403** | &#x60;token_not_allowed&#x60;: the endpoint doesn&#39;t accept tokens, or not of this type. &#x60;insufficient_scope&#x60;: the token lacks the permission. &#x60;no_active_organization&#x60; or &#x60;forbidden&#x60;: the session has no organization, or isn&#39;t a member of the one requested |  -  |
| **404** | Customer not found |  -  |
| **409** | &#x60;portal_disabled&#x60;: the product&#39;s customer portal is disabled. &#x60;test_recipient_not_member&#x60;: the product is a test product, and the customer&#39;s email isn&#39;t a member&#39;s of the organization |  -  |
| **422** | &#x60;validation_error&#x60;: invalid body. &#x60;invalid_token&#x60;: the token isn&#39;t valid, has expired, or isn&#39;t a customer token of this customer |  -  |
| **429** | &#x60;rate_limited&#x60;: the API key made more than 10 requests in the last second. Wait for the &#x60;Retry-After&#x60; seconds |  -  |

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

