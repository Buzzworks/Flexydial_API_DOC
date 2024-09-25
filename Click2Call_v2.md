# Click to Call API

### `POST /api/click-to-call/`

#### Parameters

Content- type: ‘application/json’

```json
{
        "agent_number": "agent_number",
        "customer_number": "customer_number",
        "origination": "agent", //expected values("agent","customer")
        "campaign": "campaign_value",
        "raw_data": { //CRM DATA for reports and webhook purpose
            "customer_info:customer_id": "12345",
            "customer_info:customer_name": "John Doe"
        }
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
    "message": "Call initiated successfully"
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
