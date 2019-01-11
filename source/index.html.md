---
title: API Reference

language_tabs:
 - shell

toc_footers:
  - <a href='https://limelightgaming.net/forums/thread-24089.html'>Release Thread</a>
  - <a href='https://github.com/lord/slate'>Documentation Powered by Slate</a>

includes:
  - v1
  - codes
  - contrib

search: true
---

# Introduction

Welcome to the Limelight API documentation.
Our API can be used to access various endpoints, for information about our players and services.

We currently have no language bindings, however you can view example shell scripts, which you can then use for your own bindings.

# Authentication

> To authorize, we accept API keys as bearer tokens in Authorization headers.

```shell
curl "endpoint"
  -H "Authorization: Bearer my_api_key"
```

Key generation endpoints also support Basic authentication using your Limelight Forum account details.

> Basic auth is also supported.

```shell
curl "endpoint"
  -H "Authorization: Basic basic_auth"
```

Currently API keys can only be generated programatically using basic auth via key generation endpoints. As this can be done via browser, we highly recommend manually generating these keys, and using them for your applications.

We only require API keys for secured endpoints.

# Versioning

API version are differentated by an optional version identifier between the host and endpoint sections of the URL.

> This points at the default API root.

```shell
curl "https://api.limelightgaming.net/"
```

> This points at the development API root.

```shell
curl "https://api.limelightgaming.net/dev/"
```

> This points at the v2 API root.

```shell
curl "https://api.limelightgaming.net/v2/"
```

API Version | Status
--- | ---
dev | Development, Unstable
v1 | Default, Stable, Legacy
v2 | Development, Stable

# Resource Relationships

Some endpoints which have related data, such as clans and their members, can be retrieved in a single API call, using the with parameter.

For example, the /clans/{id} endpoint allows with settings to retrieve ranks without using the /clans/{id}/ranks endpoint, by using /clans/{id}/?with=ranks.

These are simple comma seperated values, added to the with parameter.
