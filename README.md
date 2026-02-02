# SEC API

REST API for retrieving SEC EDGAR filings. Returns filing metadata and direct links to official SEC documents.

## Features

- Single endpoint for all supported filing types
- Returns structured JSON with direct SEC EDGAR URLs
- Supports 10-K, 10-Q, 8-K, S-1, S-2, S-3, DEF14A, 13D
- 5,000 requests/month on free tier
- Example Response:
```json
[
  {
    "symbol": "GOOG",
    "filing_type": "10-K",
    "submitted_on": "2025-02-05",
    "filing_link": "https://www.sec.gov/Archives/edgar/data/1652044/000165204425000014/goog-20241231.htm"
  }
]
```

## Authentication

1. Create account at [omkar.cloud](https://www.omkar.cloud/auth/sign-up)

<!-- ![Sign Up](https://raw.githubusercontent.com/omkarcloud/assets/master/images/signup.png) -->

2. Get API key from [omkar.cloud/api-key](https://www.omkar.cloud/api-key)

<!-- ![Copy API Key](https://raw.githubusercontent.com/omkarcloud/assets/master/images/enrichment-key-omkar.png) -->

3. Include `API-Key` header in requests

## Quick Start

```bash
curl -X GET "https://sec-api.omkar.cloud/sec?ticker=GOOG&filing=10-K" \
  -H "API-Key: YOUR_API_KEY"
```

```json
[
  {
    "symbol": "GOOG",
    "filing_type": "10-K",
    "submitted_on": "2025-02-05",
    "filing_link": "https://www.sec.gov/Archives/edgar/data/1652044/000165204425000014/goog-20241231.htm"
  }
]
```

## Installation

### Python

```bash
pip install requests
```

```python
import requests

response = requests.get(
    "https://sec-api.omkar.cloud/sec",
    params={"ticker": "GOOG", "filing": "10-K"},
    headers={"API-Key": "YOUR_API_KEY"}
)

filings = response.json()
```

### Node.js

```bash
npm install axios
```

```javascript
import axios from "axios";

const response = await axios.get("https://sec-api.omkar.cloud/sec", {
    params: { ticker: "GOOG", filing: "10-K" },
    headers: { "API-Key": "YOUR_API_KEY" }
});

const filings = response.data;
```

## API Reference

### Endpoint

```
GET https://sec-api.omkar.cloud/sec
```

### Headers

| Header | Required | Description |
|--------|----------|-------------|
| `API-Key` | Yes | API key from [omkar.cloud/api-key](https://www.omkar.cloud/api-key) |

### Parameters

| Parameter | Required | Default | Description |
|-----------|----------|---------|-------------|
| `ticker` | Yes | — | Stock ticker symbol |
| `filing` | No | `10-K` | Filing type |

### Supported Filing Types

| Type | Description |
|------|-------------|
| `10-K` | Annual report |
| `10-Q` | Quarterly report |
| `8-K` | Current report (material events) |
| `S-1` | IPO registration statement |
| `S-2` | Simplified registration |
| `S-3` | Shelf registration |
| `DEF14A` | Proxy statement |
| `13D` | Beneficial ownership (>5%) |

### Response

```json
[
  {
    "symbol": "string",
    "filing_type": "string",
    "submitted_on": "YYYY-MM-DD",
    "filing_link": "string"
  }
]
```

| Field | Type | Description |
|-------|------|-------------|
| `symbol` | string | Ticker symbol |
| `filing_type` | string | SEC form type |
| `submitted_on` | string | Submission date |
| `filing_link` | string | SEC EDGAR URL |

## Examples

### Fetch 10-K filings

```python
response = requests.get(
    "https://sec-api.omkar.cloud/sec",
    params={"ticker": "AAPL", "filing": "10-K"},
    headers={"API-Key": "YOUR_API_KEY"}
)

for filing in response.json():
    print(f"{filing['submitted_on']}: {filing['filing_link']}")
```

### Fetch latest 8-K

```python
response = requests.get(
    "https://sec-api.omkar.cloud/sec",
    params={"ticker": "TSLA", "filing": "8-K"},
    headers={"API-Key": "YOUR_API_KEY"}
)

latest = response.json()[0]
```

### Fetch quarterly reports

```javascript
const { data } = await axios.get("https://sec-api.omkar.cloud/sec", {
    params: { ticker: "MSFT", filing: "10-Q" },
    headers: { "API-Key": "YOUR_API_KEY" }
});

const lastFourQuarters = data.slice(0, 4);
```

## Error Handling

```python
response = requests.get(
    "https://sec-api.omkar.cloud/sec",
    params={"ticker": "INVALID"},
    headers={"API-Key": "YOUR_API_KEY"}
)

if response.status_code == 200:
    data = response.json()
    if not data:
        # No filings found
        pass
elif response.status_code == 401:
    # Invalid API key
    pass
elif response.status_code == 429:
    # Rate limit exceeded
    pass
```

## Rate Limits

| Plan | Price | Requests/Month |
|------|-------|----------------|
| Free | $0 | 5,000 |
| Starter | $25 | 100,000 |
| Grow | $75 | 1,000,000 |
| Scale | $150 | 10,000,000 |

## Support

[![Contact Us on WhatsApp about SEC API](https://raw.githubusercontent.com/omkarcloud/assets/master/images/whatsapp-us.png)](https://api.whatsapp.com/send?phone=918178804274&text=I%20have%20a%20question%20about%20the%20SEC%20API.)

[![Contact Us on Email about SEC API](https://raw.githubusercontent.com/omkarcloud/assets/master/images/ask-on-email.png)](mailto:happy.to.help@omkar.cloud?subject=SEC%20API%20Question)