# Day 01 – What is a Backend?

## What I learned
Today I watched this video:
https://www.youtube.com/watch?v=6Ss4dJD9Kzg&list=PLui3EUkuMTPgZcV0QhQrOcwMPcBCcd_Q1&index=3

This is the 3rd video from the *Backend from First Principles* series by Sriniously, which is highly recommended on YouTube. I found this video quite high level as it targets backend engineers, but it was still useful for building foundational understanding.

I learned that a backend is not just about storing data, as I originally thought. The backend is where logic, rules, and decision-making live. Frontend tools are mainly interfaces for interaction, while the backend is where rules are enforced and decisions are made regardless of who sends the request.

## Request trace exercise – wrong vs correct understanding
I called my FastAPI endpoint via the `/docs` page and identified the client, request, backend logic, and response.  
(The exact steps are documented in a separate exercise file.)

### Client
- Initial understanding:
  Me from FastAPI http://127.0.0.1:8000
- Correct understanding:
  The client is my browser using FastAPI Swagger UI (`/docs`). FastAPI itself is the backend, not the client.

### Request
- Initial understanding:
  POST
- Correct understanding:
  POST /ingest  
  (An HTTP request is always method + path, not just the method.)

### Payload
- Initial understanding:
  Text string "Tracing one request end to end"
- Correct understanding:
  JSON payload sent from client to backend:
  `{ "text": "Tracing one request end to end" }`

### Backend entry point
- Initial understanding:
  Not sure
- Correct understanding:
  The backend entry point is the `ingest` function in `main.py`, mapped to `POST /ingest`.

### Decision / logic
- Initial understanding:
  Count words in the string
- Correct understanding:
  The backend reads the input text and applies business logic by counting the number of words.

### Response
- Initial understanding:
  200 response successful and returned a string
- Correct understanding:
  The backend returns an HTTP 200 status code with a JSON response containing:
  - the received text
  - the calculated word count

### Effect
- Initial understanding:
  Just calculation
- Correct understanding:
  No data was stored or changed. The backend only performed a calculation with no side effects.
