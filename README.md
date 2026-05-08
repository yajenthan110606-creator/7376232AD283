# Vehicle Maintenance Scheduler Microservice

This backend microservice solves the vehicle maintenance scheduling problem using a 0/1 knapsack dynamic programming approach for each depot.

## Endpoints

- `GET /health`
- `POST /api/vehicle-scheduling/optimize`

## Environment Variables

Copy values from `.env.example` into your shell or environment before starting the service.

- `ASSESSMENT_AUTH_TOKEN` is required unless you provide `ASSESSMENT_AUTH_VALUE`.
- `ASSESSMENT_AUTH_VALUE` lets you send a complete auth header value if the assessment token does not use the default `Bearer <token>` format.
- `INTERNAL_API_KEY` protects the optimize route through the `x-api-key` header when set.

## Run

```powershell
node src/server.js
```

## Example Request

```powershell
$headers = @{
  Authorization = "Bearer <assessment-token>"
  "x-api-key" = "<internal-api-key>"
  "Content-Type" = "application/json"
}

Invoke-RestMethod -Method Post -Uri http://localhost:8080/api/vehicle-scheduling/optimize -Headers $headers -Body "{}"
```

The service writes structured request logs to `logs/app.log` and stores the latest generated schedule in `vehicle_scheduling/latest-schedule.json`.
