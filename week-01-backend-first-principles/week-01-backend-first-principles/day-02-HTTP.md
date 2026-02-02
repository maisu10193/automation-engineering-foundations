# Day 02 – HTTP Requests, Responses, and Side Effects

## What I studied
Today I studied selected parts of the video **“Understanding HTTP for backend engineers”** (Sriniously), focusing only on:
- What an HTTP request is
- What an HTTP response is
- HTTP methods (especially POST)
- The idea of idempotent vs non-idempotent requests

I intentionally skipped many advanced sections (headers, CORS, caching, TLS) to focus on fundamentals and practice.

---

## What I learned (theory)
- HTTP is the message format used between a client and a backend.
- A client sends an **HTTP request** (method, path, body).
- The backend processes the request and returns an **HTTP response** (status code, body).
- Requests always go **client → backend**.
- Responses always go **backend → client**.
- HTTP itself does not decide meaning; the backend logic does.

---

## Practice – HTTP request tracing
I used FastAPI Swagger UI (`/docs`) as a client and sent POST requests to my backend.

From observation:
- Method: POST
- Path: `/ingest`
- Request body:
  ```json
  { "text": "HTTP practice exercise" }
  ```
- Response body:
  ```json
  {
    "received_text": "HTTP practice exercise",
    "word_count": 3
  }
  ```

This helped me clearly separate:
- URL vs path
- request body vs full request
- client responsibility vs backend responsibility

---

## Exercise – Same request twice (idempotency intuition)
I sent the same POST request twice to `/ingest` when the backend had **no side effects**.

Observation:
- Both responses were identical.
- No data was stored.
- Retrying the request caused no problem.

Conclusion:
- Even though the method was POST, the operation behaved **idempotently** because it had no side effects.

---

## Exercise – Breaking it on purpose (side effects)
I modified the backend to store incoming text in an in-memory list (`received_events`).

After sending the same POST request twice:
- `events_count` increased from 1 → 2
- GET `/events` showed duplicate entries

Conclusion:
- Retrying a POST request **created duplicate side effects**.
- This request is **not safe to retry automatically**.

---

## Key insight for automation
- Automation tools (n8n, Power Automate, webhooks) rely on HTTP.
- Networks fail and retries happen.
- If a request has side effects, retries can silently create duplicates.
- Understanding idempotency is critical for building reliable automation systems.

---

## Personal reflection
This session made it clear why learning backend fundamentals matters even when using low-code tools.
Without understanding HTTP and side effects, it is easy to build automations that work most of the time but fail in subtle and dangerous ways.
