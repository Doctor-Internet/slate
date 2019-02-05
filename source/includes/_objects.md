# Response Objects

As of API version v2, API response objects have been standardized, and the response objects are documented here.

## API Response Object

> JSON Schema:

```json
{
	"$schema": "http://json-schema.org/draft-07/schema#",
	"$id": "https://joshpiper.github.io/slate/api-response.schema.json",
	"title": "API Response Object",
	"description": "The base object returned by any query.",
	"type": "object",
	"properties": {
		"status": {
			"description": "Representation of the status of the request.",
			"type": "string",
			"enum": ["success", "error"]
		},
		"message": {
			"description": "Message provided by the request.",
			"type": "string"
		},
		"data": {
			"description": "Any data returned by the request, such as a created object for POST.",
			"type": ["boolean", "object", "array", "number", "string"]
		}
	},
	"required": ["status"]
}
```

This object is used as the base of all v2+ API responses. Any further response data or resources are returned in the data section.

## Array

A collection of multiple returned resources.

> Array Schema

```json
{
	"$schema": "http://json-schema.org/draft-07/schema#",
	"$id": "https://joshpiper.github.io/slate/array.schema.json",
	"title": "Array",
	"description": "An array with multiple sets of contained data.",
	"type": "array",
	"items": {
		"type": ["boolean", "object", "array", "number", "string"]
	}
}
```

## API Data Object

The API data object is returned when providing a generic query against the root endpoint.

> API Data

```json
{
	"$schema": "http://json-schema.org/draft-07/schema#",
	"$id": "https://joshpiper.github.io/slate/apidata.schema.json",
	"title": "API Data",
	"description": "An object which contains data about the API itself.",
	"type": "object",
	"properties": {
		"name": {
			"description": "The name of the API service.",
			"type": "string"
		},
		"description": {
			"description": "The API description.",
			"type": "string"
		},
		"endpoints": {
			"description": "Array of endpoints and help messages.",
			"type": "array",
			"items": {
				"type": "string"
			}
		}
	},
	"required": ["steamid", "name"]
}
```

## Player Objects

Player objects may vary with extra data depending on the endpoint. However, all of these base themselves off a base player object.

### Base Player Object

The base player object is the minimum amount of data used to describe a player in a way which allows getting extra data from other endpoints.

> Base Schema:

```json
{
	"$schema": "http://json-schema.org/draft-07/schema#",
	"$id": "https://joshpiper.github.io/slate/base-player.schema.json",
	"title": "Base Player Object",
	"description": "The base player object.",
	"type": "object",
	"properties": {
		"steamid": {
			"description": "The user's 64bit SteamID.",
			"type": "string",
			"regex": "\\d{17}"
		},
		"name": {
			"description": "User's Steam Name. This is mutatable and should not be used as a user key.",
			"type": "string"
		}
	},
	"required": ["steamid", "name"]
}
```

### Clan Member

The clan member object is returned from clan APIs, and has additional information to represent users within the clan.

> Clan Schema:

```json
{
	"$schema": "http://json-schema.org/draft-07/schema#",
	"$id": "https://joshpiper.github.io/slate/clan-player.schema.json",
	"title": "Clan Player Object",
	"description": "The player object returned by Clan APIs.",
	"type": "object",
	"allOf": [{"$ref": "https://joshpiper.github.io/slate/base-player.schema.json"}],
	"properties": {
		"rankid": {
			"description": "ID which represents the player's rank within the clan.",
			"type": "integer"
		},
		"icname": {
			"description": "User's RP name.",
			"type": "string"
		}
	},
	"required": ["steamid", "name", "rankid", "icname"]
}
```

## Changelog

These objects are emitted by the changelog APIs.

> Changelog Schema:

```json
{
	"$schema": "http://json-schema.org/draft-07/schema#",
	"$id": "https://joshpiper.github.io/slate/changelog.schema.json",
	"title": "Changelog",
	"description": "The representation of a public commit.",
	"type": "object",
	"properties": {
		"revision": {
			"description": "Internal revision ID.",
			"type": ["string", "number"]
		},
		"commit": {
			"description": "Commit message.",
			"type": "string"
		},
		"author": {
			"description": "Internal author-string.",
			"type": "string"
		},
		"time": {
			"description": "RFC 3339 encoded timestamp.",
			"type": "string",
			"regex": "(\\d+)-(0[1-9]|1[012])-(0[1-9]|[12]\\d|3[01])[Tt]([01]\\d|2[0-3]):([0-5]\\d):([0-5]\\d|60)(\\.\\d+)?(([Zz])|([\\+|\\-]([01]\\d|2[0-3]):[0-5]\\d))"
		}
	},
	"required": ["revision", "commit", "author", "time"]
}
```

## Clan Rank

These objects are both emitted when getting clan ranks, and also when requesting clan objects with rank relations.

### Rank Permissions

Rank permission objects are used to represent different rank permission structures.

> Permission Schema:

