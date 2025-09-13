# 📌 Device Fingerprint & Bot Detection API

Detect unique device/browser fingerprints and identify potential bots or automated tools.
Support  **POST** (JSON body) requests.

![Device Fingerprint & Bot Detection API](https://res.cloudinary.com/ds64xs2lp/image/upload/v1757735565/fingerprinting_aettoj.gif)

---

* [Get Started on RapidAPI](https://rapidapi.com/dakidarts-dakidarts-default/api/device-fingerprint-bot-detection-api)
* [API Docs on Dakidarts](https://dakidarts.com/api/device-fingerprint-and-bot-detection-api/)

## Base URL

```
device-fingerprint-bot-detection-api.p.rapidapi.com
```

---

## Endpoint



### 🔹 `POST /fingerprint`

Generates a fingerprint from **custom JSON input**.
Supports both **snake\_case** and **camelCase** keys.

#### Request Body (JSON)

* `user_agent` or `userAgent` (string, optional) → Browser User-Agent.
* `ip` (string, optional) → Client IP address (defaults to request’s remote address).
* `headers` (object, optional) → Custom headers dictionary.

#### Example

```bash
curl -X POST http://127.0.0.1:5000/fingerprint \
  -H "Content-Type: application/json" \
  -d '{
        "userAgent": "Mozilla/5.0 (X11; Linux)",
        "ip": "203.0.113.9",
        "headers": {"X-Test-Header":"boom"}
      }'
```

#### Response

```json
{
  "fingerprint": "2c9e2a54d6a5f0f6f83b4a88964b94f84b309c1e17c2d4f31cbf10c0f5a1c123",
  "ip": "203.0.113.9",
  "user_agent": "Mozilla/5.0 (X11; Linux)",
  "risk": {
    "risk_score": 0,
    "risk_level": "low",
    "reasons": []
  }
}
```


---

## 🔍 Risk Detection

Risk score is computed using heuristic rules:

* Missing User-Agent → +40
* Suspicious UA keywords (`headless`, `puppeteer`, `selenium`, etc.) → +50
* AJAX automation header (`X-Requested-With: XMLHttpRequest`) → +20
* Proxy headers (`X-Forwarded-For`, `CF-Connecting-IP`) → flagged in reasons

### Risk Levels

* `low` → 0–29
* `medium` → 30–69
* `high` → 70+


