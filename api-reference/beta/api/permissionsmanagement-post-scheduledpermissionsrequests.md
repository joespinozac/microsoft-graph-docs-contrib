---
title: "Create scheduledPermissionsRequest"
description: "Create a new scheduledPermissionsRequest object."
author: "mrudulahg01"
ms.localizationpriority: medium
ms.prod: "multicloud-permissions-management"
doc_type: apiPageType
---

# Create scheduledPermissionsRequest
Namespace: microsoft.graph

[!INCLUDE [beta-disclaimer](../../includes/beta-disclaimer.md)]

Create a new [scheduledPermissionsRequest](../resources/scheduledpermissionsrequest.md) object.

## Permissions
One of the following permissions is required to call this API. To learn more, including how to choose permissions, see [Permissions](/graph/permissions-reference).

|Permission type|Permissions (from least to most privileged)|
|:---|:---|
|Delegated (work or school account)|Not supported.|
|Delegated (personal Microsoft account)|Not supported.|
|Application|Not supported.|

<!--
[!INCLUDE [epm-rbac-servicenow-apis-write](../includes/rbac-for-apis/epm-rbac-servicenow-apis-write.md)]
-->

## HTTP request

<!-- {
  "blockType": "ignored"
}
-->
``` http
POST /identityGovernance/permissionsManagement/scheduledPermissionsRequests
```

## Request headers
|Name|Description|
|:---|:---|
|Authorization|Bearer {token}. Required.|
|Content-Type|application/json. Required.|

## Request body
In the request body, supply a JSON representation of the [scheduledPermissionsRequest](../resources/scheduledpermissionsrequest.md) object.

You can specify the following properties when creating a **scheduledPermissionsRequest**.

|Property|Type|Description|
|:---|:---|:---|
|requestedPermissions|[permissionsDefinition](../resources/permissionsdefinition.md)|Defines the permission request itself. Required. <br/> You must specify the **@odata.type** property with the value of the **permissionDefinition** object type in the request body. For example `"@odata.type": "#microsoft.graph.awsPermissionsDefinition"`. |
|notes|String|Additional notes to add to the request. Optional.|
|justification|String|Request justification. Optional.|
|createdDateTime|DateTimeOffset|Time when the scheduledPermissionsRequest was created. Required.|
|scheduleInfo|[requestSchedule](../resources/requestschedule.md)|Schedule to assign the requestedPermissions. Optional.|
|ticketInfo|[ticketInfo](../resources/ticketinfo.md)|Represents ticketing related metadata that can be used to correlate to the request. Optional.|
|statusDetail|statusDetail|The current status of the request. The possible values are: `submitted`, `approved`, `completed`, `canceled`, `rejected`, `unknownFutureValue`. Required.|



## Response

If successful, this method returns a `201 Created` response code and a [scheduledPermissionsRequest](../resources/scheduledpermissionsrequest.md) object in the response body.

## Examples

### Example 1: AWS policy request

#### Request
The following example shows a request.
<!-- {
  "blockType": "request",
  "name": "create_scheduledpermissionsrequest_aws_policy"
}
-->
``` http
POST https://graph.microsoft.com/beta/identityGovernance/permissionsManagement/scheduledPermissionsRequests
Content-Type: application/json

{
  "requestedPermissions": {
    "@odata.type": "#microsoft.graph.awsPermissionsDefinition",
    "authorizationSystemInfo": {
      "authorizationSystemId": "956987887735",
      "authorizationSystemType": "AWS"
    },
    "actionInfo": {
      "@odata.type": "microsoft.graph.awsPolicyPermissionsDefinitionAction",
      "policies": [
        {
          "id": "arn:aws:iam::956987887735:policy/AddUserToGroup"
        }
      ],
      "assignToRoleId": "arn:aws:aim::956987887735:role/saml-user"
    },
    "identityInfo": {
      "externalId": "alex@contoso.com",
      "source": {
        "@odata.type": "microsoft.graph.samlIdentitySource"
      },
      "identityType": "user"
    }
  },
  "justification": "I need to do this because I want to add a user to a group",
  "notes": "Pretty Please",
  "scheduleInfo": {
    "expiration": {
      "duration": "PT1H"
    }
  },
  "ticketInfo": {
    "ticketNumber": "INC1234567",
    "ticketSystem": "ServiceNow",
    "ticketSubmitterIdentityId": "alex@contoso.com",
    "ticketApproverIdentityId": "alexmanager@contoso.com"
  }
}
```


