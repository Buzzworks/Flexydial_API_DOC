# Bulk Contact Upload API

### `POST /api/bulkphonebookupload/v1/`

#### Parameters

Content- type: ‘application/json’

```json
{
  "campaign":"<flexydial_campaign_name(string)>",
  "bulk_data":
  [
    {
      "numeric":"<1st_customer_mobile_number(string)>",
      "user":"<flexydial_agent_id(string)>", //Data Allocation to User
      "customer_info:customer_id":"<customer_id(string)>",
		},
		{
      "numeric":"<2nd_customer_mobile_number(string)>",
      "user":"<flexydial_agent_id(string)>",
      "customer_info:customer_id":"<customer_id(string)>”,
		}
  ]
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
  "success":"Reference/Phonebook Name:<UNIQUEID_OF_UPLOAD>",
  "job_id": "<job_id>"
}
```

### Error

##### Code `500`

##### Description

```json
{
  "errors": "Headers are not matching with Campaign CRM Fields. Please refer to the sample CSV"
}
```
```json
{
  "errors": "Oops Something went wrong, Please contact Administrator"
}
```

### Scenarios
#### Inappropriate use of the “reference_field” during the insert operation
** Payload 1: **

```json
{
  "campaign":"<flexydial_campaign_name(string)>",
  "reference_field": "numeric"
  "bulk_data":
  [
    {
      "numeric":"<1st_customer_mobile_number(string)>",
      "user":"<flexydial_agent_id(string)>", //Data Allocation to User
      "flexydial_campaign_crm_section_name:field_name1(string":"value"
		},
		{
      "numeric":"<2nd_customer_mobile_number(string)>",
      "user":"<flexydial_agent_id(string)>",
      "flexydial_campaign_crm_section_name:field_name1(string":"value"
		}
   ]
}
```
** Payload 2: **

```json
{
  "campaign":"<flexydial_campaign_name(string)>",
  "reference_field": "<flexydial_campaign_crm_section_name:field_name1(string)>"
  "bulk_data":
  [
    {
      "numeric":"<1st_customer_mobile_number(string)>",
      "user":"<flexydial_agent_id(string)>", //Data Allocation to User
      "flexydial_campaign_crm_section_name:field_name1(string":"value"
		},
		{
      "numeric":"<2nd_customer_mobile_number(string)>",
      "user":"<flexydial_agent_id(string)>",
      "flexydial_campaign_crm_section_name:field_name1(string":"value"
		}
   ]
}
```
** Error Response: **
```json
{
    "errors": "Insert operation cannot have reference_field."
}
```

### For Status check of the Job

[Click here for Status Check API Doc](https://github.com/Buzzworks/Flexydial_API_DOC/blob/main/UploadStatusCheck.md)