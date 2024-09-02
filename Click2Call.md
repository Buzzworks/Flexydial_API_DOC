# Click to Call API

### `POST /api/click-to-call/`

#### Parameters

Content- type: ‘application/json’

```json
{
  "customer_number": "Customer Number",
  "agent_number": "Agent Number"
}
```

**AUTHORIZATION**:

[Click here for authentication API Doc](https://github.com/Buzzworks/Flexydial_API_DOC/blob/main/Authentication.md)

**API Key:** tokenAuth

Token-based authentication with required prefix "**Token**"

**Header Parameter Name:** Authorization



### Responses

### Success

##### Code `200`

##### Description

```json
{
    "token": "Call initiated successfully"
}
```

### Error

##### Code `500`

##### Description

```json
{
    "error": "Failed to initiate call"
}
```