#### Response
The following example shows the response.
>**Note:** The response object shown here might be shortened for readability.
<!-- {
  "blockType": "response",
  "truncated": true,
  "@odata.type": "microsoft.graph.scheduledPermissionsRequest"
}
-->
``` http
HTTP/1.1 201 Created
Content-Type: application/json

{
  "@odata.type": "microsoft.graph.scheduledPermissionsRequest",
  "id": "00000000-0000-0000-0000-000000000002",
  "requestedPermissions": {
    "@odata.type": "microsoft.graph.awsPermissionsDefinition",
    "authorizationSystemInfo": {
      "authorizationSystemId": "956987887735",
      "authorizationSystemType": "AWS",
    },
    "actionInfo": {
      "@odata.type": "microsoft.graph.awsPolicyPermissionsDefinitionAction",
      "policies": [
        {
          "id": "arn:aws:iam::956987887735:policy/AddUserToGroup"
        }
      ],
      "assignToRoleId": "arn:aws:aim::956987887735:role/saml-user"
    },
    "identityInfo": {
      "externalId": "alex@contoso.com",
      "source": {
        "@odata.type": "microsoft.graph.samlIdentitySource"
      },
      "identityType": "user"
    }
 },
 "justification": "I need to do this because I want to add a user to a group",
 "notes": "Pretty Please",
 "createdDateTime": "2023-02-06T12:15:00Z",
 "scheduleInfo": {
    "expiration": {
      "duration": "PT1H"
    },
 },
 "ticketInfo": {
    "ticketNumber": "INC1234567",
    "ticketSystem": "ServiceNow",
    "ticketSubmitterIdentityId": "alex@contoso.com",
    "ticketApproverIdentityId": "alexmanager@contoso.com"
 },
 "statusDetail": "submitted"
}
```

### Example 2: Azure roles request

#### Request
The following example shows a request.
<!-- {
  "blockType": "request",
  "name": "create_scheduledpermissionsrequest_azure_roles"
}
-->
``` http
POST https://graph.microsoft.com/beta/identityGovernance/permissionsManagement/scheduledPermissionsRequests
Content-Type: application/json

{
  "requestedPermissions": {
    "@odata.type": "microsoft.graph.singleResourceAzurePermissionsDefinition",
    "authorizationSystemInfo": {
      "authorizationSystemId": "87eefd90-95a3-480a-ba42-56ff299a05ee",
      "authorizationSystemType": "AZURE"
    },
    "actionInfo": {
      "@odata.type": "microsoft.graph.azureRolePermissionsDefinitionAction",
      "roles": [
        {
          "id": "cdda3590-29a3-44f6-95f2-9f980659eb04"
        },
        {
          "id": "312a565d-c81f-4fd8-895a-4e21e48d571c"
        }
      ]
    },
    "identityInfo": {
      "externalId": "alex@contoso.com",
      "source": {
        "@odata.type": "microsoft.graph.edIdentitySource"
      },
      "identityType": "user"
    },
    "resourceId": "/subscriptions/87eefd90-95a3-480a-ba42-56ff299a05ee"
  },
  "justification": "I need to do this because I want to some new azure roles",
  "notes": "Pretty Pleaseeeee",
  "scheduleInfo": {
    "expiration": {
      "duration": "PT1H"
    },
    "recurrence": null
  },
  "ticketInfo": {
    "ticketNumber": "INC1234567",
    "ticketSystem": "ServiceNow",
    "ticketSubmitterIdentityId": "alex@contoso.com",
    "ticketApproverIdentityId": "alexmanager@contoso.com"
  }
}
```


