# GraphQL_Setup
🔑 GraphQL vs REST API

1. Data Fetching

REST API:
Each endpoint returns a fixed structure of data.
You may over-fetch (get more fields than needed) or under-fetch (need multiple requests).
Example: /users/1 → returns all user details even if you just need the name.

GraphQL:
Client specifies exactly what fields it needs in the query.
One request can fetch related data (nested).

Example:

{
user(id: 1) {
name
email
posts {
title
}
}
}


→ returns only requested fields.

2. Endpoints

REST API: Multiple endpoints (/users, /posts, /comments).
GraphQL: Single endpoint (/graphql) for all queries and mutations.

3. Request Types

REST API: Uses HTTP methods (GET, POST, PUT, DELETE) to define the action.
GraphQL: Uses queries (for fetching), mutations (for write/update), and subscriptions (for real-time updates).

4. Flexibility

REST API: Rigid, server defines what the response looks like.
GraphQL: Flexible, client defines what data it needs.

5. Performance

REST API: Can lead to over-fetching or multiple round trips.
GraphQL: Reduces network calls by batching related data in one request.

6. Versioning

REST API: Often requires versioning (/api/v1/users, /api/v2/users) when response changes.
GraphQL: Avoids versioning, clients just query new fields as schema evolves.

7. Error Handling

REST API: Based on HTTP status codes (e.g., 404, 500).
GraphQL: Returns data + error object together in JSON.



Who Controls the Shape of Data?

REST API:
The server developer decides what the endpoint returns.
Even if you make models on the client side, the server must still expose endpoints (or parameters) that match those models.
Example: /users/1 always returns full user data unless server creates a "lightweight" endpoint like /users/1?fields=name,email.

GraphQL:
The client decides the data shape dynamically at runtime.
No need for server to create multiple versions of the same endpoint.

Example:

{
user(id: 1) {
name
email
}
}

and later you can ask for

{
user(id: 1) {
name
posts { title }
}
}

— without changing backend.

✅ In short:

Use REST when your API is simple, caching is critical, and predictable responses are enough.
Use GraphQL when you need flexible queries, reduce network calls, and want clients to control what data they receive.