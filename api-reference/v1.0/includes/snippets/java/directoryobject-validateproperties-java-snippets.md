---
description: "Automatically generated file. DO NOT MODIFY"
---

```java

IGraphServiceClient graphClient = GraphServiceClient.builder().authenticationProvider( authProvider ).buildClient();

String entityType = "Group";

String displayName = "Myprefix_test_mysuffix";

String mailNickname = "Myprefix_test_mysuffix";

UUID onBehalfOfUserId = UUID.fromString("onBehalfOfUserId-value");

graphClient.directoryObjects()
	.validateProperties(entityType,displayName,mailNickname,onBehalfOfUserId)
	.buildRequest()
	.post();

```