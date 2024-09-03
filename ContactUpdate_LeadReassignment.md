# Bulk Contact Upload API

### `POST /api/bulkphonebookupload/v1/`

#### Parameters

Content- type: ‘application/json’
**Type: 1  - Using “numeric” as a reference field**
```json
{
  "campaign": "<flexydial_campaign_name(string)>",
  "reference_field": "numeric", //Customer Mobile Number
  "action_type": "update",                                               //make sure this is present for the update operation
  "bulk_data": [
    {
      "numeric": "value",                                                //reference_field that has been mentioned earlier
      "flexydial_campaign_crm_section_name:field_name1": "value",
      "flexydial_campaign_crm_section_name:field_name2": "value"
    },
    {
      "numeric": "value",                                                //reference_field that has been mentioned earlier
      "flexydial_campaign_crm_section_name:field_name1": "value",
      "flexydial_campaign_crm_section_name:field_name2": "value"
    }
  ]
}
```

**Type: 2 - Lead Update with reference field as CRM Field(UniqueID)**
```json
{
  "campaign": "<flexydial_campaign_name(string)>",
  "reference_field": "<flexydial_campaign_crm_section_name:field_name1(string)>",    //customer_info:customer_id - reference_crm_field - should be available in bulk_data as well
  "action_type": "update",                                                           //make sure this is present for the update operation
  "bulk_data": [
    {
      "flexydial_campaign_crm_section_name:field_name1": "value",                   //reference_crm_field that has been mentioned earlier
      "flexydial_campaign_crm_section_name:field_name2": "value"
      "numeric":"value"
    },
    {
      "flexydial_campaign_crm_section_name:field_name1": "value",                  //reference_crm_field that has been mentioned earlier
      "flexydial_campaign_crm_section_name:field_name2": "value",
      "numeric":"value"
    }
  ]
}
```
**Type: 3 - Agent Reassignment with reference field as numeric**
```json
{
  "campaign": "<flexydial_campaign_name(string)>",
  "reference_field": "numeric",
  "action_type": "update",                                                           //make sure this is present for the update operation
  "bulk_data": [
    {
      "user":"<flexydial_agent_id(string)>",
      "numeric":"value"
    },
    {
      "user":"<flexydial_agent_id(string)>",
      "numeric":"value"
    }
  ]
}
```
**Type: 4 - Agent Reassignment with reference field as CRM Field(UniqueID)**
```json
{
  "campaign": "<flexydial_campaign_name(string)>",
  "reference_field": "<flexydial_campaign_crm_section_name:field_name1(string)>", //customer_info:customer_id - reference_crm_field - should be available in bulk_data as well
  "action_type": "update",                                                           //make sure this is present for the update operation
  "bulk_data": [
    {
      "user":"<flexydial_agent_id(string)>",
      "numeric":"value"
    },
    {
      "user":"<flexydial_agent_id(string)>",
      "numeric":"value"
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

##### Code `201`

##### Description

```json
{
  "success":"Reference/Phonebook Name:<UNIQUEID_OF_UPLOAD>",
  "job_id": "<job_id>"
}
```

### Error
#### Type 1: Missing “campaign” or “bulk_data” in the payload
**Payload 1:**
```json
{
    "reference_field": "numeric",
    "action_type": "update",
    "bulk_data":[
        {
        "flexydial_campaign_crm_section_name:field_name1":"value",
        "flexydial_campaign_crm_section_name:field_name2":"value"
        },
        {
        "supersection:age":"value",
        "supersection:name":"value"
        }
    ]
}
```
```json
{
  "errors": "Oops Something went wrong, Please contact Administrator"
}
```

### Scenarios
#### Inappropriate use of the “reference_field” during the insert operation
**Payload 1:**

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

**Payload 2:**

```json
{
    "campaign": "<flexydial_campaign_name(string)>"
}
```
**Payload 3:**
```json
{
    "bulk_data":[
        {
        "flexydial_campaign_crm_section_name:field_name1":"value",
        "flexydial_campaign_crm_section_name:field_name2":"value"
        },
        {
        "flexydial_campaign_crm_section_name:field_name1":"value",
        "flexydial_campaign_crm_section_name:field_name2":"value"
        }
    ]
}
```
**Error Response:**
```json
{
    "errors": "Invalid request structure"
}
```

#### Type 2: Missing “campaign” or “bulk_data” in the payload
**Payload 1:**

```json
{
    "campaign":"<flexydial_campaign_name(string)>",
    "action_type": "update",
    "bulk_data":[
        {
        "flexydial_campaign_crm_section_name:field_name1":"value",
        "flexydial_campaign_crm_section_name:field_name2":"value"
        },
        {
        "flexydial_campaign_crm_section_name:field_name1":"value",
        "flexydial_campaign_crm_section_name:field_name2":"value"
        }
    ]
}
```

**Error Response:**
```json
{
    "errors": "reference_field is missing in the request!"
}
```

#### Type 3:  “reference_field” missing in the “bulk_data”
**Payload 1:**

```json
{
    "campaign":"<flexydial_campaign_name(string)>",
    "reference_field": "numeric",
    "action_type": "update",
    "bulk_data":[
        {
        "flexydial_campaign_crm_section_name:field_name1":"value",
        "flexydial_campaign_crm_section_name:field_name2":"value"
        },
        {
        "flexydial_campaign_crm_section_name:field_name1":"value",
        "flexydial_campaign_crm_section_name:field_name2":"value"
        }
    ]
}
```
**Payload 2:**

```json
{
    "campaign":"<flexydial_campaign_name(string)>",
    "reference_field": "numeric",
    "action_type": "update",
    "bulk_data":[
        {
        "flexydial_campaign_crm_section_name:field_name1":"value",
        "flexydial_campaign_crm_section_name:field_name2":"value"
        },
        {
        "flexydial_campaign_crm_section_name:field_name1":"value",
        "flexydial_campaign_crm_section_name:field_name2":"value"
        }
    ]
}
```
**Payload 3:**
```json
{
    "campaign":"<flexydial_campaign_name(string)>",
    "reference_field": "flexydial_campaign_crm_section_name:field_name1",
    "action_type": "update",
    "bulk_data":[
        {
        "numeric":"value",
        "flexydial_campaign_crm_section_name:field_name2":"value"
        },
        {
        "numeric":"value",
        "flexydial_campaign_crm_section_name:field_name1":"value",
        "flexydial_campaign_crm_section_name:field_name2":"value"
        }
    ]
}
```
**Payload 4:**
```json
{
    "campaign":"<flexydial_campaign_name(string)>",
    "reference_field": "flexydial_campaign_crm_section_name:field_name1",
    "action_type": "update",
    "bulk_data":[
        {
        "numeric":"value",
        "flexydial_campaign_crm_section_name:field_name2":"value"
        },
        {
        "numeric":"value",
        "flexydial_campaign_crm_section_name:field_name2":"value"
        }
    ]
}
```

**Error Response:**
```json
{
    "errors": "reference_field - numeric is missing in some bulk_data item(s)"
}
```

```json
{
    "errors": "reference_field - <flexydial_campaign_crm_section_name:field_name> is missing in some bulk_data item(s)"
}
```

#### Type 4:  “reference_field” missing in the “bulk_data”
**Payload 1:**
```json
{
    "campaign":"<flexydial_campaign_name(string)>",
    "reference_field": "numeric",
    "action_type": "update",
    "bulk_data":[
        {
        "numeric":"value",
        "flexydial_campaign_crm_section_name:field_name1":"value",
        "flexydial_campaign_crm_section_name:field_name2":"value"
        },
        {
        "numeric":"value",
        "flexydial_campaign_crm_section_name:field_name2":"value"
        }
    ]
}
```

**Payload 2:**
```json
{
    "campaign":"<flexydial_campaign_name(string)>",
    "reference_field": "flexydial_campaign_crm_section_name:field_name2",
    "action_type": "update",
    "bulk_data":[
        {
        "numeric":"value",
        "flexydial_campaign_crm_section_name:field_name1":"value",
        "flexydial_campaign_crm_section_name:field_name2":"value"
        },
        {
        "flexydial_campaign_crm_section_name:field_name2":"value",
        "numeric":"value",
        }
    ]
}
```
```json
{
    "campaign":"<flexydial_campaign_name(string)>",
    "reference_field": "numeric",
    "action_type": "update",
    "bulk_data":[
        {
        "numeric":"value",
        "flexydial_campaign_crm_section_name:field_name1":"value",
        "flexydial_campaign_crm_section_name:field_name2":"value"
        },
        {
        "numeric":"value",
        }
    ]
}
```

**Error Response:**
```json
{
    "errors": "All items in bulk_data must have uniform structure"
}
```

#### Type 5:  Columns that needs to be updated were not provided only “reference_field” is passed
**Payload 1:**
```json
{
    "campaign":"<flexydial_campaign_name(string)>",
    "reference_field": "numeric",
    "action_type": "update",
    "bulk_data":[
        {
        "numeric":"value"
        },
        {
        "numeric":"value"
        }
    ]
}
```

**Error Response:**
```json
{
    "errors": "Please provide the columns data that you want to update along with the reference_field"
}
```

### For Status check of the Job

[Click here for Status Check API Doc](https://github.com/Buzzworks/Flexydial_API_DOC/blob/main/UploadStatusCheck.md)