#### Response
The following example shows the response.
>**Note:** The response object shown here might be shortened for readability.
<!-- {
  "blockType": "response",
  "truncated": true,
  "@odata.type": "microsoft.graph.scheduledPermissionsRequest"
}
-->
``` http
HTTP/1.1 201 Created
Content-Type: application/json

{
  "@odata.type": "microsoft.graph.scheduledPermissionsRequest",
  "id": "00000000-0000-0000-0000-000000000004",
   "requestedPermissions": {
    "@odata.type": "microsoft.graph.singleResourceAzurePermissionsDefinition",
    "authorizationSystemInfo": {
      "authorizationSystemId": "87eefd90-95a3-480a-ba42-56ff299a05ee",
      "authorizationSystemType": "AZURE",
    },
    "actionInfo" : {
      "@odata.type": "microsoft.graph.azureRolePermissionsDefinitionAction",
      "roles": [
        {
          "id": "cdda3590-29a3-44f6-95f2-9f980659eb04"
        },
        {
          "id": "312a565d-c81f-4fd8-895a-4e21e48d571c"
        }
      ]
    },
    "identityInfo": {
      "externalId": "alex@contoso.com",
      "source": {
        "@odata.type": "microsoft.graph.edIdentitySource"
      },
      "identityType": "user"
    },
    "resourceId": "/subscriptions/87eefd90-95a3-480a-ba42-56ff299a05ee"
  },
  "justification": "I need to do this because I want to some new azure roles",
  "notes": "Pretty Pleaseeeee",
  "createdDateTime": "2023-02-06T12:15:00Z",
  "scheduleInfo": {
    "expiration": {
      "duration": "PT1H"
    },
  },
  "ticketInfo": {
    "ticketNumber": "INC1234567",
    "ticketSystem": "ServiceNow",
    "ticketSubmitterIdentityId": "alex@contoso.com",
    "ticketApproverIdentityId": "alexmanager@contoso.com"
  },
  "statusDetail": "submitted"
}
```

### Example 3: GCP actions request

#### Request
The following example shows a request.
<!-- {
  "blockType": "request",
  "name": "create_scheduledpermissionsrequest_from_gcp_actions"
}
-->
``` http
POST https://graph.microsoft.com/beta/identityGovernance/permissionsManagement/scheduledPermissionsRequests
Content-Type: application/json

{
  "requestedPermissions": {
    "@odata.type": "microsoft.graph.singleResourceGcpPermissionsDefinition",
    "authorizationSystemInfo": {
      "authorizationSystemId": "carbide-bonsai-205017",
      "authorizationSystemType": "GCP"
    },
    "actionInfo": {
      "@odata.type": "microsoft.graph.gcpActionPermissionsDefinitionAction",
      "actions": [
        "aiplatform:dataitems"
      ]
    },
    "identityInfo": {
      "externalId": "alex@contoso.com",
      "source": {
        "@odata.type": "microsoft.graph.edIdentitySource"
      },
      "identityType": "user"
    },
    "resourceId": "carbide-bonsai-205017"
  },
  "justification": "I need to do this because I want to code my own chat GPT-3 bot on GCP",
  "notes": "Pretty Pleaseeeee",
  "scheduleInfo": {
    "expiration": {
      "duration": "PT1H"
    }
  },
  "ticketInfo": {
    "ticketNumber": "INC1234567",
    "ticketSystem": "ServiceNow",
    "ticketSubmitterIdentityId": "alex@contoso.com",
    "ticketApproverIdentityId": "alexmanager@contoso.com"
  }
}
```


#### Response
The following example shows the response.
>**Note:** The response object shown here might be shortened for readability.
<!-- {
  "blockType": "response",
  "truncated": true,
  "@odata.type": "microsoft.graph.scheduledPermissionsRequest"
}
-->
``` http
HTTP/1.1 201 Created
Content-Type: application/json

{
  "@odata.type": "microsoft.graph.scheduledPermissionsRequest",
  "id": "00000000-0000-0000-0000-000000000005",
   "requestedPermissions": {
    "@odata.type": "microsoft.graph.singleResourceGcpPermissionsDefinition",
    "authorizationSystemInfo": {
      "authorizationSystemId": "carbide-bonsai-205017",
      "authorizationSystemType": "GCP",
    },
    "actionInfo" : {
      "@odata.type": "microsoft.graph.gcpActionPermissionsDefinitionAction",
      "actions": [
        "aiplatform:dataitems"
      ]
    },
    "identityInfo": {
      "externalId": "alex@contoso.com",
      "source": {
        "@odata.type": "microsoft.graph.edIdentitySource"
      },
      "identityType": "user"
    },
    "resourceId": "carbide-bonsai-205017"
  },
  "justification": "I need to do this because I want to code my own chat GPT-3 bot on GCP",
  "notes": "Pretty Pleaseeeee",
  "createdDateTime": "2023-02-06T12:15:00Z",
  "scheduleInfo": {
    "expiration": {
      "duration": "PT1H"
    }
  },
  "ticketInfo": {
    "ticketNumber": "INC1234567",
    "ticketSystem": "ServiceNow",
    "ticketSubmitterIdentityId": "alex@contoso.com",
    "ticketApproverIdentityId": "alexmanager@contoso.com"
  },
  "statusDetail": "submitted"
}
```

