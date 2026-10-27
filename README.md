# LicenseManager C# SDK

[![NuGet version](https://img.shields.io/nuget/v/LicenseMan.Sdk)](https://www.nuget.org/packages/LicenseMan.Sdk)
[![NuGet downloads](https://img.shields.io/nuget/dt/LicenseMan.Sdk)](https://www.nuget.org/packages/LicenseMan.Sdk)
[![Publish](https://github.com/licenseman/licensemanager-dotnet/actions/workflows/publish.yml/badge.svg)](https://github.com/licenseman/licensemanager-dotnet/actions/workflows/publish.yml)
[![License](https://img.shields.io/github/license/licenseman/licensemanager-dotnet)](https://github.com/licenseman/licensemanager-dotnet/blob/main/LICENSE)
[![Documentation](https://img.shields.io/badge/docs-licensemanager.dev-blue)](https://licensemanager.dev/docs/sdks/csharp)

The official C# SDK for the [LicenseManager](https://licensemanager.dev) API: issue, manage and validate software licenses. Async client built on `HttpClient`, for .NET 8 or later, and .NET Standard 2.0 (.NET Framework 4.6.1 or later).

**[Documentation](https://licensemanager.dev/docs/sdks/csharp)** · **[API reference](https://api.licensemanager.dev/docs)** · **[Changelog](CHANGELOG.md)**

## Requirements

.NET 8 or later, or any platform implementing .NET Standard 2.0.

## Installation

```sh
dotnet add package LicenseMan.Sdk
```

## Usage

Create an API key in the LicenseManager app, then create a license after a sale:

```csharp
using LicenseManager.Api;
using LicenseManager.Client;
using LicenseManager.Model;

var configuration = new Configuration();
configuration.AddApiKey("x-api-key", Environment.GetEnvironmentVariable("LICENSEMANAGER_API_KEY"));
var licenses = new LicensesApi(configuration);

var license = await licenses.CreateLicenseAsync(
    "x7Kp2QaZ",
    new CreateLicense(email: "jane@example.com")
);
```

And validate it from your application, which needs no API key:

```csharp
using LicenseManager.Api;
using LicenseManager.Model;

var licenses = new LicensesApi();

var licenseToken = await licenses.ValidateKeyAsync(
    "x7Kp2QaZ",
    new ValidateKey(
        key: "7KQ2M-X9ZPA-H4TRC-WN6EY-B3JDF",
        fingerprint: "4c:32:75:8f:9a:1e",
        varVersion: "1.4.2"
    )
);
```

## Authentication

Most endpoints take an organization API key: keep it on your servers. The endpoints your application calls directly, like validating a key, take no credentials or a token scoped to a customer, license or machine. See [authentication](https://licensemanager.dev/docs/api/authentication) and [scoped tokens](https://licensemanager.dev/docs/api/scoped-tokens).

```csharp
using LicenseManager.Client;

var configuration = new Configuration();
// With an API key, from your backend:
configuration.AddApiKey("x-api-key", Environment.GetEnvironmentVariable("LICENSEMANAGER_API_KEY"));
// Or with a token scoped to a customer, license or machine:
configuration.AccessToken = token;
```

## Errors

Failed requests answer an error with a stable `code` to branch on, listed for each endpoint in the [API reference](https://api.licensemanager.dev/docs). See [errors](https://licensemanager.dev/docs/api/errors).

```csharp
using LicenseManager.Client;

try
{
    await licenses.GetLicenseAsync("l3Nv8KwB");
}
catch (ApiException error)
{
    // The body is { "error": { "code", "message" } }.
    Console.Error.WriteLine($"{error.ErrorCode} {error.ErrorContent}");
}
```

## Reference

Every method is documented, with its parameters and responses, in the [`docs`](docs) folder:

| Class | Methods |
| --- | --- |
| [`LicensesApi`](docs/LicensesApi.md) | `ValidateKeyAsync`, `ListLicensesAsync`, `CreateLicenseAsync`, `ListCustomerLicensesAsync`, `GetLicenseAsync`, `DeleteLicenseAsync`, `UpdateLicenseAsync`, `GetLicenseStatsAsync`, `CancelLicenseAsync`, `SendLicenseKeysAsync`, `GetSigningKeyAsync` |
| [`PortalApi`](docs/PortalApi.md) | `GetPortalAsync`, `RequestPortalLinkAsync`, `CreatePortalLinkAsync`, `SendPortalLinkAsync` |
| [`ProductsApi`](docs/ProductsApi.md) | `ListProductsAsync`, `CreateProductAsync`, `GetProductAsync`, `DeleteProductAsync`, `UpdateProductAsync`, `ResetProductAsync`, `UploadProductLogoAsync`, `DeleteProductLogoAsync`, `GetProductStatsAsync` |
| [`PoliciesApi`](docs/PoliciesApi.md) | `ListPoliciesAsync`, `CreatePolicyAsync`, `GetPolicyAsync`, `DeletePolicyAsync`, `UpdatePolicyAsync` |
| [`CustomersApi`](docs/CustomersApi.md) | `ListCustomersAsync`, `CreateCustomerAsync`, `GetCustomerAsync`, `DeleteCustomerAsync`, `UpdateCustomerAsync` |
| [`MachinesApi`](docs/MachinesApi.md) | `ListMachinesAsync`, `GetMachineAsync`, `DeactivateMachineAsync` |
| [`ReleasesApi`](docs/ReleasesApi.md) | `ListReleasesAsync`, `CreateReleaseAsync`, `GetReleaseAsync`, `DeleteReleaseAsync`, `UpdateReleaseAsync` |
| [`TokensApi`](docs/TokensApi.md) | `CreateCustomerTokenAsync`, `CreateLicenseTokenAsync`, `CreateMachineTokenAsync` |
| [`EventsApi`](docs/EventsApi.md) | `ListPolicyEventsAsync`, `ListLicenseEventsAsync` |
| [`IntegrationsApi`](docs/IntegrationsApi.md) | `GetStripeIntegrationAsync`, `ConnectStripeAsync`, `DisconnectIntegrationAsync`, `UpdateIntegrationAsync`, `CheckIntegrationAsync`, `ListStripePricesAsync`, `CreateStripeMappingAsync`, `DeleteStripeMappingAsync`, `UpdateStripeMappingAsync` |

## Versioning

This SDK follows [semantic versioning](https://semver.org) and is generated from the [OpenAPI document](openapi.json) of the API: each release is listed in the [changelog](CHANGELOG.md). Please don't open pull requests, they would be overwritten by the next release: [open an issue](https://github.com/licenseman/licensemanager-dotnet/issues) instead.

## License

See [LICENSE](LICENSE).
