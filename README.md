# ALX Project 0x14 - MoviesDatabase API

![MoviesDatabase API Banner](https://via.placeholder.com/800x200?text=MoviesDatabase+API)  
_A TypeScript project for interacting with the MoviesDatabase API_

---

## Table of Contents

- [API Overview](#api-overview)
- [Endpoints](#endpoints)
- [Authentication](#authentication)
- [Request/Response Examples](#requestresponse-examples)
- [Error Handling](#error-handling)
- [Rate Limits](#rate-limits)
- [Setup Instructions](#setup-instructions)

---

## API Overview

The MoviesDatabase API provides:

- 🎬 **9+ million titles** (movies, TV shows, episodes)
- 🎥 **11+ million actor/crew records**
- 📅 Weekly updates for new content
- ⭐ Daily rating updates

Key features:

- Search by title, keyword, or actor
- Get detailed metadata (ratings, cast, trailers)
- Filter by genre, year, or popularity

---

## Endpoints

### Titles

| Endpoint                 | Description       | Parameters               |
| ------------------------ | ----------------- | ------------------------ |
| `GET /titles`            | List titles       | `limit`, `genre`, `year` |
| `GET /titles/{id}`       | Title details     | `info=base_info`         |
| `GET /titles/x/upcoming` | Upcoming releases | `limit=10`               |

### Search

| Endpoint                             | Description       |
| ------------------------------------ | ----------------- |
| `GET /titles/search/keyword/{query}` | Search by keyword |
| `GET /titles/search/title/{query}`   | Search by title   |

---

## Authentication

```http
GET /titles/tt123456 HTTP/1.1
Authorization: Bearer YOUR_API_KEY
Accept: application/json

MOVIESDB_API_KEY=your_key_here

## Authentication
Request:
const response = await fetch('https://api.moviesdatabase.com/titles/tt0111161', {
  headers: {
    'Authorization': `Bearer ${process.env.MOVIESDB_API_KEY}`
  }
});

Successful Response:

json
{
  "id": "tt0111161",
  "title": "The Shawshank Redemption",
  "year": 1994,
  "rating": 9.3,
  "genres": ["Drama"]
}
```

## Error Handling

Code Meaning Solution
401 Unauthorized Check API key
404 Not Found Verify title ID
429 Too Many Requests Wait 1 hour
Error Response:

json
{
"error": "Title not found",
"status": 404
}

## Usage Limits and Best Practices

Usage Limits and Best Practices
Rate Limits
Tier Requests
Free 100/hour
Paid 10,000/hour
Best Practices
✅ Cache API responses

typescript
// Example: Cache for 1 hour
import { cache } from 'react';
export const getMovie = cache(fetchMovie);
✅ Implement pagination

http
GET /titles?limit=20&page=2
✅ Handle errors gracefully

typescript
try {
const data = await fetchMovie("tt123");
} catch (error) {
if (error.status === 429) {
await new Promise(resolve => setTimeout(resolve, 2000)); // Retry after delay
}
}
❌ Never expose API keys

env

# GOOD (in .env):

MOVIESDB_API_KEY=your_key

# BAD (in code):

const apiKey = "123abc";
✅ Validate responses

typescript
interface Movie {
id: string;
title: string;
year?: number; // Optional field
}
Setup Instructions
Install dependencies:

bash

npm install axios typescript @types/node

##Run the project:

bash

npm run dev
