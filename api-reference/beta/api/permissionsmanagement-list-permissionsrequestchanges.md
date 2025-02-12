---
title: "List permissionsRequestChanges"
description: "List the permissionsRequestChange objects and their properties."
author: "mrudulahg01"
ms.localizationpriority: medium
ms.prod: "multicloud-permissions-management"
doc_type: apiPageType
---

# List permissionsRequestChanges
Namespace: microsoft.graph

[!INCLUDE [beta-disclaimer](../../includes/beta-disclaimer.md)]

List the [permissionsRequestChange](../resources/permissionsrequestchange.md) objects and their properties.

## Permissions
One of the following permissions is required to call this API. To learn more, including how to choose permissions, see [Permissions](/graph/permissions-reference).

|Permission type|Permissions (from least to most privileged)|
|:---|:---|
|Delegated (work or school account)|Not supported.|
|Delegated (personal Microsoft account)|Not supported.|
|Application|Not supported.|

<!--
[!INCLUDE [epm-rbac-servicenow-apis-read](../includes/rbac-for-apis/epm-rbac-servicenow-apis-read.md)]
-->

## HTTP request

<!-- {
  "blockType": "ignored"
}
-->
``` http
GET /identityGovernance/permissionsManagement/permissionsRequestChanges
```

## Optional query parameters
This method supports the `$filter`, `$top`, and `$orderBy` OData query parameters to help customize the response. For general information, see [OData query parameters](/graph/query-parameters).

## Request headers
|Name|Description|
|:---|:---|
|Authorization|Bearer {token}. Required.|

## Request body
Don't supply a request body for this method.

## Response

If successful, this method returns a `200 OK` response code and a collection of [permissionsRequestChange](../resources/permissionsrequestchange.md) objects in the response body.

## Examples

#### Request
The following example shows a request to retrieve a changelog of a scheduled permissions requests at time `t`.
<!-- {
  "blockType": "request",
  "name": "list_permissionsrequestchange"
}
-->
``` http
GET https://graph.microsoft.com/beta/identityGovernance/permissionsManagement/permissionsRequestChanges?$filter=modificationDateTime gt {t}
```


#### Response
The following example shows the response.
>**Note:** The response object shown here might be shortened for readability.
<!-- {
  "blockType": "response",
  "truncated": true,
  "@odata.type": "Collection(microsoft.graph.permissionsRequestChange)"
}
-->
``` http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "@odata.context": "https://graph.microsoft.com/beta/$metadata#permissionsRequestChanges",
  "value": [
    {
      "id": "00000000-0000-0000-0000-000000000001",
      "modificationDateTime": "2023-02-06T12:15:00Z",
      "statusDetail": "submitted",
      "ticketId": "INC1234567",
      "permissionsRequestId": "00000000-0000-0000-0000-000000000001"
    },
    {
      "id": "00000000-0000-0000-0000-000000000002",
      "modificationDateTime": "2023-02-08T12:15:00Z",
      "statusDetail": "submitted",
      "ticketId": "INC1234567",
      "permissionsRequestId": "00000000-0000-0000-0000-000000000002"
    },
    {
      "id": "00000000-0000-0000-0000-000000000003",
      "modificationDateTime": "2023-02-010T12:15:00Z",
      "statusDetail": "approved",
      "activeOccurenceStatus": "granting",
      "ticketId": "INC1234567",
      "permissionsRequestId": "00000000-0000-0000-0000-000000000001"
    },
  ],
  "@odata.nextLink": "https://graph.microsoft.com/beta/identityGovernance/permissionsManagement/permissionsRequestChanges?$filter=modificationDateTime gt {t}&$skiptoken=Mg"
}
```

