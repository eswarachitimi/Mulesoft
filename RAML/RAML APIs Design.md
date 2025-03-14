RAML (RESTful API Modeling Language) is a widely used, human-readable language for designing RESTful APIs in MuleSoft. RAML enables developers to define API endpoints, methods, request/response payloads, and security in a structured format. This makes it easy to design, document, and manage APIs effectively.

### _What is RAML?_

RAML is a language that simplifies the process of designing APIs by providing a clear, structured format. With RAML, you can define:

- Endpoints and HTTP Methods
- Query parameters and headers
- Request and response bodies
- Data types and schemas
- Security configurations, such as OAuth

RAML is part of MuleSoft’s API-first approach, which emphasizes defining and designing APIs before implementing them. This approach ensures that APIs are consistent, reusable, and easy to manage.

### _Why Use RAML in MuleSoft?_

- **Standardized API Design:** RAML offers a consistent format that allows developers to understand and collaborate on API design.
- **Documentation:** RAML serves as both an API blueprint and documentation, making it easier for developers and stakeholders to understand API functionality.
- **Reusability:** RAML allows you to reuse data types, endpoints, and security settings across multiple APIs.
- **Compatibility with MuleSoft:** Anypoint Platform supports RAML, enabling you to import RAML files directly into Mule projects.

### _Define the API Basics_

Basic metadata for your RAML API.

```
#%RAML 1.0
title: Customer API
version: v1
baseUri: https://api.example.com/{version}
mediaType: application/json
```

- **title:** A friendly name for the API.
- **version:** The API version, which can be referenced throughout the RAML file.
- **baseUri:** The base URI of the API, using `{version}` to represent the version number dynamically.
- **mediaType:** Sets the default media type for requests and responses.

### _let’s define a GET method for fetching customer data_

```
/customers:
  get:
    description: Retrieve a list of customers
    responses:
      200:
        body:
          application/json:
            type: Customer[]
            example: |
              [
                {
                  "id": "1",
                  "name": "John Doe",
                  "email": "john.doe@example.com"
                },
                {
                  "id": "2",
                  "name": "Jane Smith",
                  "email": "jane.smith@example.com"
                }
              ]
      400:
        description: Bad request
      500:
        description: Internal server error
```

- **/customers:** This path represents the API endpoint for accessing customer data.
- **GET:** Defines the GET method to retrieve customer data.
- **responses:** Lists the expected response codes and body formats.
- **200:** Success response with an example JSON array of customers.
- **400:** Error code for bad requests.
- **500:** Error code for server errors.

**_Define a reusable Customer type to enforce consistent data structure across endpoints_**

```
types:
  Customer:
    type: object
    properties:
      id:
        type: string
        description: Unique identifier for the customer
      name:
        type: string
        required: true
        description: Full name of the customer
      email:
        type: string
        required: true
        description: Customer's email address
```

- **types:** This section defines reusable types within the RAML file.
- **Customer:** Defines an object structure for customer data, including `id`, `name`, and `email`.
- **required: true:** Specifies that `name` and `email` are required fields for a valid customer object.

### _Implement Security (Optional)_

If your API requires authentication, you can add security schemes. Here’s an example using OAuth 2.0:

```
securitySchemes:
  oauth_2_0:
    description: OAuth 2.0 Authentication
    type: OAuth 2.0
    describedBy:
      headers:
        Authorization:
          description: Access token for the API
          type: string
      responses:
        401:
          description: Unauthorized access
    settings:
      authorizationUri: https://auth.example.com/oauth/authorize
      accessTokenUri: https://auth.example.com/oauth/token
      authorizationGrants: [ authorization_code ]
```

- **securitySchemes:** Defines available security configurations for the API.
- **OAuth 2.0:** Configures OAuth 2.0 as the security method, with endpoints for obtaining authorization tokens.

### _RAML file for Customer API -_

