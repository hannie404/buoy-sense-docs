# API Overview

The BuoySense API provides programmatic access to all buoy sensor data, alerts, and system configurations.

## Base URL

```
https://api.buoysense.com/v1
```

For development:
```
http://localhost:3001/v1
```

## Authentication

All API requests require authentication using an API key.

### Get Your API Key

1. Log in to your BuoySense dashboard
2. Navigate to **Settings** → **Network** → **API Keys**
3. Click **Regenerate** to create a new key
4. Copy your API key (starts with `sk_prod_` or `sk_test_`)

### Using API Keys

Include your API key in the request header:

```bash
Authorization: Bearer sk_prod_your_api_key_here
```

Example request:
```bash
curl -H "Authorization: Bearer sk_prod_abc123" \
  https://api.buoysense.com/v1/buoys
```

## Rate Limiting

- **Free Tier**: 100 requests/minute
- **Pro Tier**: 1000 requests/minute
- **Enterprise**: Unlimited

Rate limit headers are included in every response:
```
X-RateLimit-Limit: 100
X-RateLimit-Remaining: 95
X-RateLimit-Reset: 1699564800
```

## Response Format

All responses are in JSON format.

### Success Response

```json
{
  "success": true,
  "data": {
    // Response data
  },
  "timestamp": "2025-11-09T12:00:00Z"
}
```

### Error Response

```json
{
  "success": false,
  "error": {
    "code": "BUOY_NOT_FOUND",
    "message": "Buoy with ID B001 not found",
    "details": {}
  },
  "timestamp": "2025-11-09T12:00:00Z"
}
```

## HTTP Status Codes

| Code | Description |
|------|-------------|
| `200` | Success |
| `201` | Created |
| `400` | Bad Request |
| `401` | Unauthorized |
| `403` | Forbidden |
| `404` | Not Found |
| `429` | Rate Limit Exceeded |
| `500` | Internal Server Error |

## Error Codes

| Code | Description |
|------|-------------|
| `INVALID_API_KEY` | API key is missing or invalid |
| `BUOY_NOT_FOUND` | Requested buoy does not exist |
| `INVALID_PARAMETERS` | Request parameters are invalid |
| `RATE_LIMIT_EXCEEDED` | Too many requests |
| `INTERNAL_ERROR` | Server error occurred |

## Pagination

List endpoints support pagination using cursor-based pagination:

```bash
GET /v1/buoys?limit=20&cursor=eyJpZCI6IkIwMDEifQ==
```

Response includes pagination metadata:
```json
{
  "data": [...],
  "pagination": {
    "has_more": true,
    "next_cursor": "eyJpZCI6IkIwMjEifQ=="
  }
}
```

## Filtering

Most list endpoints support filtering:

```bash
GET /v1/buoys?status=active&river=Pasig
GET /v1/alerts?severity=critical&from=2025-11-01
```

## Sorting

Sort results using the `sort` parameter:

```bash
GET /v1/buoys?sort=-created_at  # Descending
GET /v1/buoys?sort=water_level  # Ascending
```

## Field Selection

Request specific fields to reduce payload size:

```bash
GET /v1/buoys?fields=id,name,water_level
```

## WebSocket Support

For real-time updates, connect to our WebSocket endpoint:

```javascript
const ws = new WebSocket('wss://api.buoysense.com/v1/realtime');

ws.on('open', () => {
  ws.send(JSON.stringify({
    type: 'auth',
    token: 'sk_prod_your_key'
  }));
  
  ws.send(JSON.stringify({
    type: 'subscribe',
    channels: ['buoy.B001', 'alerts']
  }));
});

ws.on('message', (data) => {
  const event = JSON.parse(data);
  console.log(event);
});
```

## API Endpoints

### Core Resources

- [Buoys](./buoys) - Manage and query buoy devices
- [Sensor Data](./sensor-data) - Access real-time sensor readings
- [Alerts](./alerts) - Manage flood alerts and notifications
- [Analytics](./analytics) - Query analytics and reports
- [Users](./users) - User management (admin only)

### Utility Endpoints

- [Health Check](./health) - API status and uptime
- [Webhooks](./webhooks) - Configure event webhooks

## SDKs & Libraries

Official SDKs are available for:

- **JavaScript/TypeScript**: `npm install @buoysense/sdk`
- **Python**: `pip install buoysense`
- **Go**: `go get github.com/buoysense/go-sdk`

Example using JavaScript SDK:

```javascript
import BuoySense from '@buoysense/sdk';

const client = new BuoySense({
  apiKey: 'sk_prod_your_key'
});

const buoys = await client.buoys.list();
const data = await client.sensorData.get('B001');
```

## Postman Collection

Download our [Postman Collection](https://postman.com/buoysense) for easy API testing.

## Need Help?

- View detailed endpoint documentation in the sidebar
- Check our [examples](./examples)
- Join our [developer community](https://discord.gg/buoysense)
- Email: api-support@buoysense.com
