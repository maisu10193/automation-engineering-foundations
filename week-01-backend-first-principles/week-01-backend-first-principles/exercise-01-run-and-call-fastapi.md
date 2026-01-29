# Exercise 01 – Run a backend server and send one request

This exercise demonstrates how a client sends an HTTP request to a backend
and how the backend processes the request and returns a response.

This guide assumes no prior backend knowledge.

---

## Step 1 – Open PowerShell and navigate to the project folder

```powershell
cd C:\Users\Username\ai-automation-platform
```

---

## Step 2 – Activate the virtual environment

```powershell
.\venv\Scripts\Activate.ps1
```

When this works, `(venv)` appears at the beginning of the terminal line.

---

## Step 3 – Start the backend server

```powershell
python -m uvicorn main:app --reload
```

The backend server is now running at:

```
http://127.0.0.1:8000
```

---

## Step 4 – Open the API client

Open a browser and go to:

```
http://127.0.0.1:8000/docs
```

This page (Swagger UI) acts as a client that can send HTTP requests to the backend.

---

## Step 5 – Send a request

1. Open **POST /ingest**
2. Click **Try it out**
3. Enter the request body:

```json
{
  "text": "Tracing one request end to end"
}
```

4. Click **Execute**

