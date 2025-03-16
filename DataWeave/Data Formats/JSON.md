JSON (JavaScript Object Notation) is a standard, text-based format for storing and exchanging data easily. It is widely-used in APIs, configuration files, and data exchange between servers and clients. JSON (JavaScript Object Notation) and XML (eXtensible Markup Language) are popular formats for data representation.It's commonly used for web development, data analysis, and software engineering. 

> **JSON Editor** https://jsoneditoronline.org/

### Features

**_Human-readable:_** JSON is easy for people to read and understand. 

**_Machine-parsable:_** JSON is easy for computers to understand and process. 

**_Language-independent:_** JSON can be used to exchange data between different programming languages and platforms. While it is derived from JavaScript, JSON is supported by many programming languages including Python, Java, PHP, and more.

**_Lightweight:_** JSON is a simple format that's easy to learn and troubleshoot. 

**_Data structure:_** It represents data as objects, arrays, strings, numbers, booleans, and null.

### Use cases 

- Transferring data between a server and a web application/mobile application.
- Storing unstructured data in log files or NoSQL databases

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
