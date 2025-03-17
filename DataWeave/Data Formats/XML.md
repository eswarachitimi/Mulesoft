### What is XML?

 XML `Extensible Markup Language`, is a markup language designed to store and transport data, allowing for structured and flexible data representation and exchange between systems. 

> **MIME type (or) Media Type (or) Content-Type:** application/xml

> **File Name:** <File_Name>.xml

> **XML Editor:** https://jsonformatter.org/xml-formatter

- **Purpose:** XML is used to describe data, not to display it like HTML, and is designed for structured data storage and exchange, facilitating data sharing between different applications and systems.
- **Flexibility:** XML allows you to create custom tags to define your own data structures, making it highly adaptable to various data formats and applications. 
- While both XML and JSON are used for data exchange, JSON is generally considered simpler and more lightweight than XML.

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

If these XML fragments were added together, there would be a name conflict. Both contain a <table> element, but the elements have different content and meaning.

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

https://www.w3schools.com/xml/xml_wsdl.asp

### SOAP XML

https://www.w3schools.com/xml/xml_soap.asp

### XML and XPATH

https://www.w3schools.com/xml/xpath_intro.asp

### XML Schema

https://www.w3schools.com/xml/schema_intro.asp

### XML DOM

https://www.w3schools.com/xml/dom_intro.asp
