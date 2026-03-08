# Comprehensive Guide to Web APIs

This document provides a consolidated overview of web APIs, from fundamental concepts to design principles and practical implementation details.

## 1. Core Concepts

### What is a Web Server?

A web server is a process running on a machine that listens for incoming HTTP requests on a specific IP address and port. When a request is received, the server processes it and sends back a response, which typically includes a status code and content (like an HTML page or JSON data).

-   **Common Web Servers**: Apache HTTP Server, Nginx, Caddy.
-   **Default Ports**: HTTP traffic uses port 80 by default, while HTTPS uses port 443.

When you type a URL like `www.example.com` into your browser:
1.  The domain name is translated into an IP address by a DNS (Domain Name System) server.
2.  The browser sends an HTTP request to that IP address on the appropriate port.
3.  The web server at that address receives the request, processes it, and sends back an HTTP response.
4.  Your browser renders the content from the response.

### API Layers

APIs are often structured in layers to separate concerns:

-   **HTTP/Controller Layer**: This is the entry point for third-party applications. It handles incoming requests and outgoing responses, authentication, validation, and caching. It contains the API routes and controller methods that orchestrate the execution of tasks.
-   **Business Logic/Domain Layer**: This is the core of the application, containing the business rules and logic. It's where services that implement specific business needs (e.g., adding a new customer, calculating a price) reside.

## 2. HTTP & URLS

### URL Structure

A URL (Uniform Resource Locator) is used to identify and locate a resource on the web. It has several parts:

`http://en.wikipedia.org:8000/w/index.php?title=Burrito#Breakfast_burrito`

-   **Scheme/Protocol**: `http`
-   **Domain Name (Host)**: `en.wikipedia.org`
-   **Port**: `8000`
-   **Path**: `/w/index.php`
-   **Parameters (Query String)**: `?title=Burrito`
-   **Anchor/Fragment**: `#Breakfast_burrito`

In the context of APIs, the URL is often referred to as a URI (Uniform Resource Identifier) that uniquely identifies a resource. For example: `https://adventure-works.com/orders/1`.

### HTTP Messages

Communication between a client and server happens through HTTP messages.

-   **HTTP Request**: Sent by the client to the server. It consists of:
    -   A URL (endpoint + parameters).
    -   An HTTP method (e.g., `GET`, `POST`).
    -   HTTP headers (metadata about the request).
    -   An optional request body (payload).
-   **HTTP Response**: Sent by the server to the client.

Example HTTP Request:
```http
POST /cgi-bin/process.cgi?tag=networking&order=newest HTTP/1.1
User-Agent: Mozilla/4.0 (compatible; MSIE5.01; Windows NT)
Host: www.tutorialspoint.com
Content-Type: text/xml; charset=utf-8
Content-Length: 60
Accept-Language: en-us
Accept-Encoding: gzip, deflate
Connection: Keep-Alive

first=Zara&last=Ali
```

## 3. Designing APIs: The REST Architectural Style

REST (Representational State Transfer) is a popular architectural style for web APIs defined by a set of constraints that result in a scalable, simple, and reliable system.

### REST Constraints

1.  **Client-Server**: The client and server are separate and act independently.
2.  **Stateless**: The server does not store any information about the client's state between requests. Every request must contain all the information needed to process it.
3.  **Cacheable**: The server's response should indicate whether the data is cacheable to improve performance.
4.  **Uniform Interface**: The client and server interact in a predictable way. A key aspect is the focus on "resources" (e.g., users, orders).
5.  **Layered System**: The application behaves the same whether the client is communicating directly with the server or through intermediaries (like a load balancer or proxy).

### Passing Information in Requests

Data can be passed from the client to the server in several ways:

-   **Path Parameters**: Used to identify a specific resource.
    -   Example: `/users/{id}` becomes `/users/123`.
-   **Query Parameters**: Used to filter or sort a collection of resources.
    -   Example: `/users?role=admin`
-   **Request Body (Payload)**: Used with `POST`, `PUT`, and `PATCH` requests to send data, typically in JSON or XML format.
-   **HTTP Headers**: Used to send metadata about the request, such as authentication tokens (`Authorization: Bearer <token>`).

**Best Practice**: Use path parameters to identify resources (`/cars/:id`) and query parameters to filter or sort them (`/cars?color=blue`).

### Handling Parameters on the Server (Node.js/Express Example)

On the server, you can access these parameters from the request object:
-   `req.params`: For path parameters (e.g., from `/users/:id`).
-   `req.query`: For query parameters (e.g., from `/users?id=123`).

### CRUD Actions and HTTP Methods

CRUD (Create, Read, Update, Delete) operations are mapped to HTTP methods:

-   **`POST`**: **C**reates a new resource. The response body typically contains a representation of the newly created resource.
-   **`GET`**: **R**eads (retrieves) a resource or a collection of resources.
-   **`PUT`**: **U**pdates an entire resource by replacing it. Can also be used to create a resource if it doesn't exist.
-   **`PATCH`**: **U**pdates a part of a resource.
-   **`DELETE`**: **D**eletes a resource.

## 4. Making API Requests (Client-Side)

### Using the `fetch` API

The modern `fetch` API provides an interface for making HTTP requests.

-   To handle JSON responses, use the `.json()` method on the response object.
-   To handle plain text, use the `.text()` method.
-   **Important**: The `response.json()` or `response.text()` method can only be called **once** on a response object. Consuming it more than once will result in an error.

```javascript
// Example: Fetching and parsing JSON
fetch('https://api.example.com/data')
  .then(response => {
    if (!response.ok) {
      throw new Error('Network response was not ok');
    }
    // The response is a ReadableStream. .json() parses it into a JavaScript object.
    return response.json();
  })
  .then(data => {
    console.log(data);
  })
  .catch(error => {
    console.error('Fetch error:', error);
  });
```

### Using jQuery AJAX

For older codebases, you might see jQuery used for API calls.

-   **`$.ajax()`**: A highly configurable method for making requests.
-   **`$.get()`**: A shorthand for making `GET` requests.
-   **`$.post()`**: A shorthand for making `POST` requests.

```javascript
// Example: $.get()
$.get("https://api.example.com/data", function(data, status){
  console.log("Data: " + data + "\nStatus: " + status);
});

// Example: $.ajax() with more options
$.ajax({
  url: "https://api.example.com/data",
  type: 'POST',
  data: { name: 'Mel' },
  dataType: 'json',
  success: function(response) {
    console.log('Success!', response);
  },
  error: function(xhr, status, error) {
    console.error('Error:', error);
  }
});
```

## 5. API-Related Technologies

### WebSockets

WebSockets provide a persistent, full-duplex communication channel between a client and a server over a single TCP connection. This is different from the request-response model of HTTP and is ideal for real-time applications like chat, live notifications, and collaborative editing, where the server needs to push data to the client without the client constantly polling for it.

### Swagger / OpenAPI Specification

Swagger is a set of tools built around the OpenAPI Specification, which is a standard way to describe and document RESTful APIs. You can write an API definition in a YAML or JSON file, which can then be used to:
-   Generate interactive API documentation.
-   Generate client and server code.
-   Create a mock server for testing.

---
*This document was created by consolidating notes from multiple files, including `ajax_api.md`, `CRUD-actions.md`, `http3.md`, `json-fetch.md`, `layers.md`, `params.md`, `REST.md`, `server-passing-info.md`, `swagger.md`, `url.md`, and `websockets.md`.*
