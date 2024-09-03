# Lead Insert/Update Status Check API

### `POST /api/bulkphonebookupload/status/<operation_status_reference_id>/ `

#### Parameters


**AUTHORIZATION**:

[Click here for authentication API Doc](https://github.com/Buzzworks/Flexydial_API_DOC/blob/main/Authentication.md)

**API Key:** tokenAuth

Token-based authentication with required prefix "**Token**"

**Header Parameter Name:** Authorization



### Responses

### Success
```json
{
    "status": "Completed"
}
```
### Pending Response
```json
{
    "status": "Pending state. Please check with Administrator!"
}
```

### Error

##### Code `500`

##### Description

**Invalid “operation_status_reference_id” provided in GET request URL**
```json
{
    "errors": "Job not found."
}
```
**When inserted/updated data is improper**
```json
{
    "status": "Invalid Data",
    "improper_data": [
        {
            "flexydial_campaign_crm_section_name:field_name1": "value"
            "flexydial_campaign_crm_section_name:field_name2": "value"
            "description": "{error_description}"
        }
    ]
}
```

```json
{
    "status": "Invalid Data",
    "improper_data": [
        {
            "numeric": "value"
            "flexydial_campaign_crm_section_name:field_name2": "value"
            "description": "{error_description}"
        }
    ]
}
```