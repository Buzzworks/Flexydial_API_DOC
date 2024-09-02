# Flexydial Authentication Token Generation

## Authorization API

### `POST /api/generate-token/`

#### Parameters

Content- type: ‘application/json’

```json
{
  "username": "string",
  "password": "string"
}
```

### Responses

#### Code `200`

#### Description

```json
{
  "token": "string"
}
```
