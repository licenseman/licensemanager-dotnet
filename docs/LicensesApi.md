# LicenseManager.Api.LicensesApi

All URIs are relative to *https://api.licensemanager.dev*

| Method | HTTP request | Description |
|--------|--------------|-------------|
| [**CancelLicense**](LicensesApi.md#cancellicense) | **POST** /v1/licenses/{id}/cancel | Cancel a license |
| [**CreateLicense**](LicensesApi.md#createlicense) | **POST** /v1/products/{productId}/licenses | Create a license |
| [**DeleteLicense**](LicensesApi.md#deletelicense) | **DELETE** /v1/licenses/{id} | Delete a license |
| [**GetLicense**](LicensesApi.md#getlicense) | **GET** /v1/licenses/{id} | Get a license |
| [**GetLicenseStats**](LicensesApi.md#getlicensestats) | **GET** /v1/licenses/{id}/stats | Get the stats of a license |
| [**GetSigningKey**](LicensesApi.md#getsigningkey) | **GET** /v1/signing-key | Get the organization&#39;s signing key |
| [**ListCustomerLicenses**](LicensesApi.md#listcustomerlicenses) | **GET** /v1/customers/{customerId}/licenses | List the licenses of a customer |
| [**ListLicenses**](LicensesApi.md#listlicenses) | **GET** /v1/products/{productId}/licenses | List the licenses of a product |
| [**SendLicenseKeys**](LicensesApi.md#sendlicensekeys) | **POST** /v1/licenses/send-keys | Email license keys to their customers |
| [**UpdateLicense**](LicensesApi.md#updatelicense) | **PATCH** /v1/licenses/{id} | Update a license |
| [**ValidateKey**](LicensesApi.md#validatekey) | **POST** /v1/products/{productId}/validate-key | Validate a license key |

<a id="cancellicense"></a>
# **CancelLicense**
> License CancelLicense (string id, CancelLicense cancelLicense)

Cancel a license

Cancels the license right away: validating its key then fails with `license_expired`, like an expired license, and its status is `canceled`. A cancellation can't be undone.  Customers can cancel their licenses until their `cancellableUntil`, the end of their money back guarantee: tokens can't cancel a license past it, or without one. API keys and sessions can cancel any license.  When the license was bought through the Stripe integration, its payment is refunded in the background, unless the integration disables `autoRefund`, its API key lacks the optional Refunds: Write permission (`canRefund`), or `refund` is `false`: the refund is its price paid, taxes included, and its id is set as `stripeRefundId`. The customer is emailed a confirmation, and the owners and admins of the organization are told about the cancellation and its refund. In test products, the customer is only emailed when their email is a member's of the organization.  Records a `license.canceled` event, then a `license.refunded` or `license.refund_failed` one once the refund is done.  **Token access**: customer, license tokens with the `license:cancel` permission (or the matching write one). A token reaches the license it's scoped to, or the licenses of its customer.  **Required role permission**: `license:cancel` when called with a session, granted by the member's role. API keys aren't limited by roles.

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
    public class CancelLicenseExample
    {
        public static void Main()
        {
            Configuration config = new Configuration();
            config.BasePath = "https://api.licensemanager.dev";
            // Configure API key authorization: apiKey
            config.AddApiKey("x-api-key", "YOUR_API_KEY");
            // Uncomment below to setup prefix (e.g. Bearer) for API key, if needed
            // config.AddApiKeyPrefix("x-api-key", "Bearer");
            // Configure Bearer token for authorization: token
            config.AccessToken = "YOUR_BEARER_TOKEN";

            // create instances of HttpClient, HttpClientHandler to be reused later with different Api classes
            HttpClient httpClient = new HttpClient();
            HttpClientHandler httpClientHandler = new HttpClientHandler();
            var apiInstance = new LicensesApi(httpClient, config, httpClientHandler);
            var id = l3Nv8KwB;  // string | 
            var cancelLicense = new CancelLicense(); // CancelLicense | 

            try
            {
                // Cancel a license
                License result = apiInstance.CancelLicense(id, cancelLicense);
                Debug.WriteLine(result);
            }
            catch (ApiException  e)
            {
                Debug.Print("Exception when calling LicensesApi.CancelLicense: " + e.Message);
                Debug.Print("Status Code: " + e.ErrorCode);
                Debug.Print(e.StackTrace);
            }
        }
    }
}
```

#### Using the CancelLicenseWithHttpInfo variant
This returns an ApiResponse object which contains the response data, status code and headers.

```csharp
try
{
    // Cancel a license
    ApiResponse<License> response = apiInstance.CancelLicenseWithHttpInfo(id, cancelLicense);
    Debug.Write("Status Code: " + response.StatusCode);
    Debug.Write("Response Headers: " + response.Headers);
    Debug.Write("Response Body: " + response.Data);
}
catch (ApiException e)
{
    Debug.Print("Exception when calling LicensesApi.CancelLicenseWithHttpInfo: " + e.Message);
    Debug.Print("Status Code: " + e.ErrorCode);
    Debug.Print(e.StackTrace);
}
```

### Parameters

| Name | Type | Description | Notes |
|------|------|-------------|-------|
| **id** | **string** |  |  |
| **cancelLicense** | [**CancelLicense**](CancelLicense.md) |  |  |

### Return type

[**License**](License.md)

### Authorization

[apiKey](../README.md#apiKey), [token](../README.md#token)

### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: application/json


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **200** | Canceled license |  -  |
| **401** | &#x60;unauthorized&#x60;: no credentials. &#x60;invalid_api_key&#x60;: the API key doesn&#39;t exist, was revoked or has expired. &#x60;invalid_token&#x60;: the token&#39;s signature is invalid, it has expired, or the resource it&#39;s scoped to was deleted |  -  |
| **402** | &#x60;plan_limit_exceeded&#x60;: the organization stayed over its plan&#39;s limits after the grace period, its API is blocked until it upgrades. &#x60;plan_limit_reached&#x60;: creating the resource would go over the plan&#39;s limit |  -  |
| **403** | &#x60;token_not_allowed&#x60;: the endpoint doesn&#39;t accept tokens, or not of this type. &#x60;insufficient_scope&#x60;: the token lacks the permission. &#x60;no_active_organization&#x60; or &#x60;forbidden&#x60;: the session has no organization, or isn&#39;t a member of the one requested |  -  |
| **404** | License not found |  -  |
| **409** | &#x60;already_canceled&#x60;: the license is already canceled. &#x60;not_cancellable&#x60;: for tokens, the license has no money back guarantee, or it has ended |  -  |
| **422** | &#x60;validation_error&#x60;: invalid path, query or body, with the &#x60;issues&#x60; |  -  |
| **429** | &#x60;rate_limited&#x60;: the API key made more than 10 requests in the last second. Wait for the &#x60;Retry-After&#x60; seconds |  -  |

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

<a id="createlicense"></a>
# **CreateLicense**
> License CreateLicense (string productId, CreateLicense createLicense)

Create a license

Without a `key`, the license gets a random one, like `7KQ2M-X9ZPA-H4TRC-WN6EY-B3JDF`: 5 groups of 5 characters separated by dashes, each character an upper case letter or a digit other than `O`, `0`, `I` and `1`. That's 32 possible characters encoding 5 bits each, for 125 random bits.  Without a `policyId`, the license follows the product's default policy.  Without an `expiresAt`, the license expires after the duration of its policy, or never when the policy has none. `expiresAt: null` makes it never expire.  Without a `price`, the price paid for the license is unknown: it's left out of the revenue stats.  Without a `cancellableUntil`, the customer can cancel the license during the policy's `moneyBackGuaranteeDays` after its creation, or never when the policy has none.  The values of `maxVersion` left out are taken from the max version of the policy: its hard-coded version, or the times after the creation of the license its versions lock.  The license belongs to the product's customer with the given `email`, which is created when there's none.  With `sendKey: true`, the key is emailed to the customer once the license is created.  The license copies the settings of its policy when it's created: later changes to the policy don't affect it. Its key, policy and customer can't be changed afterwards.  **Required role permission**: `license:create` when called with a session, granted by the member's role. API keys aren't limited by roles.

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
    public class CreateLicenseExample
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
            var apiInstance = new LicensesApi(httpClient, config, httpClientHandler);
            var productId = x7Kp2QaZ;  // string | 
            var createLicense = new CreateLicense(); // CreateLicense | 

            try
            {
                // Create a license
                License result = apiInstance.CreateLicense(productId, createLicense);
                Debug.WriteLine(result);
            }
            catch (ApiException  e)
            {
                Debug.Print("Exception when calling LicensesApi.CreateLicense: " + e.Message);
                Debug.Print("Status Code: " + e.ErrorCode);
                Debug.Print(e.StackTrace);
            }
        }
    }
}
```

#### Using the CreateLicenseWithHttpInfo variant
This returns an ApiResponse object which contains the response data, status code and headers.

```csharp
try
{
    // Create a license
    ApiResponse<License> response = apiInstance.CreateLicenseWithHttpInfo(productId, createLicense);
    Debug.Write("Status Code: " + response.StatusCode);
    Debug.Write("Response Headers: " + response.Headers);
    Debug.Write("Response Body: " + response.Data);
}
catch (ApiException e)
{
    Debug.Print("Exception when calling LicensesApi.CreateLicenseWithHttpInfo: " + e.Message);
    Debug.Print("Status Code: " + e.ErrorCode);
    Debug.Print(e.StackTrace);
}
```

### Parameters

| Name | Type | Description | Notes |
|------|------|-------------|-------|
| **productId** | **string** |  |  |
| **createLicense** | [**CreateLicense**](CreateLicense.md) |  |  |

### Return type

[**License**](License.md)

### Authorization

[apiKey](../README.md#apiKey)

### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: application/json


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **201** | Created license |  -  |
| **401** | &#x60;unauthorized&#x60;: no credentials. &#x60;invalid_api_key&#x60;: the API key doesn&#39;t exist, was revoked or has expired. &#x60;invalid_token&#x60;: the token&#39;s signature is invalid, it has expired, or the resource it&#39;s scoped to was deleted |  -  |
| **402** | &#x60;plan_limit_exceeded&#x60;: the organization stayed over its plan&#39;s limits after the grace period, its API is blocked until it upgrades. &#x60;plan_limit_reached&#x60;: creating the resource would go over the plan&#39;s limit |  -  |
| **403** | &#x60;token_not_allowed&#x60;: the endpoint doesn&#39;t accept tokens, or not of this type. &#x60;insufficient_scope&#x60;: the token lacks the permission. &#x60;no_active_organization&#x60; or &#x60;forbidden&#x60;: the session has no organization, or isn&#39;t a member of the one requested |  -  |
| **404** | &#x60;not_found&#x60;: product not found. &#x60;policy_not_found&#x60;: the product has no policy with this &#x60;policyId&#x60; |  -  |
| **409** | &#x60;key_taken&#x60;: key already used by another license of the product |  -  |
| **422** | &#x60;validation_error&#x60;: invalid path, query or body, with the &#x60;issues&#x60; |  -  |
| **429** | &#x60;rate_limited&#x60;: the API key made more than 10 requests in the last second. Wait for the &#x60;Retry-After&#x60; seconds |  -  |

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

<a id="deletelicense"></a>
# **DeleteLicense**
> void DeleteLicense (string id)

Delete a license

Deletes the license along with its deactivated machines. A license used on active machines can't be deleted: deactivate them first. The tokens scoped to the license or its machines stop working, but the license tokens `validateKey` already returned stay valid until they expire. Its events can no longer be listed.  **Required role permission**: `license:delete` when called with a session, granted by the member's role. API keys aren't limited by roles.

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
    public class DeleteLicenseExample
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
            var apiInstance = new LicensesApi(httpClient, config, httpClientHandler);
            var id = l3Nv8KwB;  // string | 

            try
            {
                // Delete a license
                apiInstance.DeleteLicense(id);
            }
            catch (ApiException  e)
            {
                Debug.Print("Exception when calling LicensesApi.DeleteLicense: " + e.Message);
                Debug.Print("Status Code: " + e.ErrorCode);
                Debug.Print(e.StackTrace);
            }
        }
    }
}
```

#### Using the DeleteLicenseWithHttpInfo variant
This returns an ApiResponse object which contains the response data, status code and headers.

```csharp
try
{
    // Delete a license
    apiInstance.DeleteLicenseWithHttpInfo(id);
}
catch (ApiException e)
{
    Debug.Print("Exception when calling LicensesApi.DeleteLicenseWithHttpInfo: " + e.Message);
    Debug.Print("Status Code: " + e.ErrorCode);
    Debug.Print(e.StackTrace);
}
```

### Parameters

| Name | Type | Description | Notes |
|------|------|-------------|-------|
| **id** | **string** |  |  |

### Return type

void (empty response body)

### Authorization

[apiKey](../README.md#apiKey)

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **204** | Deleted |  -  |
| **401** | &#x60;unauthorized&#x60;: no credentials. &#x60;invalid_api_key&#x60;: the API key doesn&#39;t exist, was revoked or has expired. &#x60;invalid_token&#x60;: the token&#39;s signature is invalid, it has expired, or the resource it&#39;s scoped to was deleted |  -  |
| **402** | &#x60;plan_limit_exceeded&#x60;: the organization stayed over its plan&#39;s limits after the grace period, its API is blocked until it upgrades. &#x60;plan_limit_reached&#x60;: creating the resource would go over the plan&#39;s limit |  -  |
| **403** | &#x60;token_not_allowed&#x60;: the endpoint doesn&#39;t accept tokens, or not of this type. &#x60;insufficient_scope&#x60;: the token lacks the permission. &#x60;no_active_organization&#x60; or &#x60;forbidden&#x60;: the session has no organization, or isn&#39;t a member of the one requested |  -  |
| **404** | License not found |  -  |
| **409** | &#x60;license_in_use&#x60;: the license is used on active machines |  -  |
| **422** | &#x60;validation_error&#x60;: invalid path, query or body, with the &#x60;issues&#x60; |  -  |
| **429** | &#x60;rate_limited&#x60;: the API key made more than 10 requests in the last second. Wait for the &#x60;Retry-After&#x60; seconds |  -  |

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

<a id="getlicense"></a>
# **GetLicense**
> License GetLicense (string id)

Get a license

**Token access**: customer, license, machine tokens with the `license:read` permission (or the matching write one). A token reaches the license it's scoped to, the licenses of its customer, or the license of its machine.

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
    public class GetLicenseExample
    {
        public static void Main()
        {
            Configuration config = new Configuration();
            config.BasePath = "https://api.licensemanager.dev";
            // Configure API key authorization: apiKey
            config.AddApiKey("x-api-key", "YOUR_API_KEY");
            // Uncomment below to setup prefix (e.g. Bearer) for API key, if needed
            // config.AddApiKeyPrefix("x-api-key", "Bearer");
            // Configure Bearer token for authorization: token
            config.AccessToken = "YOUR_BEARER_TOKEN";

            // create instances of HttpClient, HttpClientHandler to be reused later with different Api classes
            HttpClient httpClient = new HttpClient();
            HttpClientHandler httpClientHandler = new HttpClientHandler();
            var apiInstance = new LicensesApi(httpClient, config, httpClientHandler);
            var id = l3Nv8KwB;  // string | 

            try
            {
                // Get a license
                License result = apiInstance.GetLicense(id);
                Debug.WriteLine(result);
            }
            catch (ApiException  e)
            {
                Debug.Print("Exception when calling LicensesApi.GetLicense: " + e.Message);
                Debug.Print("Status Code: " + e.ErrorCode);
                Debug.Print(e.StackTrace);
            }
        }
    }
}
```

#### Using the GetLicenseWithHttpInfo variant
This returns an ApiResponse object which contains the response data, status code and headers.

```csharp
try
{
    // Get a license
    ApiResponse<License> response = apiInstance.GetLicenseWithHttpInfo(id);
    Debug.Write("Status Code: " + response.StatusCode);
    Debug.Write("Response Headers: " + response.Headers);
    Debug.Write("Response Body: " + response.Data);
}
catch (ApiException e)
{
    Debug.Print("Exception when calling LicensesApi.GetLicenseWithHttpInfo: " + e.Message);
    Debug.Print("Status Code: " + e.ErrorCode);
    Debug.Print(e.StackTrace);
}
```

### Parameters

| Name | Type | Description | Notes |
|------|------|-------------|-------|
| **id** | **string** |  |  |

### Return type

[**License**](License.md)

### Authorization

[apiKey](../README.md#apiKey), [token](../README.md#token)

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **200** | License |  -  |
| **401** | &#x60;unauthorized&#x60;: no credentials. &#x60;invalid_api_key&#x60;: the API key doesn&#39;t exist, was revoked or has expired. &#x60;invalid_token&#x60;: the token&#39;s signature is invalid, it has expired, or the resource it&#39;s scoped to was deleted |  -  |
| **402** | &#x60;plan_limit_exceeded&#x60;: the organization stayed over its plan&#39;s limits after the grace period, its API is blocked until it upgrades. &#x60;plan_limit_reached&#x60;: creating the resource would go over the plan&#39;s limit |  -  |
| **403** | &#x60;token_not_allowed&#x60;: the endpoint doesn&#39;t accept tokens, or not of this type. &#x60;insufficient_scope&#x60;: the token lacks the permission. &#x60;no_active_organization&#x60; or &#x60;forbidden&#x60;: the session has no organization, or isn&#39;t a member of the one requested |  -  |
| **404** | License not found |  -  |
| **422** | &#x60;validation_error&#x60;: invalid path, query or body, with the &#x60;issues&#x60; |  -  |
| **429** | &#x60;rate_limited&#x60;: the API key made more than 10 requests in the last second. Wait for the &#x60;Retry-After&#x60; seconds |  -  |

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

<a id="getlicensestats"></a>
# **GetLicenseStats**
> LicenseStats GetLicenseStats (string id)

Get the stats of a license

Daily number of successful activations of the license over the last 90 days, today included, per machine and per version of the application. Days are in UTC.

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
    public class GetLicenseStatsExample
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
            var apiInstance = new LicensesApi(httpClient, config, httpClientHandler);
            var id = l3Nv8KwB;  // string | 

            try
            {
                // Get the stats of a license
                LicenseStats result = apiInstance.GetLicenseStats(id);
                Debug.WriteLine(result);
            }
            catch (ApiException  e)
            {
                Debug.Print("Exception when calling LicensesApi.GetLicenseStats: " + e.Message);
                Debug.Print("Status Code: " + e.ErrorCode);
                Debug.Print(e.StackTrace);
            }
        }
    }
}
```

#### Using the GetLicenseStatsWithHttpInfo variant
This returns an ApiResponse object which contains the response data, status code and headers.

```csharp
try
{
    // Get the stats of a license
    ApiResponse<LicenseStats> response = apiInstance.GetLicenseStatsWithHttpInfo(id);
    Debug.Write("Status Code: " + response.StatusCode);
    Debug.Write("Response Headers: " + response.Headers);
    Debug.Write("Response Body: " + response.Data);
}
catch (ApiException e)
{
    Debug.Print("Exception when calling LicensesApi.GetLicenseStatsWithHttpInfo: " + e.Message);
    Debug.Print("Status Code: " + e.ErrorCode);
    Debug.Print(e.StackTrace);
}
```

### Parameters

| Name | Type | Description | Notes |
|------|------|-------------|-------|
| **id** | **string** |  |  |

### Return type

[**LicenseStats**](LicenseStats.md)

### Authorization

[apiKey](../README.md#apiKey)

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **200** | Stats of the license |  -  |
| **401** | &#x60;unauthorized&#x60;: no credentials. &#x60;invalid_api_key&#x60;: the API key doesn&#39;t exist, was revoked or has expired. &#x60;invalid_token&#x60;: the token&#39;s signature is invalid, it has expired, or the resource it&#39;s scoped to was deleted |  -  |
| **402** | &#x60;plan_limit_exceeded&#x60;: the organization stayed over its plan&#39;s limits after the grace period, its API is blocked until it upgrades. &#x60;plan_limit_reached&#x60;: creating the resource would go over the plan&#39;s limit |  -  |
| **403** | &#x60;token_not_allowed&#x60;: the endpoint doesn&#39;t accept tokens, or not of this type. &#x60;insufficient_scope&#x60;: the token lacks the permission. &#x60;no_active_organization&#x60; or &#x60;forbidden&#x60;: the session has no organization, or isn&#39;t a member of the one requested |  -  |
| **404** | License not found |  -  |
| **422** | &#x60;validation_error&#x60;: invalid path, query or body, with the &#x60;issues&#x60; |  -  |
| **429** | &#x60;rate_limited&#x60;: the API key made more than 10 requests in the last second. Wait for the &#x60;Retry-After&#x60; seconds |  -  |

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

<a id="getsigningkey"></a>
# **GetSigningKey**
> SigningKey GetSigningKey ()

Get the organization's signing key

Public key verifying the license tokens returned by `validateKey`, to embed in applications. Created the first time it's needed, and never rotated. The organization has a single key, signing the tokens of its live and test products alike: check the tokens' `aud` to tell them apart.

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
    public class GetSigningKeyExample
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
            var apiInstance = new LicensesApi(httpClient, config, httpClientHandler);

            try
            {
                // Get the organization's signing key
                SigningKey result = apiInstance.GetSigningKey();
                Debug.WriteLine(result);
            }
            catch (ApiException  e)
            {
                Debug.Print("Exception when calling LicensesApi.GetSigningKey: " + e.Message);
                Debug.Print("Status Code: " + e.ErrorCode);
                Debug.Print(e.StackTrace);
            }
        }
    }
}
```

#### Using the GetSigningKeyWithHttpInfo variant
This returns an ApiResponse object which contains the response data, status code and headers.

```csharp
try
{
    // Get the organization's signing key
    ApiResponse<SigningKey> response = apiInstance.GetSigningKeyWithHttpInfo();
    Debug.Write("Status Code: " + response.StatusCode);
    Debug.Write("Response Headers: " + response.Headers);
    Debug.Write("Response Body: " + response.Data);
}
catch (ApiException e)
{
    Debug.Print("Exception when calling LicensesApi.GetSigningKeyWithHttpInfo: " + e.Message);
    Debug.Print("Status Code: " + e.ErrorCode);
    Debug.Print(e.StackTrace);
}
```

### Parameters
This endpoint does not need any parameter.
### Return type

[**SigningKey**](SigningKey.md)

### Authorization

[apiKey](../README.md#apiKey)

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **200** | Signing key |  -  |
| **401** | &#x60;unauthorized&#x60;: no credentials. &#x60;invalid_api_key&#x60;: the API key doesn&#39;t exist, was revoked or has expired. &#x60;invalid_token&#x60;: the token&#39;s signature is invalid, it has expired, or the resource it&#39;s scoped to was deleted |  -  |
| **402** | &#x60;plan_limit_exceeded&#x60;: the organization stayed over its plan&#39;s limits after the grace period, its API is blocked until it upgrades. &#x60;plan_limit_reached&#x60;: creating the resource would go over the plan&#39;s limit |  -  |
| **403** | &#x60;token_not_allowed&#x60;: the endpoint doesn&#39;t accept tokens, or not of this type. &#x60;insufficient_scope&#x60;: the token lacks the permission. &#x60;no_active_organization&#x60; or &#x60;forbidden&#x60;: the session has no organization, or isn&#39;t a member of the one requested |  -  |
| **422** | &#x60;validation_error&#x60;: invalid path, query or body, with the &#x60;issues&#x60; |  -  |
| **429** | &#x60;rate_limited&#x60;: the API key made more than 10 requests in the last second. Wait for the &#x60;Retry-After&#x60; seconds |  -  |

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

<a id="listcustomerlicenses"></a>
# **ListCustomerLicenses**
> LicenseList ListCustomerLicenses (string customerId, int? page = null, int? pageSize = null, string sort = null, string search = null, string key = null, string policyId = null, string machineVersion = null, LicenseStatus? status = null, DateTime? createdFrom = null, DateTime? createdTo = null, DateTime? lastActivatedFrom = null, DateTime? lastActivatedTo = null, string neverActivated = null, DateTime? expiresFrom = null, DateTime? expiresTo = null, string neverExpires = null, string currency = null, decimal? price = null, decimal? priceMin = null, decimal? priceMax = null, string hasPrice = null)

List the licenses of a customer

Sorting by `lastActivatedAt` puts the licenses never activated last in both orders. Sorting by `price` compares the amounts whatever their currency, and puts the licenses without a price last in both orders.  **Token access**: customer tokens with the `license:read` permission (or the matching write one). A customer token reaches its own licenses.

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
    public class ListCustomerLicensesExample
    {
        public static void Main()
        {
            Configuration config = new Configuration();
            config.BasePath = "https://api.licensemanager.dev";
            // Configure API key authorization: apiKey
            config.AddApiKey("x-api-key", "YOUR_API_KEY");
            // Uncomment below to setup prefix (e.g. Bearer) for API key, if needed
            // config.AddApiKeyPrefix("x-api-key", "Bearer");
            // Configure Bearer token for authorization: token
            config.AccessToken = "YOUR_BEARER_TOKEN";

            // create instances of HttpClient, HttpClientHandler to be reused later with different Api classes
            HttpClient httpClient = new HttpClient();
            HttpClientHandler httpClientHandler = new HttpClientHandler();
            var apiInstance = new LicensesApi(httpClient, config, httpClientHandler);
            var customerId = c9Wd3RtE;  // string | 
            var page = 1;  // int? | Page to return. Pages are numbered from 1: `1` is the first page. A page past the last one returns an empty `data`, not an error. Defaults to `1`. (optional)  (default to 1)
            var pageSize = 20;  // int? | Maximum number of items per page, from 1 to 100. Every page holds this many items except the last one, which can hold fewer. Defaults to `20`. (optional)  (default to 20)
            var sort = -createdAt;  // string | Field to sort by, prefixed with `-` for descending order. Defaults to `-createdAt`. (optional)  (default to -createdAt)
            var search = X9ZPA;  // string | Case-insensitive text the key contains. (optional) 
            var key = 7KQ2M-X9ZPA-H4TRC-WN6EY-B3JDF;  // string | Only returns the license with this exact key, case included. Keys of test products start with `TEST-`. (optional) 
            var policyId = p4Rt8LmQ;  // string | Only returns the licenses following this policy. (optional) 
            var machineVersion = 2.3.1;  // string | Only returns the licenses with at least one active machine running this version of the product. (optional) 
            var status = (LicenseStatus) "active";  // LicenseStatus? | Only returns the licenses with this status. (optional) 
            var createdFrom = 2026-01-01T00:00:00.000Z;  // DateTime? | Only returns the licenses created at or after this date. (optional) 
            var createdTo = 2026-02-01T00:00:00.000Z;  // DateTime? | Only returns the licenses created at or before this date. (optional) 
            var lastActivatedFrom = 2026-01-01T00:00:00.000Z;  // DateTime? | Only returns the licenses last activated at or after this date. Licenses never activated are left out. (optional) 
            var lastActivatedTo = 2026-02-01T00:00:00.000Z;  // DateTime? | Only returns the licenses last activated at or before this date. Licenses never activated are left out. (optional) 
            var neverActivated = true;  // string | `true` only returns the licenses never activated, `false` only the ones activated at least once. (optional) 
            var expiresFrom = 2026-01-01T00:00:00.000Z;  // DateTime? | Only returns the licenses expiring at or after this date. Licenses that never expire are left out. (optional) 
            var expiresTo = 2026-02-01T00:00:00.000Z;  // DateTime? | Only returns the licenses expiring at or before this date. Licenses that never expire are left out. (optional) 
            var neverExpires = true;  // string | `true` only returns the licenses that never expire, `false` only the ones with an expiration date. (optional) 
            var currency = USD;  // string | Only returns the licenses paid in this currency. (optional) 
            var price = 49.99;  // decimal? | Only returns the licenses paid exactly this amount, in major units of its currency: combine with `currency` to compare amounts of one currency. Licenses without a price are left out. (optional) 
            var priceMin = 49.99;  // decimal? | Only returns the licenses paid at least this amount, in major units of its currency: combine with `currency` to compare amounts of one currency. Licenses without a price are left out. (optional) 
            var priceMax = 49.99;  // decimal? | Only returns the licenses paid at most this amount, in major units of its currency: combine with `currency` to compare amounts of one currency. Licenses without a price are left out. (optional) 
            var hasPrice = true;  // string | `true` only returns the licenses with a price, `false` only the ones without. (optional) 

            try
            {
                // List the licenses of a customer
                LicenseList result = apiInstance.ListCustomerLicenses(customerId, page, pageSize, sort, search, key, policyId, machineVersion, status, createdFrom, createdTo, lastActivatedFrom, lastActivatedTo, neverActivated, expiresFrom, expiresTo, neverExpires, currency, price, priceMin, priceMax, hasPrice);
                Debug.WriteLine(result);
            }
            catch (ApiException  e)
            {
                Debug.Print("Exception when calling LicensesApi.ListCustomerLicenses: " + e.Message);
                Debug.Print("Status Code: " + e.ErrorCode);
                Debug.Print(e.StackTrace);
            }
        }
    }
}
```

#### Using the ListCustomerLicensesWithHttpInfo variant
This returns an ApiResponse object which contains the response data, status code and headers.

```csharp
try
{
    // List the licenses of a customer
    ApiResponse<LicenseList> response = apiInstance.ListCustomerLicensesWithHttpInfo(customerId, page, pageSize, sort, search, key, policyId, machineVersion, status, createdFrom, createdTo, lastActivatedFrom, lastActivatedTo, neverActivated, expiresFrom, expiresTo, neverExpires, currency, price, priceMin, priceMax, hasPrice);
    Debug.Write("Status Code: " + response.StatusCode);
    Debug.Write("Response Headers: " + response.Headers);
    Debug.Write("Response Body: " + response.Data);
}
catch (ApiException e)
{
    Debug.Print("Exception when calling LicensesApi.ListCustomerLicensesWithHttpInfo: " + e.Message);
    Debug.Print("Status Code: " + e.ErrorCode);
    Debug.Print(e.StackTrace);
}
```

### Parameters

| Name | Type | Description | Notes |
|------|------|-------------|-------|
| **customerId** | **string** |  |  |
| **page** | **int?** | Page to return. Pages are numbered from 1: &#x60;1&#x60; is the first page. A page past the last one returns an empty &#x60;data&#x60;, not an error. Defaults to &#x60;1&#x60;. | [optional] [default to 1] |
| **pageSize** | **int?** | Maximum number of items per page, from 1 to 100. Every page holds this many items except the last one, which can hold fewer. Defaults to &#x60;20&#x60;. | [optional] [default to 20] |
| **sort** | **string** | Field to sort by, prefixed with &#x60;-&#x60; for descending order. Defaults to &#x60;-createdAt&#x60;. | [optional] [default to -createdAt] |
| **search** | **string** | Case-insensitive text the key contains. | [optional]  |
| **key** | **string** | Only returns the license with this exact key, case included. Keys of test products start with &#x60;TEST-&#x60;. | [optional]  |
| **policyId** | **string** | Only returns the licenses following this policy. | [optional]  |
| **machineVersion** | **string** | Only returns the licenses with at least one active machine running this version of the product. | [optional]  |
| **status** | **LicenseStatus?** | Only returns the licenses with this status. | [optional]  |
| **createdFrom** | **DateTime?** | Only returns the licenses created at or after this date. | [optional]  |
| **createdTo** | **DateTime?** | Only returns the licenses created at or before this date. | [optional]  |
| **lastActivatedFrom** | **DateTime?** | Only returns the licenses last activated at or after this date. Licenses never activated are left out. | [optional]  |
| **lastActivatedTo** | **DateTime?** | Only returns the licenses last activated at or before this date. Licenses never activated are left out. | [optional]  |
| **neverActivated** | **string** | &#x60;true&#x60; only returns the licenses never activated, &#x60;false&#x60; only the ones activated at least once. | [optional]  |
| **expiresFrom** | **DateTime?** | Only returns the licenses expiring at or after this date. Licenses that never expire are left out. | [optional]  |
| **expiresTo** | **DateTime?** | Only returns the licenses expiring at or before this date. Licenses that never expire are left out. | [optional]  |
| **neverExpires** | **string** | &#x60;true&#x60; only returns the licenses that never expire, &#x60;false&#x60; only the ones with an expiration date. | [optional]  |
| **currency** | **string** | Only returns the licenses paid in this currency. | [optional]  |
| **price** | **decimal?** | Only returns the licenses paid exactly this amount, in major units of its currency: combine with &#x60;currency&#x60; to compare amounts of one currency. Licenses without a price are left out. | [optional]  |
| **priceMin** | **decimal?** | Only returns the licenses paid at least this amount, in major units of its currency: combine with &#x60;currency&#x60; to compare amounts of one currency. Licenses without a price are left out. | [optional]  |
| **priceMax** | **decimal?** | Only returns the licenses paid at most this amount, in major units of its currency: combine with &#x60;currency&#x60; to compare amounts of one currency. Licenses without a price are left out. | [optional]  |
| **hasPrice** | **string** | &#x60;true&#x60; only returns the licenses with a price, &#x60;false&#x60; only the ones without. | [optional]  |

### Return type

[**LicenseList**](LicenseList.md)

### Authorization

[apiKey](../README.md#apiKey), [token](../README.md#token)

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **200** | One page of the licenses of the customer |  -  |
| **401** | &#x60;unauthorized&#x60;: no credentials. &#x60;invalid_api_key&#x60;: the API key doesn&#39;t exist, was revoked or has expired. &#x60;invalid_token&#x60;: the token&#39;s signature is invalid, it has expired, or the resource it&#39;s scoped to was deleted |  -  |
| **402** | &#x60;plan_limit_exceeded&#x60;: the organization stayed over its plan&#39;s limits after the grace period, its API is blocked until it upgrades. &#x60;plan_limit_reached&#x60;: creating the resource would go over the plan&#39;s limit |  -  |
| **403** | &#x60;token_not_allowed&#x60;: the endpoint doesn&#39;t accept tokens, or not of this type. &#x60;insufficient_scope&#x60;: the token lacks the permission. &#x60;no_active_organization&#x60; or &#x60;forbidden&#x60;: the session has no organization, or isn&#39;t a member of the one requested |  -  |
| **404** | Customer not found |  -  |
| **422** | &#x60;validation_error&#x60;: invalid path, query or body, with the &#x60;issues&#x60; |  -  |
| **429** | &#x60;rate_limited&#x60;: the API key made more than 10 requests in the last second. Wait for the &#x60;Retry-After&#x60; seconds |  -  |

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

<a id="listlicenses"></a>
# **ListLicenses**
> LicenseList ListLicenses (string productId, int? page = null, int? pageSize = null, string sort = null, string search = null, string key = null, string policyId = null, string customerId = null, string machineVersion = null, LicenseStatus? status = null, DateTime? createdFrom = null, DateTime? createdTo = null, DateTime? lastActivatedFrom = null, DateTime? lastActivatedTo = null, string neverActivated = null, DateTime? expiresFrom = null, DateTime? expiresTo = null, string neverExpires = null, string currency = null, decimal? price = null, decimal? priceMin = null, decimal? priceMax = null, string hasPrice = null)

List the licenses of a product

Sorting by `lastActivatedAt` puts the licenses never activated last in both orders. Sorting by `price` compares the amounts whatever their currency, and puts the licenses without a price last in both orders.

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
    public class ListLicensesExample
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
            var apiInstance = new LicensesApi(httpClient, config, httpClientHandler);
            var productId = x7Kp2QaZ;  // string | 
            var page = 1;  // int? | Page to return. Pages are numbered from 1: `1` is the first page. A page past the last one returns an empty `data`, not an error. Defaults to `1`. (optional)  (default to 1)
            var pageSize = 20;  // int? | Maximum number of items per page, from 1 to 100. Every page holds this many items except the last one, which can hold fewer. Defaults to `20`. (optional)  (default to 20)
            var sort = -createdAt;  // string | Field to sort by, prefixed with `-` for descending order. Defaults to `-createdAt`. (optional)  (default to -createdAt)
            var search = X9ZPA;  // string | Case-insensitive text the key contains. (optional) 
            var key = 7KQ2M-X9ZPA-H4TRC-WN6EY-B3JDF;  // string | Only returns the license with this exact key, case included. Keys of test products start with `TEST-`. (optional) 
            var policyId = p4Rt8LmQ;  // string | Only returns the licenses following this policy. (optional) 
            var customerId = c9Wd3RtE;  // string | Only returns the licenses of this customer. (optional) 
            var machineVersion = 2.3.1;  // string | Only returns the licenses with at least one active machine running this version of the product. (optional) 
            var status = (LicenseStatus) "active";  // LicenseStatus? | Only returns the licenses with this status. (optional) 
            var createdFrom = 2026-01-01T00:00:00.000Z;  // DateTime? | Only returns the licenses created at or after this date. (optional) 
            var createdTo = 2026-02-01T00:00:00.000Z;  // DateTime? | Only returns the licenses created at or before this date. (optional) 
            var lastActivatedFrom = 2026-01-01T00:00:00.000Z;  // DateTime? | Only returns the licenses last activated at or after this date. Licenses never activated are left out. (optional) 
            var lastActivatedTo = 2026-02-01T00:00:00.000Z;  // DateTime? | Only returns the licenses last activated at or before this date. Licenses never activated are left out. (optional) 
            var neverActivated = true;  // string | `true` only returns the licenses never activated, `false` only the ones activated at least once. (optional) 
            var expiresFrom = 2026-01-01T00:00:00.000Z;  // DateTime? | Only returns the licenses expiring at or after this date. Licenses that never expire are left out. (optional) 
            var expiresTo = 2026-02-01T00:00:00.000Z;  // DateTime? | Only returns the licenses expiring at or before this date. Licenses that never expire are left out. (optional) 
            var neverExpires = true;  // string | `true` only returns the licenses that never expire, `false` only the ones with an expiration date. (optional) 
            var currency = USD;  // string | Only returns the licenses paid in this currency. (optional) 
            var price = 49.99;  // decimal? | Only returns the licenses paid exactly this amount, in major units of its currency: combine with `currency` to compare amounts of one currency. Licenses without a price are left out. (optional) 
            var priceMin = 49.99;  // decimal? | Only returns the licenses paid at least this amount, in major units of its currency: combine with `currency` to compare amounts of one currency. Licenses without a price are left out. (optional) 
            var priceMax = 49.99;  // decimal? | Only returns the licenses paid at most this amount, in major units of its currency: combine with `currency` to compare amounts of one currency. Licenses without a price are left out. (optional) 
            var hasPrice = true;  // string | `true` only returns the licenses with a price, `false` only the ones without. (optional) 

            try
            {
                // List the licenses of a product
                LicenseList result = apiInstance.ListLicenses(productId, page, pageSize, sort, search, key, policyId, customerId, machineVersion, status, createdFrom, createdTo, lastActivatedFrom, lastActivatedTo, neverActivated, expiresFrom, expiresTo, neverExpires, currency, price, priceMin, priceMax, hasPrice);
                Debug.WriteLine(result);
            }
            catch (ApiException  e)
            {
                Debug.Print("Exception when calling LicensesApi.ListLicenses: " + e.Message);
                Debug.Print("Status Code: " + e.ErrorCode);
                Debug.Print(e.StackTrace);
            }
        }
    }
}
```

#### Using the ListLicensesWithHttpInfo variant
This returns an ApiResponse object which contains the response data, status code and headers.

```csharp
try
{
    // List the licenses of a product
    ApiResponse<LicenseList> response = apiInstance.ListLicensesWithHttpInfo(productId, page, pageSize, sort, search, key, policyId, customerId, machineVersion, status, createdFrom, createdTo, lastActivatedFrom, lastActivatedTo, neverActivated, expiresFrom, expiresTo, neverExpires, currency, price, priceMin, priceMax, hasPrice);
    Debug.Write("Status Code: " + response.StatusCode);
    Debug.Write("Response Headers: " + response.Headers);
    Debug.Write("Response Body: " + response.Data);
}
catch (ApiException e)
{
    Debug.Print("Exception when calling LicensesApi.ListLicensesWithHttpInfo: " + e.Message);
    Debug.Print("Status Code: " + e.ErrorCode);
    Debug.Print(e.StackTrace);
}
```

### Parameters

| Name | Type | Description | Notes |
|------|------|-------------|-------|
| **productId** | **string** |  |  |
| **page** | **int?** | Page to return. Pages are numbered from 1: &#x60;1&#x60; is the first page. A page past the last one returns an empty &#x60;data&#x60;, not an error. Defaults to &#x60;1&#x60;. | [optional] [default to 1] |
| **pageSize** | **int?** | Maximum number of items per page, from 1 to 100. Every page holds this many items except the last one, which can hold fewer. Defaults to &#x60;20&#x60;. | [optional] [default to 20] |
| **sort** | **string** | Field to sort by, prefixed with &#x60;-&#x60; for descending order. Defaults to &#x60;-createdAt&#x60;. | [optional] [default to -createdAt] |
| **search** | **string** | Case-insensitive text the key contains. | [optional]  |
| **key** | **string** | Only returns the license with this exact key, case included. Keys of test products start with &#x60;TEST-&#x60;. | [optional]  |
| **policyId** | **string** | Only returns the licenses following this policy. | [optional]  |
| **customerId** | **string** | Only returns the licenses of this customer. | [optional]  |
| **machineVersion** | **string** | Only returns the licenses with at least one active machine running this version of the product. | [optional]  |
| **status** | **LicenseStatus?** | Only returns the licenses with this status. | [optional]  |
| **createdFrom** | **DateTime?** | Only returns the licenses created at or after this date. | [optional]  |
| **createdTo** | **DateTime?** | Only returns the licenses created at or before this date. | [optional]  |
| **lastActivatedFrom** | **DateTime?** | Only returns the licenses last activated at or after this date. Licenses never activated are left out. | [optional]  |
| **lastActivatedTo** | **DateTime?** | Only returns the licenses last activated at or before this date. Licenses never activated are left out. | [optional]  |
| **neverActivated** | **string** | &#x60;true&#x60; only returns the licenses never activated, &#x60;false&#x60; only the ones activated at least once. | [optional]  |
| **expiresFrom** | **DateTime?** | Only returns the licenses expiring at or after this date. Licenses that never expire are left out. | [optional]  |
| **expiresTo** | **DateTime?** | Only returns the licenses expiring at or before this date. Licenses that never expire are left out. | [optional]  |
| **neverExpires** | **string** | &#x60;true&#x60; only returns the licenses that never expire, &#x60;false&#x60; only the ones with an expiration date. | [optional]  |
| **currency** | **string** | Only returns the licenses paid in this currency. | [optional]  |
| **price** | **decimal?** | Only returns the licenses paid exactly this amount, in major units of its currency: combine with &#x60;currency&#x60; to compare amounts of one currency. Licenses without a price are left out. | [optional]  |
| **priceMin** | **decimal?** | Only returns the licenses paid at least this amount, in major units of its currency: combine with &#x60;currency&#x60; to compare amounts of one currency. Licenses without a price are left out. | [optional]  |
| **priceMax** | **decimal?** | Only returns the licenses paid at most this amount, in major units of its currency: combine with &#x60;currency&#x60; to compare amounts of one currency. Licenses without a price are left out. | [optional]  |
| **hasPrice** | **string** | &#x60;true&#x60; only returns the licenses with a price, &#x60;false&#x60; only the ones without. | [optional]  |

### Return type

[**LicenseList**](LicenseList.md)

### Authorization

[apiKey](../README.md#apiKey)

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **200** | One page of the licenses of the product |  -  |
| **401** | &#x60;unauthorized&#x60;: no credentials. &#x60;invalid_api_key&#x60;: the API key doesn&#39;t exist, was revoked or has expired. &#x60;invalid_token&#x60;: the token&#39;s signature is invalid, it has expired, or the resource it&#39;s scoped to was deleted |  -  |
| **402** | &#x60;plan_limit_exceeded&#x60;: the organization stayed over its plan&#39;s limits after the grace period, its API is blocked until it upgrades. &#x60;plan_limit_reached&#x60;: creating the resource would go over the plan&#39;s limit |  -  |
| **403** | &#x60;token_not_allowed&#x60;: the endpoint doesn&#39;t accept tokens, or not of this type. &#x60;insufficient_scope&#x60;: the token lacks the permission. &#x60;no_active_organization&#x60; or &#x60;forbidden&#x60;: the session has no organization, or isn&#39;t a member of the one requested |  -  |
| **404** | Product not found |  -  |
| **422** | &#x60;validation_error&#x60;: invalid path, query or body, with the &#x60;issues&#x60; |  -  |
| **429** | &#x60;rate_limited&#x60;: the API key made more than 10 requests in the last second. Wait for the &#x60;Retry-After&#x60; seconds |  -  |

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

<a id="sendlicensekeys"></a>
# **SendLicenseKeys**
> void SendLicenseKeys (SendLicenseKeys sendLicenseKeys)

Email license keys to their customers

Emails each customer the keys of its licenses among `ids`, with their expiration date: one email per customer, whatever their number of licenses. The licenses can belong to different products of the organization.  Test products only email the members of the organization, so testing never emails real customers: nothing is sent when a license of a test product belongs to a customer whose email isn't a member's.  **Required role permission**: `license:send` when called with a session, granted by the member's role. API keys aren't limited by roles.

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
    public class SendLicenseKeysExample
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
            var apiInstance = new LicensesApi(httpClient, config, httpClientHandler);
            var sendLicenseKeys = new SendLicenseKeys(); // SendLicenseKeys | 

            try
            {
                // Email license keys to their customers
                apiInstance.SendLicenseKeys(sendLicenseKeys);
            }
            catch (ApiException  e)
            {
                Debug.Print("Exception when calling LicensesApi.SendLicenseKeys: " + e.Message);
                Debug.Print("Status Code: " + e.ErrorCode);
                Debug.Print(e.StackTrace);
            }
        }
    }
}
```

#### Using the SendLicenseKeysWithHttpInfo variant
This returns an ApiResponse object which contains the response data, status code and headers.

```csharp
try
{
    // Email license keys to their customers
    apiInstance.SendLicenseKeysWithHttpInfo(sendLicenseKeys);
}
catch (ApiException e)
{
    Debug.Print("Exception when calling LicensesApi.SendLicenseKeysWithHttpInfo: " + e.Message);
    Debug.Print("Status Code: " + e.ErrorCode);
    Debug.Print(e.StackTrace);
}
```

### Parameters

| Name | Type | Description | Notes |
|------|------|-------------|-------|
| **sendLicenseKeys** | [**SendLicenseKeys**](SendLicenseKeys.md) |  |  |

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
| **204** | Keys emailed |  -  |
| **401** | &#x60;unauthorized&#x60;: no credentials. &#x60;invalid_api_key&#x60;: the API key doesn&#39;t exist, was revoked or has expired. &#x60;invalid_token&#x60;: the token&#39;s signature is invalid, it has expired, or the resource it&#39;s scoped to was deleted |  -  |
| **402** | &#x60;plan_limit_exceeded&#x60;: the organization stayed over its plan&#39;s limits after the grace period, its API is blocked until it upgrades. &#x60;plan_limit_reached&#x60;: creating the resource would go over the plan&#39;s limit |  -  |
| **403** | &#x60;token_not_allowed&#x60;: the endpoint doesn&#39;t accept tokens, or not of this type. &#x60;insufficient_scope&#x60;: the token lacks the permission. &#x60;no_active_organization&#x60; or &#x60;forbidden&#x60;: the session has no organization, or isn&#39;t a member of the one requested |  -  |
| **404** | &#x60;not_found&#x60;: one of the licenses wasn&#39;t found |  -  |
| **409** | &#x60;test_recipient_not_member&#x60;: a license of a test product belongs to a customer whose email isn&#39;t a member&#39;s of the organization |  -  |
| **422** | &#x60;validation_error&#x60;: invalid path, query or body, with the &#x60;issues&#x60; |  -  |
| **429** | &#x60;rate_limited&#x60;: the API key made more than 10 requests in the last second. Wait for the &#x60;Retry-After&#x60; seconds |  -  |

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

<a id="updatelicense"></a>
# **UpdateLicense**
> License UpdateLicense (string id, UpdateLicense updateLicense)

Update a license

The key, policy and customer of a license can't be changed: sending them does nothing.  The changes apply to the next validations of the key, not to the license tokens `validateKey` already returned, which stay valid until they expire. Lowering `maxMachines` doesn't deactivate machines: the ones already active keep validating, and new ones replace them one at a time when the product has `autoMachineChange`, or are refused until enough are deactivated.  **Required role permission**: `license:update` when called with a session, granted by the member's role. API keys aren't limited by roles.

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
    public class UpdateLicenseExample
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
            var apiInstance = new LicensesApi(httpClient, config, httpClientHandler);
            var id = l3Nv8KwB;  // string | 
            var updateLicense = new UpdateLicense(); // UpdateLicense | 

            try
            {
                // Update a license
                License result = apiInstance.UpdateLicense(id, updateLicense);
                Debug.WriteLine(result);
            }
            catch (ApiException  e)
            {
                Debug.Print("Exception when calling LicensesApi.UpdateLicense: " + e.Message);
                Debug.Print("Status Code: " + e.ErrorCode);
                Debug.Print(e.StackTrace);
            }
        }
    }
}
```

#### Using the UpdateLicenseWithHttpInfo variant
This returns an ApiResponse object which contains the response data, status code and headers.

```csharp
try
{
    // Update a license
    ApiResponse<License> response = apiInstance.UpdateLicenseWithHttpInfo(id, updateLicense);
    Debug.Write("Status Code: " + response.StatusCode);
    Debug.Write("Response Headers: " + response.Headers);
    Debug.Write("Response Body: " + response.Data);
}
catch (ApiException e)
{
    Debug.Print("Exception when calling LicensesApi.UpdateLicenseWithHttpInfo: " + e.Message);
    Debug.Print("Status Code: " + e.ErrorCode);
    Debug.Print(e.StackTrace);
}
```

### Parameters

| Name | Type | Description | Notes |
|------|------|-------------|-------|
| **id** | **string** |  |  |
| **updateLicense** | [**UpdateLicense**](UpdateLicense.md) |  |  |

### Return type

[**License**](License.md)

### Authorization

[apiKey](../README.md#apiKey)

### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: application/json


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **200** | Updated license |  -  |
| **401** | &#x60;unauthorized&#x60;: no credentials. &#x60;invalid_api_key&#x60;: the API key doesn&#39;t exist, was revoked or has expired. &#x60;invalid_token&#x60;: the token&#39;s signature is invalid, it has expired, or the resource it&#39;s scoped to was deleted |  -  |
| **402** | &#x60;plan_limit_exceeded&#x60;: the organization stayed over its plan&#39;s limits after the grace period, its API is blocked until it upgrades. &#x60;plan_limit_reached&#x60;: creating the resource would go over the plan&#39;s limit |  -  |
| **403** | &#x60;token_not_allowed&#x60;: the endpoint doesn&#39;t accept tokens, or not of this type. &#x60;insufficient_scope&#x60;: the token lacks the permission. &#x60;no_active_organization&#x60; or &#x60;forbidden&#x60;: the session has no organization, or isn&#39;t a member of the one requested |  -  |
| **404** | License not found |  -  |
| **422** | &#x60;validation_error&#x60;: invalid path, query or body, with the &#x60;issues&#x60; |  -  |
| **429** | &#x60;rate_limited&#x60;: the API key made more than 10 requests in the last second. Wait for the &#x60;Retry-After&#x60; seconds |  -  |

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

<a id="validatekey"></a>
# **ValidateKey**
> LicenseToken ValidateKey (string productId, ValidateKey validateKey)

Validate a license key

Checks the license key of the product on a machine and returns a token the application can verify offline with the organization's public key. Doesn't need authentication.  The license must allow the `version`: up to its `maxVersion.version` when it has one, like `\"2.3\"` for every 2.3.z version and older. Its `maxVersion.lockMajorAt` and `maxVersion.lockMinorAt` are enforced once they hard-code `maxVersion.version`, within the hour they're reached. When it doesn't, the error's `latestAllowedVersion` is the latest release of the product the license allows, so the application can offer to install it.  The machine with the `fingerprint` is created when the license has none, and activated when it's deactivated, unless the license is already active on its maximum number of machines. A machine that's already active is never refused for the maximum number of machines, even when it was lowered below the number of active machines. Its `version`, and its `name` and `platform` when given, are updated: they can't be cleared.  Unless the product disables `autoMachineChange`, a new machine isn't refused when the license is on its maximum number of machines: it takes the place of the active machine validated the longest ago, which is deactivated with its `overriddenByMachineId` set to the new machine, and recorded as a `machine.deactivated` event. When a machine deactivated this way is validated again, it takes its place back: the machine that overrode it, and the ones that overrode that one in turn, are locked, with their `overriddenByMachineId` set to the machine coming back. A locked machine is always refused, so two machines can't take turns on one place.  The checks run in this order, and the first one failing answers: the license has expired or was canceled, then it doesn't allow the version, then the machine is locked, then it's on its maximum number of machines. Each failure is recorded as a `license.validation_failed` event, except for keys that don't exist.  Changes to the license, like deactivating the machine or shortening its expiration, don't revoke the tokens already returned: the application only sees them when it validates its key again, at the latest when its token expires.

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
    public class ValidateKeyExample
    {
        public static void Main()
        {
            Configuration config = new Configuration();
            config.BasePath = "https://api.licensemanager.dev";
            // create instances of HttpClient, HttpClientHandler to be reused later with different Api classes
            HttpClient httpClient = new HttpClient();
            HttpClientHandler httpClientHandler = new HttpClientHandler();
            var apiInstance = new LicensesApi(httpClient, config, httpClientHandler);
            var productId = x7Kp2QaZ;  // string | 
            var validateKey = new ValidateKey(); // ValidateKey | 

            try
            {
                // Validate a license key
                LicenseToken result = apiInstance.ValidateKey(productId, validateKey);
                Debug.WriteLine(result);
            }
            catch (ApiException  e)
            {
                Debug.Print("Exception when calling LicensesApi.ValidateKey: " + e.Message);
                Debug.Print("Status Code: " + e.ErrorCode);
                Debug.Print(e.StackTrace);
            }
        }
    }
}
```

#### Using the ValidateKeyWithHttpInfo variant
This returns an ApiResponse object which contains the response data, status code and headers.

```csharp
try
{
    // Validate a license key
    ApiResponse<LicenseToken> response = apiInstance.ValidateKeyWithHttpInfo(productId, validateKey);
    Debug.Write("Status Code: " + response.StatusCode);
    Debug.Write("Response Headers: " + response.Headers);
    Debug.Write("Response Body: " + response.Data);
}
catch (ApiException e)
{
    Debug.Print("Exception when calling LicensesApi.ValidateKeyWithHttpInfo: " + e.Message);
    Debug.Print("Status Code: " + e.ErrorCode);
    Debug.Print(e.StackTrace);
}
```

### Parameters

| Name | Type | Description | Notes |
|------|------|-------------|-------|
| **productId** | **string** |  |  |
| **validateKey** | [**ValidateKey**](ValidateKey.md) |  |  |

### Return type

[**LicenseToken**](LicenseToken.md)

### Authorization

No authorization required

### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: application/json


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **200** | Signed license token |  -  |
| **402** | &#x60;plan_limit_exceeded&#x60;: the organization stayed over its plan&#39;s limits after the grace period |  -  |
| **403** | &#x60;license_expired&#x60;: the license has expired, or was canceled. &#x60;version_not_allowed&#x60;: the license doesn&#39;t allow the version, with the &#x60;latestAllowedVersion&#x60;. &#x60;machine_locked&#x60;: the machine was locked after the machine it overrode came back. &#x60;machine_limit_reached&#x60;: the license is already active on its maximum number of machines, and the product disables &#x60;autoMachineChange&#x60; or the machine isn&#39;t new |  -  |
| **404** | &#x60;not_found&#x60;: the product doesn&#39;t exist, or has no license with this key |  -  |
| **422** | &#x60;validation_error&#x60;: invalid body |  -  |

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

