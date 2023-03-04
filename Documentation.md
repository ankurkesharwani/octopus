## Objects

These are used internally to represent the requests and their mock responses.

### Project
| Field | Type | Optional | Description |
|--|--| -- | -- |
| id | UUID4 |✘|
| name | String |✘|
| templatesRelativePath | String |✘ | A relative path where project specific templates will be found. |

#### Example
```
{
    "id": "UUID-4",
    "name": "Instagram Clone",
    "templatesRelativePath": "/templates/insta-clone"
}
```

### RequestTemplate

| Field | Type | Optional | Description |
|--|--| -- | -- |
| id | `UUID4` |✘|
|pathTemplate| `String` | ✘ ||
|method | `String` | ✘ | Possible values are GET, POST, PUT, DELETE.
|pathParams | `Array<KeyValuePair>` | ✔ | The value is expected to be a regex. | 
|queryParams | `Array<KeyValuePair>` | ✔ | The value is expected to be a regex. |
|headers | `Array<KeyValuePair>` | ✔ | The value is expected to be a regex. |
|body | `BodyTemplate` | ✔ | |

### BodyTemplate

| Field | Type | Optional | Description |
|--|--| -- | -- |
| type | `Enum` |✘| Possible values are `JSON`, `PainText`, `XML`.
|hash| `Base64 String` |✘| |

### KeyValuePair
| Field | Type | Optional | Description |
|--|--| -- | -- |
|key|`String`|✘| |
|value|`String`|✘| |

#### Example 
```
{
    "id": "UUID-4",
    "pathTemplate": "api/v1/users/:userId/posts/:postId/comments",
    "method": "GET/POST/PUT/DELETE",
    "pathParams": [
      {
        "key": "userId",
        "value": "UUID-4"
      },
      {
        "key": "postId",
        "value": "^.+$"
      }
    ],
    "queryParams": [
      {
        "key": "limit",
        "value": "^[0-9]+$"
      },
      {
        "key": "offset",
        "value": "^[0-9]+$"
      }
    ],
    "headers": [
      {
        "key": "Authorization",
        "value": "^.+$"
      },
      {
        "key": "X-DeviceId",
        "value": "^.+$"
      }
    ],
    "body": {
      "type": "JSON/PlainText/XML/BINARY",
      "hash": "Base 64 encoded hash"
    }
}
```

### ResponseTemplate

| Field | Type | Optional | Description |
|--|--| -- | -- |
|id|`UUID4`|✘| |
|requestTemplateId|`UUID4`|✘| |
|statusCode| `Int`|✘ ||
|latency|`Int`|✔| Default will be considered 0.|
|headers| `Array<KeyValuePair>`|✔|
|body|`ResponseBodyTemplate`| ✔ |

### ResponseBodyTemplate
| Field | Type | Optional | Description |
|--|--| -- | -- |
|responseBodyFilePath|`String`|✘| |
|type|`Enum`|✘| Possible values are `JSON`, `PlainText`, `Binary`|

#### Example
```
{
    "id": "UUID-4",
    "requestTemplateId": "UUID-4",
    "statusCode": 200,
    "latency": 2000,
    "headers": [
      {
        "key": "Authorization",
        "value": "UUID-4"
      }
    ],
    "body": {
      "responseBodyFilePath": "some/relative/path/to/file.json",
      "type": "JSON"
    }
}
```
