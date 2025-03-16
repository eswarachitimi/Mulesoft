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

#### _let’s define a GET method for fetching customer data_

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

#### _Define a reusable Customer type to enforce consistent data structure across endpoints_**

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

#### _Implement Security (Optional)_

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

#### _Sample RAML files-_

###### `customer-api.raml`

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

##### `books-api.raml`

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

### _Libraries vs Fragments -_

In RAML (RESTful API Modeling Language), libraries are reusable collections of `data types, resource types, traits, and security schemas`, while fragments are smaller, more specific units like `data types or traits`.

![image](https://github.com/user-attachments/assets/955dd091-ce10-4c77-8c02-d8b11d435af0)

A RAML library is a collection of the data type declaration, traits declaration, security scheme declaration, and resource type declaration into a modular and reusable group. It also allows you to define multiple types within the same library.

Fragments are basically used to externalize your security schemes, library, resource types, traits, data types, etc. They can be reused across any RAML. One of the characteristics of a fragment is that it can be published to Exchange, and it is possible to version your fragments. 

```
#%RAML 1.0
title: Baeldung Foo REST Services API
uses:
  mySecuritySchemes: !include libraries/security.raml
  myDataTypes: !include libraries/dataTypes.raml
  myResourceTypes: !include libraries/resourceTypes.raml
  myTraits: !include libraries/traits.raml
```

In API development, standardization is essential to ensure system maintenance and consistency. RAML (RESTful API Modeling Language) is a language that allows developers to model and document an API clearly and consistently. However, many developers face the challenge of repeating structures across projects, leading to inconsistencies, wasted time, and maintenance difficulties.

To address these issues, RAML fragments emerge as an efficient solution. These fragments are reusable components that allow developers to define common parts of their APIs once and reuse them in different contexts. 

#### DataType

A DataType is a definition that specifies the structure and constraints of data that can be used in APIs. DataTypes are used to define the input and output formats of an API’s data. The DataType defined in this fragment contains the error structure.

```
#%RAML 1.0 DataType
displayName: Common Response Error Format
description: The common response format used for all API Calls.
type: object
properties:
  code:
    type: string
    description: A unique code identifying the error.
    required: false
  message:
    type: string
    description: A message of the error.
    required: true
  correlationId:
    type: string
    description: A unique UUID for the request.
    required: true
  timestamp:
    type: datetime-only
    description: A timestamp identifying the time of the error.
    required: false
  details?:
    type: array
    items:
      type: object
      properties:
        code:
          type: string
          description: A unique code identifying the error.
          required: false
        message:
          type: string
          description: A message of the error.
          required: false
  additionalDetails:
    type: any
    required: false
```
#### Examples

Examples are used to provide concrete instances of data expected or returned by an API. The examples in this fragment include messages returned by APIKIT and the API itself.

```
{
    "code": "100200300",
    "message": "Required field 'name' missing.",
    "correlationId": "d449cf4e-987b-45bb-a56c-a386984ca50a",
    "timestamp": "2020-01-01T00:00:01",
    "details": [
        {
            "code": "100200300",
            "message": "Required field 'name' missing."
        }
    ],
    "additionalDetails": ""
}
```

#### Traits -

Traits are reusable definition blocks that can be applied to multiple resources and methods of an API to add common functionalities. They allow developers to define a series of properties, such as query parameters, headers, responses, and other aspects that can be shared by multiple resources and methods in the API. This promotes consistency, code reuse, and facilitates API maintenance.

The traits in this fragment are separated into errors, headers, queryParams, requests and responses.

#### Errors

The errors are divided into APIKIT errors and API errors. Below is an example of a trait containing the error structure returned by APIKIT.

```
#%RAML 1.0 Trait

responses: 
  400:
    description: Bad Request
    body: 
        application/json:
            type: !include ../../datatypes/responses/errors/error-type.raml
            example: !include ../../examples/responses/errors/bad-request.json
  404:
    description: Resource Not Found
    body: 
        application/json:
            type: !include ../../datatypes/responses/errors/error-type.raml
            example: !include ../../examples/responses/errors/resource-not-found.json
  405:
    description: Method Not Allowed
    body: 
        application/json:
            type: !include ../../datatypes/responses/errors/error-type.raml
            example: !include ../../examples/responses/errors/method-not-allowed.json
  406:
    description: Not Acceptable
    body: 
        application/json:
            type: !include ../../datatypes/responses/errors/error-type.raml
            example: !include ../../examples/responses/errors/not-acceptable.json
  415:
    description: Unsupported Media Type
    body: 
        application/json:
            type: !include ../../datatypes/responses/errors/error-type.raml
            example: !include ../../examples/responses/errors/unsuported-media-type.json
  501:
    description: Not Implemented
    body: 
        application/json:
            type: !include ../../datatypes/responses/errors/error-type.raml
            example: !include ../../examples/responses/errors/not-implemented.json
```

#### Headers

The headers contain the headers used between layers to maintain observability and those responded to in rate limit policies. The example below shows the header used between layers.

```
#%RAML 1.0 Trait
headers:
  x-correlation-id:
    description: A unique transaction id used to correlate api requests end to end.
    type: string
    required: true
    example: e393ef07-de7d-46c7-b514-27581be526d2
  x-source-system:
    type: string
    description: A unique identification string for the source system. This could be a system name or hostname where a system is hosted on multiple hosts.
    required: false
    example: "Salesforce Experience API"
```

#### QueryParams

The queryParams traits in this fragment are responsible for pagination and sorting. The next example shows the pagination trait.

```
#%RAML 1.0 Trait
usage: Apply this trait to a GET method that supports pagination.
queryParameters:
  offset:
    type: integer
    required: false
    default: 0
    minimum: 0
    description: Offset to start pagination search results.
  limit:
    type: integer
    required: false
    minimum: 1
    maximum: 1000
    description: The number of results per page.
```

#### Requests

The requests trait defines the content-type and data type, allowing the type to be passed via the ‘typeName’ variable. The request traits in this fragment include other examples, such as form-data requests, JSON with and without examples, and XML.

```
#%RAML 1.0 Trait
body:
  application/json:
    type: <<typeName>>
```

#### Responses

The responses trait has a structure similar to requests, enabling reuse through variables. The response traits in this fragment include other examples, such as JSON response 200, 201, 202 with and without examples, 204, and XML 200.

```
#%RAML 1.0 Trait

responses:
  200:
    body:
      application/json:
        type: <<typeName>>
```

#### ResourceTypes

There are four ResourceTypes in this fragment: three specific to each layer and one generic. The difference between them is that the specific ones are based on the generic, but have different security schemas and common headers between layers.

```
#%RAML 1.0 Library
usage: API RAML resource types

traits:
  hasCommonApikitErrorResponses: !include ../traits/errors/apikit-error-response.raml
  hasCommonInternalServerErrorResponses: !include ../traits/errors/internal-server-error-response.raml

resourceTypes: 
  collection:
    usage: Use this resourceType to represent any collection
    description: A collection of <<resourcePathName|!uppercamelcase>>
    get?:
      description: Get a new <<resourcePathName|!uppercamelcase|!singularize>>
      is: 
          - hasCommonApikitErrorResponses
          - hasCommonInternalServerErrorResponses
    post?:
        description: Create a new <<resourcePathName|!uppercamelcase|!singularize>>
        is: 
            - hasCommonApikitErrorResponses
            - hasCommonInternalServerErrorResponses
    put?:
        description: Update a new <<resourcePathName|!uppercamelcase|!singularize>>
        is: 
            - hasCommonApikitErrorResponses
            - hasCommonInternalServerErrorResponses
    patch?:
        description: Update parcial a new <<resourcePathName|!uppercamelcase|!singularize>>
        is: 
            - hasCommonApikitErrorResponses
            - hasCommonInternalServerErrorResponses
    delete?:
        description: Delete a new <<resourcePathName|!uppercamelcase|!singularize>>
        is: 
            - hasCommonApikitErrorResponses
            - hasCommonInternalServerErrorResponses
```

RAML fragments are powerful tools that help standardize and reuse common components in APIs. They promote consistency, reduce code duplication, and facilitate API maintenance and updates. By using commonly used RAML fragments, developers can ensure their APIs are more robust and easier to manage. 

### ResourceTypes

ResourceTypes are like resources in that they can specify descriptions, methods, and parameters. A resource that uses resourceTypes can inherit its nodes. ResourceTypes can use and inherit from other resourceTypes.

A ResourceType is basically a template that is used to define the descriptions, methods, and parameters that can be used by multiple resources without writing duplicate code. 


![image](https://github.com/user-attachments/assets/ff388fce-a915-4829-9126-9e07555e3d6c)