### `customer-api.raml`
```
#%RAML 1.0
title: Customer API
version: v1
baseUri: https://api.example.com/{version}
mediaType: application/json

types:
  Customer:
    type: object
    properties:
      id:
        type: string
      name:
        type: string
        required: true
      email:
        type: string
        required: true
/customers:
  get:
    description: Retrieve a list of customers
    responses:
      200:
        body:
          application/json:
            type: Customer[]
            example: |
              [
                {
                  "id": "1",
                  "name": "John Doe",
                  "email": "john.doe@example.com"
                },
                {
                  "id": "2",
                  "name": "Jane Smith",
                  "email": "jane.smith@example.com"
                }
              ]
      400:
        description: Bad request
      500:
        description: Internal server error
  post:
    description: Add a new customer
    body:
      application/json:
        type: Customer
        example: |
          {
            "name": "Alice Brown",
            "email": "alice.brown@example.com"
          }
    responses:
      201:
        description: Customer created successfully
      400:
        description: Bad request
      500:
        description: Internal server error
```

### `books-api.raml`

```
#%RAML 1.0
title: Book Store API
version: v1
baseUri: http://api.bookstore.com/v1

types:
  Book:
    type: object
    properties:
      id: string
      title: string
      author: string
      publishedDate: date-only
      isbn: string
      summary: string
    example: |
      {
        "id": "1",
        "title": "Moby Dick",
        "author": "Herman Melville",
        "publishedDate": "1851-10-18",
        "isbn": "978-1234567890",
        "summary": "Story of a ship captain's quest for revenge."
      }
    schema: |
      {
        "$schema": "http://json-schema.org/draft-07/schema#",
        "type": "object",
        "properties": {
          "id": {"type": "string"},
          "title": {"type": "string"},
          "author": {"type": "string"},
          "publishedDate": {"type": "string", "format": "date"},
          "isbn": {"type": "string"},
          "summary": {"type": "string"}
        },
        "required": ["id", "title", "author", "publishedDate", "isbn", "summary"]
      }

/books:
  get:
    description: Retrieve a list of books.
    queryParameters:
      author:
        description: Filter books by author name.
        type: string
      publishedBefore:
        description: Filter books published before a certain date.
        type: date-only
    responses:
      200:
        body:
          application/json:
            type: Book[]
            example: |
              [
                {
                  "id": "1",
                  "title": "Moby Dick",
                  "author": "Herman Melville",
                  "publishedDate": "1851-10-18",
                  "isbn": "978-1234567890",
                  "summary": "Story of a ship captain's quest for revenge."
                }
              ]
  post:
    description: Add a new book.
    body:
      application/json:
        type: Book
        example: |
          {
            "title": "Pride and Prejudice",
            "author": "Jane Austen",
            "publishedDate": "1813-01-28",
            "isbn": "978-0987654321",
            "summary": "A tale of love and manners set in early 19th century England."
          }
    responses:
      201:
        body:
          application/json:
            type: Book
            example: |
              {
                "id": "2",
                "title": "Pride and Prejudice",
                "author": "Jane Austen",
                "publishedDate": "1813-01-28",
                "isbn": "978-0987654321",
                "summary": "A tale of love and manners set in early 19th century England."
              }

  /{bookId}:
    get:
      description: Retrieve a specific book by ID.
      responses:
        200:
          body:
            application/json:
              type: Book
              example: |
                {
                  "id": "1",
                  "title": "Moby Dick",
                  "author": "Herman Melville",
                  "publishedDate": "1851-10-18",
                  "isbn": "978-1234567890",
                  "summary": "Story of a ship captain's quest for revenge."
                }
        404:
          description: Book not found.
    delete:
      description: Delete a specific book by ID.
      responses:
        204:
          description: Book successfully deleted.
        404:
          description: Book not found.
````

- **Metadata:** The RAML starts with metadata that defines the version of RAML, the title, version, and base URI of the API.
- **Types:** This section defines the data structures used in the API. In this case, we’ve defined a Book type.
- **Resources:** The `/books` and `/books/{bookId}` are resources. Each resource can have multiple HTTP methods (get, post, delete, etc.).
- **Query Parameters:** The get method under `/books` accepts query parameters to filter books by author and publishedBefore.
- **Responses:** Each HTTP method has potential responses. For example, the get method can return a 200 OK response with a list of books, and the post method can return a 201 Created response with the created book’s details.
- **URI Parameters:** The `/books/{bookId}` resource uses a URI parameter `{bookId}` to represent a specific book ID.
