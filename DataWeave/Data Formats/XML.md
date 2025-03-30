### What is XML?

 XML `Extensible Markup Language`, is a markup language designed to store and transport data, allowing for structured and flexible data representation and exchange between systems. 

> **MIME type (or) Media Type (or) Content-Type:** application/xml

> **File Name:** <File_Name>.xml

> **XML Editor:** https://jsonformatter.org/xml-formatter

- **Purpose:** XML is used to describe data, not to display it like HTML, and is designed for structured data storage and exchange, facilitating data sharing between different applications and systems.
- **Flexibility:** XML allows you to create custom tags to define your own data structures, making it highly adaptable to various data formats and applications. 
- While both XML and JSON are used for data exchange, JSON is generally considered simpler and more lightweight than XML.

#### Sample XML Message Explanation

![image](https://github.com/user-attachments/assets/5f27a34a-5990-48d7-9942-462be0a63ad4)

- The XML prolog is optional. If it exists, it must come first in the document.A prolog defines the XML version and the character encoding `<?xml version="1.0" encoding="UTF-8"?>`. 
- XML documents must contain one root element that is the parent of all other elements
- The next line is the root element of the document `<bookstore>`
- The next line starts a <book> element `<book category="cooking">`
- The `<book>` elements have 4 child elements: `<title>, <author>, <year>, <price>`.
- The next line ends the book element `</book>`. In XML, it is illegal to omit the closing tag. All elements must have a closing tag.

> Note: The XML prolog does not have a closing tag! This is not an error. The prolog is not a part of the XML document.

> XML tags are case sensitive. The tag `<Book>` is different from the tag `<book>`. Opening and closing tags must be written with the same case.

> In XML, all elements must be properly nested within each other

- You can assume, from this example, that the XML document contains information about books in a bookstore.
  
> **Sample Example -**

```
<?xml version="1.0" encoding="UTF-8"?>
<bookstore>
  <book category="cooking">
    <title lang="en">Everyday Italian</title>
    <author>Giada De Laurentiis</author>
    <year>2005</year>
    <price>30.00</price>
  </book>
  <book category="children">
    <title lang="en">Harry Potter</title>
    <author>J K. Rowling</author>
    <year>2005</year>
    <price>29.99</price>
  </book>
  <book category="web">
    <title lang="en">Learning XML</title>
    <author>Erik T. Ray</author>
    <year>2003</year>
    <price>39.95</price>
  </book>
</bookstore>
```

### Key Features:

- **Data Structure:** XML uses a tree-like structure with elements, attributes, and text content to organize data.
- **Human and Machine Readable:** XML is designed to be both human-readable and machine-readable, allowing for easy data interpretation and processing.
- **Standardized Syntax:** XML has a standardized syntax, ensuring that data can be parsed and interpreted correctly across different systems and platforms.
   
### Uses:

XML is used in various applications, including:

- **Data Interchange:** Sharing data between different applications, databases, and systems.
- **Web Services:** Facilitating communication and data exchange between web services.
- **E-commerce:** Storing and exchanging product information and transaction data.
- **Document Formats:** Storing documents and other data in a structured format (e.g., Microsoft Office formats like .docx, .xlsx, .pptx).
- **Configuration Files:** Storing application settings and configurations. 

### XML Namespaces

XML Namespaces provide a method to avoid element name conflicts.

#### Name Conflicts

In XML, element names are defined by the developer. This often results in a conflict when trying to mix XML documents from different XML applications.

This XML carries HTML table information:

```
<table>
  <tr>
    <td>Apples</td>
    <td>Bananas</td>
  </tr>
</table>
```

This XML carries information about a table (a piece of furniture):

```
<table>
  <name>African Coffee Table</name>
  <width>80</width>
  <length>120</length>
</table>
```

If these XML fragments were added together, there would be a name conflict. Both contain a `<table>` element, but the elements have different content and meaning.

A user or an XML application will not know how to handle these differences.

#### Solving the Name Conflict Using a Prefix

Name conflicts in XML can easily be avoided using a name prefix.

This XML carries information about an HTML table, and a piece of furniture:

```
<h:table>
  <h:tr>
    <h:td>Apples</h:td>
    <h:td>Bananas</h:td>
  </h:tr>
</h:table>

<f:table>
  <f:name>African Coffee Table</f:name>
  <f:width>80</f:width>
  <f:length>120</f:length>
</f:table>
```

In the example above, there will be no conflict because the two <table> elements have different names.

#### XML Namespaces - The xmlns Attribute

When using prefixes in XML, a namespace for the prefix must be defined.

The namespace can be defined by an `xmlns` attribute in the start tag of an element.

The namespace declaration has the following syntax. `xmlns:prefix="URI"`.

```
<root>
<h:table xmlns:h="http://www.w3.org/TR/html4/">
  <h:tr>
    <h:td>Apples</h:td>
    <h:td>Bananas</h:td>
  </h:tr>
</h:table>
<f:table xmlns:f="https://www.w3schools.com/furniture">
  <f:name>African Coffee Table</f:name>
  <f:width>80</f:width>
  <f:length>120</f:length>
</f:table>
</root>
```

In the example above:

- The xmlns attribute in the `first <table> element` gives the `h: prefix` a qualified namespace.
- The xmlns attribute in the `second <table> element` gives the `f: prefix` a qualified namespace.
- When a namespace is defined for an element, all child elements with the same prefix are associated with the same namespace.

Namespaces can also be declared in the XML root element:

```
<root xmlns:h="http://www.w3.org/TR/html4/"
xmlns:f="https://www.w3schools.com/furniture">
<h:table>
  <h:tr>
    <h:td>Apples</h:td>
    <h:td>Bananas</h:td>
  </h:tr>
</h:table>
<f:table>
  <f:name>African Coffee Table</f:name>
  <f:width>80</f:width>
  <f:length>120</f:length>
</f:table>
</root>
```

> Note: The namespace URI - `Uniform Resource Identifier` is not used by the parser to look up information.

The purpose of using an URI is to give the namespace a unique name. However, companies often use the namespace as a pointer to a web page containing namespace information.

### WSDL

WSDL, or `Web Services Description Language`, is an XML-based language used to describe the functionality of a web service. acting as a contract between the service provider and the service consumer, outlining operations, input/output formats, and protocols. 

##### Key Elements:

A WSDL document typically includes sections for:

- `types:` Defines the data types used by the web service (using XML Schema).
- `message:` Defines the structure of the messages exchanged between the client and the service.
- `portType:` Describes the operations that the service offers and the messages they use.
- `binding:` Specifies the protocol and data format used to communicate with the service (e.g., SOAP over HTTP).
- `service:` Defines the endpoints (ports) where the service can be accessed. 

##### Relationship to SOAP:

While WSDL is not limited to SOAP, it's commonly used with SOAP-based web services, as SOAP is a messaging protocol that WSDL can describe. 

##### WSDL 2.0:

Version 2.0 of WSDL provides a more flexible and extensible model for describing web services.

##### Tools:

Tools like SoapUI can utilize WSDL files to generate test requests, assertions, and mock services for testing SOAP-based services. 

https://www.tutorialspoint.com/wsdl/wsdl_introduction.htm

### SOAP XML

SOAP -  `Simple Object Access Protocol` is a messaging protocol that uses XML to format messages for exchanging data between applications. 
It's a standard for building web services, allowing applications to communicate and interact with each other, even if they are on different platforms. 
SOAP messages are typically sent over HTTP, but other protocols can also be used. 

##### SOAP Message Structure: 

A SOAP message is an XML document with a specific structure:

- `<Envelope>:` The root element of the SOAP message.
- `<Header> (optional):` Contains information for processing the message along the way.
- `<Body> (mandatory):` Contains the actual data being transmitted, including the request or response.
- `<Fault> (optional):` Used to report errors that occur during processing. 

![image](https://github.com/user-attachments/assets/dba96a1a-07aa-4756-a990-b901636eb273)

##### How SOAP Works:

- A client application sends a SOAP request (an XML document) to a server application.
- The request contains information about the method to be called and the parameters to be passed.
- The server application processes the request and sends back a SOAP response (another XML document) containing the results.
  
##### SOAP vs. REST:

- REST (Representational State Transfer) is another popular protocol for building web services.
- While SOAP uses XML for message formatting, REST is more flexible and supports various data formats, including XML, JSON, and plain text.
- SOAP is often considered more suitable for complex, enterprise-level applications, while REST is often preferred for simpler web services. 

https://www.w3schools.com/xml/xml_soap.asp

### XML and XPATH

https://www.w3schools.com/xml/xpath_intro.asp

### XML Schema

https://www.w3schools.com/xml/schema_intro.asp

### XML DOM

https://www.w3schools.com/xml/dom_intro.asp
