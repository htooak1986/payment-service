# Payment Service

.NET REST API used by `order-service` to authorize checkout payments.

## Endpoints

- `GET /payment/health`
- `POST /payment/authorize`

## Local Docker Build

```bash
docker build -f deployment/Dockerfile.dev -t payment-service:local .
```

## Run

```bash
docker run --rm -p 3003:3003 \
  -e PAYMENT_APPROVAL_LIMIT=500 \
  payment-service:local
```

## Test

Approved:

```bash
curl -X POST http://localhost:3003/payment/authorize \
  -H "Content-Type: application/json" \
  -d '{"orderId":"1","amount":120.50,"currency":"USD"}'
```

Declined:

```bash
curl -X POST http://localhost:3003/payment/authorize \
  -H "Content-Type: application/json" \
  -d '{"orderId":"2","amount":900.00,"currency":"USD"}'
```
