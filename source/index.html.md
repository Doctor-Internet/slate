---
title: API Reference

language_tabs:
 - shell

toc_footers:
  - <a href='https://limelightgaming.net/forums/thread-24089.html'>Release Thread</a>
  - <a href='https://github.com/lord/slate'>Documentation Powered by Slate</a>

includes:
  - v1
  - objects
  - v2
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

```bash
curl "endpoint"
  -H "Authorization: Bearer $my_api_key"
```

Key generation endpoints also support Basic authentication using your Limelight Forum account details.

> Basic auth is also supported.

```bash
define -r my_basic_key=$(echo "$user":"$pass" | base64 --encode)
curl "endpoint"
  -H "Authorization: Basic $my_basic_key"
```

Currently API keys can only be generated programmatically using basic auth via key generation endpoints. As this can be done via browser, we highly recommend manually generating these keys, and using them for your applications.

We only require API keys for secured endpoints.

# Versioning

API version are differentiated by an optional version identifier between the host and endpoint sections of the URL.

> This points at the default API root.

```bash
curl "https://api.limelightgaming.net/"
```

> This points at the development API root.

```bash
curl "https://api.limelightgaming.net/dev/"
```

> This points at the v2 API root.

```bash
curl "https://api.limelightgaming.net/v2/"
```

API Version | Status
--- | ---
dev | Development, Unstable
v1 | Default, Stable, Legacy
v2 | Development, Stable

# Resource Relationships

Some endpoints which have related data, such as clans and their members, can be retrieved in a single API call, using the with parameter.

For example, the /clans/:id endpoint allows with settings to retrieve ranks without using the /clans/:id/ranks endpoint, by using /clans/:id/?with=ranks.

These are simple comma separated values, added to the with parameter.

# Passing Data

Data can be passed to POST/PUT/PATCH commands in various ways.

Standard form encoding (application/x-www-form-urlencoded and multipart/form-data) work, as well as json input (application/json).

Ensure that for all requests, an appropriate Content-Type header is sent.