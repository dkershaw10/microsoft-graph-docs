---
description: "Automatically generated file. DO NOT MODIFY"
---

```csharp

GraphServiceClient graphClient = new GraphServiceClient( authProvider );

var identityProvider = await graphClient.IdentityProviders["{id}"]
	.Request()
	.GetAsync();

```