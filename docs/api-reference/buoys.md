# Buoys API

Manage and query buoy devices.

## List All Buoys

Get a list of all buoys in your system.

### Request

```http
GET /v1/buoys
```

### Query Parameters

| Parameter | Type | Description |
|-----------|------|-------------|
| `status` | string | Filter by status: `normal`, `rising`, `alert`, `offline` |
| `river` | string | Filter by river name |
| `limit` | number | Number of results (default: 20, max: 100) |
| `cursor` | string | Pagination cursor |

### Example Request

```bash
curl -X GET "https://api.buoysense.com/v1/buoys?status=normal&limit=10" \
  -H "Authorization: Bearer sk_prod_your_key"
```

### Response

```json
{
  "success": true,
  "data": [
    {
      "id": "B001",
      "name": "Pasig North",
      "river": "Pasig River",
      "location": "Pasig Bridge",
      "latitude": 14.5995,
      "longitude": 120.9842,
      "status": "normal",
      "water_level": 2.3,
      "battery_level": 72,
      "signal_strength": 92,
      "last_transmission": "2025-11-09T12:00:00Z",
      "created_at": "2025-01-15T08:00:00Z",
      "updated_at": "2025-11-09T12:00:00Z"
    }
  ],
  "pagination": {
    "has_more": false,
    "next_cursor": null
  }
}
```

## Get Buoy by ID

Retrieve details of a specific buoy.

### Request

```http
GET /v1/buoys/{buoy_id}
```

### Path Parameters

| Parameter | Type | Description |
|-----------|------|-------------|
| `buoy_id` | string | Unique buoy identifier (e.g., "B001") |

### Example Request

```bash
curl -X GET "https://api.buoysense.com/v1/buoys/B001" \
  -H "Authorization: Bearer sk_prod_your_key"
```

### Response

```json
{
  "success": true,
  "data": {
    "id": "B001",
    "name": "Pasig North",
    "river": "Pasig River",
    "location": "Pasig Bridge",
    "latitude": 14.5995,
    "longitude": 120.9842,
    "status": "normal",
    "water_level": 2.3,
    "battery_level": 72,
    "signal_strength": 92,
    "sensors": {
      "ultrasonic": "HC-SR04",
      "tilt": "MPU-6050",
      "temperature_humidity": "DHT22"
    },
    "hardware": {
      "communication": "LoRa 915MHz",
      "solar_panel": "5W",
      "battery": "3.7V LiPo"
    },
    "last_transmission": "2025-11-09T12:00:00Z",
    "created_at": "2025-01-15T08:00:00Z",
    "updated_at": "2025-11-09T12:00:00Z"
  }
}
```

## Create Buoy

Add a new buoy to the system.

### Request

```http
POST /v1/buoys
```

### Request Body

```json
{
  "id": "B010",
  "name": "Marikina Bridge",
  "river": "Marikina River",
  "location": "Marikina",
  "latitude": 14.6507,
  "longitude": 121.1029,
  "sensors": {
    "ultrasonic": "HC-SR04",
    "tilt": "MPU-6050"
  }
}
```

### Example Request

```bash
curl -X POST "https://api.buoysense.com/v1/buoys" \
  -H "Authorization: Bearer sk_prod_your_key" \
  -H "Content-Type: application/json" \
  -d '{
    "id": "B010",
    "name": "Marikina Bridge",
    "river": "Marikina River",
    "location": "Marikina",
    "latitude": 14.6507,
    "longitude": 121.1029
  }'
```

### Response

```json
{
  "success": true,
  "data": {
    "id": "B010",
    "name": "Marikina Bridge",
    "river": "Marikina River",
    "location": "Marikina",
    "latitude": 14.6507,
    "longitude": 121.1029,
    "status": "offline",
    "water_level": 0,
    "battery_level": 0,
    "signal_strength": 0,
    "created_at": "2025-11-09T12:30:00Z",
    "updated_at": "2025-11-09T12:30:00Z"
  }
}
```

## Update Buoy

Update buoy information.

### Request

```http
PATCH /v1/buoys/{buoy_id}
```

### Request Body

```json
{
  "name": "Pasig North Station",
  "location": "Pasig Bridge - North Side"
}
```

### Example Request

```bash
curl -X PATCH "https://api.buoysense.com/v1/buoys/B001" \
  -H "Authorization: Bearer sk_prod_your_key" \
  -H "Content-Type: application/json" \
  -d '{
    "name": "Pasig North Station"
  }'
```

### Response

```json
{
  "success": true,
  "data": {
    "id": "B001",
    "name": "Pasig North Station",
    "updated_at": "2025-11-09T12:35:00Z"
  }
}
```

## Delete Buoy

Remove a buoy from the system.

### Request

```http
DELETE /v1/buoys/{buoy_id}
```

### Example Request

```bash
curl -X DELETE "https://api.buoysense.com/v1/buoys/B010" \
  -H "Authorization: Bearer sk_prod_your_key"
```

### Response

```json
{
  "success": true,
  "message": "Buoy B010 deleted successfully"
}
```

## Get Buoy Status

Get real-time status of all buoys.

### Request

```http
GET /v1/buoys/status
```

### Example Request

```bash
curl -X GET "https://api.buoysense.com/v1/buoys/status" \
  -H "Authorization: Bearer sk_prod_your_key"
```

### Response

```json
{
  "success": true,
  "data": {
    "total": 25,
    "online": 24,
    "offline": 1,
    "by_status": {
      "normal": 20,
      "rising": 3,
      "alert": 1,
      "offline": 1
    }
  }
}
```

## Error Responses

### Buoy Not Found

```json
{
  "success": false,
  "error": {
    "code": "BUOY_NOT_FOUND",
    "message": "Buoy with ID B999 not found"
  }
}
```

### Invalid Parameters

```json
{
  "success": false,
  "error": {
    "code": "INVALID_PARAMETERS",
    "message": "Invalid latitude value",
    "details": {
      "field": "latitude",
      "value": "invalid",
      "expected": "number between -90 and 90"
    }
  }
}
```

## Buoy Object Schema

| Field | Type | Description |
|-------|------|-------------|
| `id` | string | Unique buoy identifier |
| `name` | string | Human-readable buoy name |
| `river` | string | River name |
| `location` | string | Physical location description |
| `latitude` | number | GPS latitude (-90 to 90) |
| `longitude` | number | GPS longitude (-180 to 180) |
| `status` | enum | `normal`, `rising`, `alert`, `offline` |
| `water_level` | number | Current water level in meters |
| `battery_level` | number | Battery percentage (0-100) |
| `signal_strength` | number | Signal strength percentage (0-100) |
| `sensors` | object | Installed sensor details |
| `hardware` | object | Hardware specifications |
| `last_transmission` | timestamp | Last data transmission time |
| `created_at` | timestamp | Creation timestamp |
| `updated_at` | timestamp | Last update timestamp |
