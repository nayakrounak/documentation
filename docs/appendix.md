# JOSN Schema

## Digital ID

```JSON
{
  "$schema": "http://json-schema.org/draft-07/schema#",
  "title": "Digital ID",
  "type": "object",
  "properties": {
    "serialNo": {
      "type": "string",
      "description": "Serial number of the device."
    },
    "make": {
      "type": "string",
      "description": "Brand name of the device."
    },
    "model": {
      "type": "string",
      "description": "Model of the device."
    },
    "type": {
      "type": "string",
      "enum": [
        "Fingerprint",
        "Iris",
        "Face"
      ],
      "description": "Type of the biometric device."
    },
    "deviceSubType": {
      "type": "string",
      "enum": [
        "Slap",
        "Single",
        "Touchless",
        "Double",
        "Full face"
      ],
      "description": "Subtype of the biometric device."
    },
    "deviceProvider": {
      "type": "string",
      "description": "Name of the device provider."
    },
    "deviceProviderId": {
      "type": "string",
      "description": "ID of the device provider."
    },
    "dateTime": {
      "type": "string",
      "description": "Current date and time in ISO 8601 format (yyyy-mm-ddTHH:MM:ssZ).",
      "pattern": "^\\d{4}-\\d{2}-\\d{2}T\\d{2}:\\d{2}:\\d{2}Z$"
    }
  },
  "required": [
    "serialNo",
    "make",
    "model",
    "type",
    "deviceSubType",
    "deviceProvider",
    "dateTime"
  ],
  "additionalProperties": false
}
```

## Device Discovery Request
```JSON
{
  "$schema": "http://json-schema.org/draft-07/schema#",
  "title": "Device Discovery Request",
  "type": "object",
  "properties": {
    "type": {
      "type": "string",
      "description": "Type of device. Type Biometric Device is used for any biometric device."
      "enum": [
        "Biometric Device",
        "Finger",
        "Face",
        "Iris"
      ]
    }
  },
  "required": ["type"],
  "additionalProperties": false
}
```

## Device Discovery Response
```JSON
{
  "$schema": "http://json-schema.org/draft-07/schema#",
  "title": "Device Discovery Response",
  "type": "array",
  "items": {
    "type": "object",
    "properties": {
      "deviceId": {
        "type": "string",
        "description": "Internal ID to identify the actual biometric device within the device service."
      },
      "deviceStatus": {
        "type": "string",
        "description": "Device status",
        "enum": ["Ready", "Busy", "Not Ready", "Not Registered"]
      },
      "certification": {
        "type": "string",
        "description": "Certification level",
        "enum": ["L0", "L1"]
      },
      "serviceVersion": {
        "type": "string",
        "description": "Device service version"
      },
      "deviceSubId": {
        "type": "array",
        "items": {
          "type": "integer",
          "description": "Supported device sub ID",
          "enum": [0, 1, 2, 3]
        },
        "description": "Array of supported device sub IDs"
      },
      "callbackId": {
        "type": "string",
        "description": "Base URL to reach the device"
      },
      "digitalId": {
        "type": "string",
        "description": "Unsigned Digital ID of the device"
      },
      "deviceCode": {
        "type": "string",
        "description": "Same as serialNo in digital ID"
      },
      "specVersion": {
        "type": "array",
        "items": {
          "type": "string",
          "description": "Supported SBI specification version"
        },
        "description": "Array of supported SBI specification versions"
      },
      "purpose": {
        "type": "string",
        "description": "Purpose of the device in the SBI ecosystem",
        "enum": ["Auth", "Registration", ""]
      },
      "error": {
        "type": "object",
        "properties": {
          "errorCode": {
            "type": "string",
            "description": "Standardized error code defined in the error code section"
          },
          "errorInfo": {
            "type": "string",
            "description": "Description of the error that can be displayed to end user. Multi-lingual support."
          }
        },
        "description": "Relevant errors as defined under the error section of this document."
      }
    }
  }
}
```
