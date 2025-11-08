# Sensor Data API

Access real-time and historical sensor data from buoys.

## Get Latest Sensor Data

Retrieve the most recent sensor readings from a buoy.

### Request

```http
GET /v1/sensor-data/{buoy_id}/latest
```

### Example Request

```bash
curl -X GET "https://api.buoysense.com/v1/sensor-data/B001/latest" \
  -H "Authorization: Bearer sk_prod_your_key"
```

### Response

```json
{
  "success": true,
  "data": {
    "buoy_id": "B001",
    "timestamp": "2025-11-09T12:00:00Z",
    "water_level": 2.3,
    "temperature": 28.5,
    "humidity": 75,
    "tilt": 2.1,
    "battery_level": 72,
    "signal_strength": 92
  }
}
```

## Get Historical Data

Query historical sensor readings with time range.

### Request

```http
GET /v1/sensor-data/{buoy_id}/history
```

### Query Parameters

| Parameter | Type | Description |
|-----------|------|-------------|
| `from` | timestamp | Start time (ISO 8601) |
| `to` | timestamp | End time (ISO 8601) |
| `interval` | string | Data aggregation interval: `1m`, `5m`, `15m`, `1h`, `1d` |
| `metrics` | array | Specific metrics to return |

### Example Request

```bash
curl -X GET "https://api.buoysense.com/v1/sensor-data/B001/history?from=2025-11-08T00:00:00Z&to=2025-11-09T00:00:00Z&interval=1h" \
  -H "Authorization: Bearer sk_prod_your_key"
```

### Response

```json
{
  "success": true,
  "data": {
    "buoy_id": "B001",
    "interval": "1h",
    "readings": [
      {
        "timestamp": "2025-11-08T00:00:00Z",
        "water_level": 1.8,
        "temperature": 27.2,
        "humidity": 78,
        "tilt": 1.9
      },
      {
        "timestamp": "2025-11-08T01:00:00Z",
        "water_level": 1.85,
        "temperature": 27.0,
        "humidity": 79,
        "tilt": 2.0
      }
    ]
  }
}
```

## Stream Real-time Data

Subscribe to real-time sensor updates via WebSocket.

### WebSocket Connection

```javascript
const ws = new WebSocket('wss://api.buoysense.com/v1/realtime');

ws.on('open', () => {
  // Authenticate
  ws.send(JSON.stringify({
    type: 'auth',
    token: 'sk_prod_your_key'
  }));
  
  // Subscribe to buoy sensor data
  ws.send(JSON.stringify({
    type: 'subscribe',
    channel: 'sensor.B001'
  }));
});

ws.on('message', (data) => {
  const event = JSON.parse(data);
  console.log('Sensor update:', event);
});
```

### Real-time Event Format

```json
{
  "type": "sensor.update",
  "buoy_id": "B001",
  "timestamp": "2025-11-09T12:00:00Z",
  "data": {
    "water_level": 2.3,
    "temperature": 28.5,
    "humidity": 75,
    "tilt": 2.1
  }
}
```

## Supported Metrics

| Metric | Unit | Description |
|--------|------|-------------|
| `water_level` | meters | Water level above sensor |
| `temperature` | °C | Air/water temperature |
| `humidity` | % | Relative humidity |
| `tilt` | degrees | Buoy tilt angle |
| `battery_level` | % | Battery charge percentage |
| `signal_strength` | % | LoRa signal quality |