```json
{
	"$schema": "http://json-schema.org/draft-07/schema#",
	"$id": "https://joshpiper.github.io/slate/rank-permissions.schema.json",
	"title": "Clan Rank Permissions",
	"description": "The representation of a clan rank's permissions.",
	"type": "object",
	"properties": {
		"invite": {
			"description": "If the rank can invite users to the clan, represented as a 1 bit integer.",
			"type": "integer"
		},
		"kick": {
			"description": "If the rank can kick users from the clan, represented as a 1 bit integer.",
			"type": "integer"
		},
		"setrank": {
			"description": "The ID of the highest rank which this rank can set. 0 if none.",
			"type": "integer"
		},
		"forum": {
			"description": "If the rank has access to clan forums.",
			"type": "integer"
		},
		"motd": {
			"description": "If the rank has access to edit the motd / motto.",
			"type": "integer"
		}
	},
	"required": ["invite", "kick", "setrank", "forum", "motd"]
}
```

### Clan Rank

The clan rank object describes a single rank within the clan structure and can optionally contain rank permission as described above.

> Rank Schema:

```json
{
	"$schema": "http://json-schema.org/draft-07/schema#",
	"$id": "https://joshpiper.github.io/slate/rank.schema.json",
	"title": "Changelog",
	"description": "The representation of a clan rank.",
	"type": "object",
	"properties": {
		"id": {
			"description": "Internal rank ID representation.",
			"type": "integer"
		},
		"name": {
			"description": "The name of the rank.",
			"type": "string"
		},
		"perms": {
			"description": "The rank permissions.",
			"$ref": "https://joshpiper.github.io/slate/base-player.schema.json"
		}
	},
	"required": ["id", "name"]
}
```

## Clan

The clan object contains all data required for the identification of a clan.

```json
{
	"$schema": "http://json-schema.org/draft-07/schema#",
	"$id": "https://joshpiper.github.io/slate/clan.schema.json",
	"title": "Changelog",
	"description": "The representation of a clan.",
	"type": "object",
	"properties": {
		"id": {
			"description": "Internal clan ID representation.",
			"type": "integer"
		},
		"name": {
			"description": "The name of the clan.",
			"type": "string"
		},
		"ranks": {
			"description": "The rank permissions.",
			"type": "array",
			"items": "https://joshpiper.github.io/slate/rank.schema.json"
		},
		"members": {
			"description": "The members.",
			"type": "array",
			"items": "https://joshpiper.github.io/slate/clan-player.schema.json"
		}
	},
	"required": ["id", "name"]
}
```

## Self Data

This data is only used by the /me endpoint to identify the user that owns this key.

```json
{
	"$schema": "http://json-schema.org/draft-07/schema#",
	"$id": "https://joshpiper.github.io/slate/me.schema.json",
	"title": "Self",
	"description": "Data about a user key.",
	"type": "object",
	"properties": {
		"auth_method": {
			"description": "The method used to authenticate.",
			"type": "string",
			"enum": ["Anonymous", "Basic", "Bearer"]
		},
		"steamid": {
			"description": "User's 64 bit steamid.",
			"type": "integer"
		},
		"steamid32": {
			"description": "User's 32 bit steamid.",
			"type": "string",
			"regex": "^STEAM_[0-5]:[01]:\\d+$"
		},
		"forumid": {
			"description": "The attached forumid.",
			"type": "integer"
		},
		"permissions": {
			"description": "The permissions attached to an API key.",
			"type": "integer",
			"minimum": "-1"
		}
	},
	"required": ["auth_method"]
}
```

## API Key

This is data returned by API key endpoints.

```json
{
	"$schema": "http://json-schema.org/draft-07/schema#",
	"$id": "https://joshpiper.github.io/slate/key.schema.json",
	"title": "API Key",
	"description": "API key data.",
	"type": "object",
	"properties": {
		"api_key": {
			"description": "The representation of the API key.",
			"type": "string"
		},
		"steamid": {
			"description": "The 64 bit steamid .",
			"type": "integer"
		},
		"permissions": {
			"description": "The permissions attached to an API key.",
			"type": "integer",
			"minimum": "-1"
		}
	},
	"required": ["api_key", "steamid", "permissions"]
}
```

## Post Object

This is data returned by any endpoint handling posts.

```json
{
	"$schema": "http://json-schema.org/draft-07/schema#",
	"$id": "https://joshpiper.github.io/slate/post.schema.json",
	"title": "Post",
	"description": "Forum post.",
	"type": "object",
	"properties": {
		"pid": {
			"description": "The ID of the post.",
			"type": "number"
		},
		"subject": {
			"description": "The title of the thread.",
			"type": "string"
		},
		"message": {
			"description": "The opening post.",
			"type": "string"
		},
		"uid": {
			"description": "The userID of the user who made the thread.",
			"type": "numer"
		},
		"type": {
			"description": "The type of post.",
			"type": "string"
		}
	},
	"required": ["pid", "subject", "message", "uid"]
}
```