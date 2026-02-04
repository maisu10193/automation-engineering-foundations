# Day 04 – JSON and Data Transformation

## What I studied

Today I studied JSON fundamentals using:
- "JSON Crash Course" by Traversy Media (https://www.youtube.com/watch?v=GpOO5iKzOmY)
- W3Schools JSON introduction (https://www.w3schools.com/js/js_json_intro.asp)

---

## What I learned (theory)

### What is JSON?

JSON (JavaScript Object Notation) is a lightweight data format used by APIs to send and receive data. It's:
- Human-readable
- Language-independent (works with Python, JavaScript, etc.)
- Structured and predictable

### JSON syntax rules

- Keys must be in double quotes: `"name"`
- Strings must be in double quotes: `"value"`
- No trailing commas after the last item
- Booleans are `true` / `false` (lowercase, no quotes)
- Numbers don't have quotes (but phone numbers should be strings because of leading zeros)
- Use `:` not `=` for key-value pairs

### Objects vs Arrays

| | Object `{}` | Array `[]` |
|---|-------------|------------|
| Access by | Key name (`deal.price`) | Index number (`contacts[0]`) |
| Use for | Named properties | Lists of similar items |
| Order | Not guaranteed | Guaranteed |

Objects can contain arrays, and arrays can contain objects:

```json
{
  "contacts": [
    {"name": "James"},
    {"name": "Priya"}
  ]
}
```

---

## Exercise – Fix broken JSON

Original (5 errors):
```json
{
  name: "Manchester Office
  "price": 450000,
  "available": yes,
  "features": ["parking", "lift", "reception",]
  "contact": {
    "name": "Sarah",
    "phone": 07123456789
  }
}
```

Corrected:
```json
{
  "name": "Manchester Office",
  "price": 450000,
  "available": true,
  "features": ["parking", "lift", "reception"],
  "contact": {
    "name": "Sarah",
    "phone": "07123456789"
  }
}
```

Errors fixed:
1. Added quotes around `name` key
2. Closed the string `"Manchester Office"`
3. Changed `yes` to `true`
4. Removed trailing comma after `"reception"`
5. Changed phone number to string (leading zero would be lost otherwise)

---

## Exercise – Read and extract data

Given this JSON:
```json
{
  "deal": {
    "id": 42,
    "title": "Retail Unit - Leeds",
    "price": 320000,
    "status": "available",
    "location": {
      "city": "Leeds",
      "postcode": "LS1 4AP",
      "coordinates": {
        "lat": 53.7965,
        "lng": -1.5478
      }
    },
    "contacts": [
      {"name": "James", "role": "agent", "email": "james@example.com"},
      {"name": "Priya", "role": "vendor", "email": "priya@example.com"}
    ]
  }
}
```

Answers:
- `deal.price` → 320000
- `deal.location.postcode` → "LS1 4AP"
- `deal.location.coordinates.lat` → 53.7965
- Number of contacts → 2
- Email of vendor → "priya@example.com" (accessed via `deal.contacts[1].email`)

**Key lesson:** Always use exact values including correct case. `"LS1 4AP"` ≠ `"ls1 4ap"` — case sensitivity can break automations.

---

## Exercise – Transform data between systems

System A sends:
```json
{
  "property_name": "High Street Shop",
  "asking_price_gbp": 275000,
  "city_name": "Birmingham",
  "owner_full_name": "David Chen",
  "owner_email_address": "david@email.com"
}
```

System B requires:
```json
{
  "title": "High Street Shop",
  "price": 275000,
  "location": {
    "city": "Birmingham"
  },
  "contact": {
    "name": "David Chen",
    "email": "david@email.com"
  }
}
```

Field mapping:
- `property_name` → `title`
- `asking_price_gbp` → `price`
- `city_name` → `location.city`
- `owner_full_name` → `contact.name`
- `owner_email_address` → `contact.email`

This is exactly what happens inside Zapier/n8n when mapping fields — transforming JSON from one shape to another.

---

## Exercise – Design JSON for property deal system

```json
{
  "title": "Nursery - Freehold",
  "price": 450000,
  "status": "vacant",
  "property_type": "D1/E",
  "size_sqft": 2800,
  "location": {
    "city": "Manchester",
    "postcode": "M33 4AB",
    "borough": "Trafford"
  },
  "contacts": [
    {
      "name": "Sarah Mills",
      "role": "agent",
      "email": "sarah@agency.com",
      "phone": "07123456789"
    },
    {
      "name": "James Wilson",
      "role": "vendor",
      "email": "james@email.com"
    }
  ],
  "features": ["parking", "separate entrance", "DDA compliant"],
  "source": "Rightmove",
  "added_date": "2025-02-04"
}
```

---

## Reflection

**Why do APIs use JSON instead of plain text?**
JSON has structure, making it predictable and easy to extract exact data. Machines can parse it reliably.

**What's the difference between an object and an array?**
- Object `{}`: access by key name, used for named properties
- Array `[]`: access by index number, used for lists of similar items

**Why does nested data matter for automation?**
When connecting systems, I need to point to the exact layer to get the data I need. Understanding paths like `deal.location.coordinates.lat` or `deal.contacts[0].email` is essential for mapping fields correctly.

---

## Key insight for automation

Every time I connect two apps in Zapier or n8n, I'm transforming JSON from one shape to another. Common issues:
- Phone numbers losing leading zeros (store as strings)
- Case sensitivity breaking matches
- Nested data requiring correct path notation
- Arrays needing index numbers to access specific items

Understanding JSON structure is fundamental to debugging when data doesn't arrive as expected.
