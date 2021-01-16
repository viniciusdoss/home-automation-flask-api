# Device Registry Service

## Usage

All responses will have the form

```json
{
	"data": "Mixed type holding the type of the response",
	"message": "Description of what happened"
}
```

Subsequent response definitions will ony detail the expected value of the `data field`

### List all devices

**Definitions**

`GET /devices`

**Response**

- `200 OK` on success

```json
[
	{
		"identifier": "floor-lamp",
		"name": "Floor Lamp",
		"device_type": "switch",
		"controller_gateway": "192.1.68.0.2"
	},
	{
		"identifier": "sansung-tv",
		"name": "Living Room TV",
		"device_type": "tv",
		"controller_gateway": "192.168.0.9"
	}
]
```

### Registering a new device

**Definition**

`POST /devices`

**Arguments**

- `"identifier":string` a globaly unique identifier for this device
- `"name":string` a friendly name for this device
- `"device_type":string` the type of the device as understood by the client
- `"controller_gateway":string` the IP address of the device's controller

If a device with the given identifier already exists, the existing device will be overwritten.

**Responses**

- `201 Created` on success

```json
{
		"identifier": "floor-lamp",
		"name": "Floor Lamp",
		"device_type": "switch",
		"controller_gateway": "192.1.68.0.2"
	}
```

## Lookup device details

`GET /device/<identifier>`

**Response**

- `404 Not Found` if the device does not exist
- `200 OK` on success

```json
{
		"identifier": "floor-lamp",
		"name": "Floor Lamp",
		"device_type": "switch",
		"controller_gateway": "192.1.68.0.2"
	}
```

## Delete a device

**Definition**

`DELETE /devices/<identifier>`

**Response**

- `404 Not Found` if the device does not exist
- `204 No Content`