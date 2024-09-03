# 1. DNC Upload and Update API

### Introduction
The DNC (Do Not Call) Management API is designed to facilitate the management of DNC numbers through various endpoints. It allows users to upload new DNC numbers and remove existing ones efficiently. This document outlines the functionality, workflows, and requirements for using the API effectively.

### `POST /api/upload-dnc/`

```json
[
    {
        "numeric": "6300868437",
        "campaign": "",
        "global_dnc": "true",
        "status": "Inactive"
    },
    {
        "numeric": "6300868438",
        "campaign": "Campaign1",
        "global_dnc": "false",
        "status": "Active"
    }
]
```
**AUTHORIZATION**:

[Click here for authentication API Doc](https://github.com/Buzzworks/Flexydial_API_DOC/blob/main/Authentication.md)

**API Key:** tokenAuth

Token-based authentication with required prefix "**Token**"

**Header Parameter Name:** Authorization

### Responses

### Success

##### Description

```json
{
    "detail": "Data processed successfully"
}
```
### Error
```json
{
    "detail": "DNC number 6300868437 already exists."
}
```

# 2. Removing DNC Numbers

### `POST /api/remove-dnc/`

```json
[
    {
        "numeric": "6300868437"
    },
    {
        "numeric": "6300868438"
    }
]
```
### Success

##### Description

```json
{
    "detail": "DNC numbers removed successfully"
}
```
### Error
```json
{
    "detail": "DNC number 6300868437 does not exist."
}
```