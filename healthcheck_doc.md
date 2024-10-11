# ${api.name} API Documentation

## Overview
The HealthCheck API allows you to monitor the status of various services by providing simple health check endpoints. This API provides two operations for checking overall health and the health of specific services by their ID.

## Endpoints

### 1. GET `/v1/healthcheck`

- **Description**: Retrieve the health status of all services.
- **Response**: A JSON object containing the status of each service.
- **Status Codes**:
  - `200 OK`: Health check successful.
  - `500 Internal Server Error`: There was an issue with one or more services.

#### Example Response:
```json
{
  "status": "healthy",
  "services": [
    {"name": "database", "status": "healthy"},
    {"name": "cache", "status": "unhealthy"}
  ]
}
```

---

### 2. GET `/v1/healthcheck/{id}`

- **Description**: Retrieve the health status of a specific service by its ID.
- **Path Parameters**:
  - `id` (string): The unique identifier of the service.
- **Response**: A JSON object containing the status of the requested service.
- **Status Codes**:
  - `200 OK`: Health check successful.
  - `404 Not Found`: Service with the provided ID was not found.
  - `500 Internal Server Error`: There was an issue with the requested service.

#### Example Response:
```json
{
  "status": "healthy",
  "service": {
    "id": "database",
    "status": "healthy"
  }
}
```

## Code Samples

### Python Example

To call the HealthCheck API using Python, you can use the `requests` library.

```python
import requests

# Get overall health status
response = requests.get('https://api.example.com/v1/healthcheck')
if response.status_code == 200:
    print(response.json())

# Get health status of a specific service by ID
service_id = "database"
response = requests.get(f'https://api.example.com/v1/healthcheck/{service_id}')
if response.status_code == 200:
    print(response.json())
```

### JavaScript Example

To call the HealthCheck API using JavaScript, you can use the `fetch` API.

```javascript
// Get overall health status
fetch('https://api.example.com/v1/healthcheck')
    .then(response => response.json())
    .then(data => console.log(data))
    .catch(error => console.error('Error:', error));

// Get health status of a specific service by ID
const serviceId = 'database';
fetch(`https://api.example.com/v1/healthcheck/${serviceId}`)
    .then(response => response.json())
    .then(data => console.log(data))
    .catch(error => console.error('Error:', error));
```

## Error Handling

Both endpoints may return the following errors:
- **500 Internal Server Error**: If there is a server-side issue during the health check.
- **404 Not Found** (for `/v1/healthcheck/{id}`): If the service ID does not exist.

## Conclusion

The HealthCheck API provides a simple way to monitor the status of various services. Use the provided endpoints to check the overall health of all services or the status of individual services by their ID.
