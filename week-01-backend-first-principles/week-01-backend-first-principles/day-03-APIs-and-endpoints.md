# Day 03 – APIs and Endpoints

## What I studied

Today I studied the fundamentals of APIs and endpoints using:
- "APIs for Beginners 2023 - How to use an API" by freeCodeCamp (first 25 minutes)
- DummyJSON API documentation (https://dummyjson.com/docs/products)

---

## What I learned (theory)

### API vs Endpoint

- **API** = the whole system that defines what you can ask for and how to ask for it. It includes all the rules, all the endpoints, and the overall contract between client and backend.
- **Endpoint** = one specific URL + method combination that does one thing. It's a single "door" into the API.

Example:
- My FastAPI app **is** an API
- `POST /ingest` is one endpoint within that API
- `GET /events` is another endpoint within the same API

An API can have 1 endpoint or 100 endpoints. The API is the whole thing; endpoints are the individual doors into it.

### Path naming

The path (like `/ingest` or `/events`) is whatever I decide to name it when I define the endpoint. There's no magic — I choose the name and the backend maps that path to a function.

**Conventions that make APIs easier to understand:**

| Convention | Example | Why |
|------------|---------|-----|
| Use nouns, not verbs | `/deals` not `/getDeals` | The HTTP method already says the action |
| Use plurals for collections | `/deals` not `/deal` | Working with a collection |
| Use IDs for specific items | `/deals/3` not `/dealThree` | Predictable pattern |
| Keep it lowercase | `/deals` not `/Deals` | Easier to type, fewer errors |

---

## Exercise – List endpoints in my FastAPI app

| Method | Path | What it does |
|--------|------|--------------|
| GET | `/` | Returns a welcome message |
| POST | `/ingest` | Receives text, counts words, stores the text, returns word count and event count |
| GET | `/events` | Returns all stored events and the total count |

---

## Exercise – Why GET vs POST?

`GET /events` only **reads** existing data without changing anything on the server. I could call it 100 times and nothing changes.

`POST /ingest` **creates** a new entry in the stored events. Each call changes the server state.

- **GET** = read data, no side effects, safe to retry
- **POST** = create or change data, has side effects

---

## Exercise – Design endpoints for property deal tracking

| Method | Path | What it does |
|--------|------|--------------|
| GET | `/deals` | List all property deals |
| GET | `/deals/{id}` | Get one specific deal by ID |
| POST | `/deals` | Create a new property deal |
| DELETE | `/deals/{id}` | Remove a deal |

The data fields (price, location, size, borough) go **inside** the request body when creating a deal:

```json
{
  "price": 250000,
  "location": "Manchester",
  "size_sqft": 1200,
  "borough": "Salford"
}
```

**Key insight:** Endpoints = actions. Fields = data inside the request.

---

## Exercise – Reading API documentation

Using https://dummyjson.com/docs/products:

| Action | Endpoint | Method |
|--------|----------|--------|
| Get all products | `https://dummyjson.com/products` | GET |
| Get single product by ID | `https://dummyjson.com/products/1` | GET |

---

## Key insight for automation

Every Zapier trigger, n8n webhook, and integration calls an API endpoint. Understanding how endpoints are designed helps me:
- Read API documentation confidently
- Debug failing automations
- Know what's possible before building

When I connect two apps in an automation tool, I'm really just calling endpoints and passing data between them.
