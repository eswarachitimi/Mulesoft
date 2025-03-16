### What is JSON?

JSON stands for `JavaScript Object Notation` and is a lightweight, text-based data format designed for easy data exchange.

- JSON is widely used to transmit data between a server and a client as part of a web API request/response. Also used in APIs, configuration files, web development, data analysis, and software engineering. 
- JSON (JavaScript Object Notation) and XML (eXtensible Markup Language) are popular formats for data representation.

> **MIME type (or) Media Type:** application/json

> **File Name:** <file_name>.json

> **JSON Editor** https://jsoneditoronline.org/

### Features

- **_Human-readable:_** JSON is easy for people to read and understand.
- **_Machine-parsable:_** JSON is easy for computers to understand and process.
- **_Language-independent:_** JSON can be used to exchange data between different programming languages and platforms. While it is derived from JavaScript, JSON is supported by many programming languages including Python, Java, PHP, and more.
- **_Lightweight:_** JSON is a simple format that's easy to learn and troubleshoot.
- **_Data structure:_** It represents data as objects, arrays, strings, numbers, booleans, and null.

### Use cases 

- Transferring data between a server and a web application/mobile application.
- Storing unstructured data in log files or NoSQL databases ( e.g., Mongo DB ).

### Data types 

**Number:** Integer or floating-point numbers, e.g., 10, 3.14.

**String:**  A sequence of characters, e.g., "hello".

**Boolean:** A value representing true or false.

**Array:** An ordered list of zero or more elements, e.g.,  [] (or) [ 1, 2, 3 ] (or) ["eswara", "rama", "krishna"]

**Object:** A collection of key-value pairs, e.g., {} (or) { "a": "b", "c": "d" }

**null:** An empty value

### JSON Structure

```
{
  "array": [
    1,
    2,
    3
  ],
  "boolean": true,
  "color": "gold",
  "null": null,
  "number": 123,
  "object": {
    "a": "b",
    "c": "d"
  },
  "string": "Hello World"
}
```

The basic structure of JSON consists of two primary components:
  
#### Objects

A JSON object is a collection of key-value pairs enclosed in curly braces {}. The key is always a string, and the value can be a variety of data types, including strings, numbers,arrays and even other objects.

**_Example:_**

```
{
    "name": "Mohit Kumar",
    "age": 30,
    "isStudent": false
}
```

> In this example, name, age, and isStudent are keys, and "Mohit Kumar", 30, and false are their respective values.

#### Arrays

A JSON array is an ordered collection of values enclosed in square brackets []. These values can be of any type, including objects, arrays, or primitive data types.

**_Example:_**

```
{
    "fruits": ["apple", "banana", "cherry"]
}
```

> Here, fruits is a key, and the value is an array containing the elements "apple", "banana", and "cherry".

### Comments in JSON

JSON file with comments (using // for single-line comments).

```
{
    // This is a comment
    "name": "John Doe",
    // The user's age
    "age": 30,
    // The user's email
    "email": "john.doe@example.com"
}
```

Another common approach is to include comments as part of the JSON data itself.This way, the comments are treated as regular key-value pairs.

```
{
    "_comment": "This JSON file contains user data",
    "name": "John Doe",
    "age": 30,
    "email": "john.doe@example.com",
    "address": {
        "_comment": "Address details",
        "street": "123 Main St",
        "city": "Anytown"
    }
}
```

