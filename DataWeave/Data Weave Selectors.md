# Selectors

- DataWeave selectors traverse the structures of objects and arrays and return matching values.
- DataWeave selectors allow navigating any combination of Objects and Arrays to get to the data you need. 

![image](https://github.com/user-attachments/assets/a99ff0c6-b866-4cc0-bf5a-d1f727a6e7fc)

![image](https://github.com/user-attachments/assets/0ff484c8-79dd-4518-9736-f2a6fe6585e5)

![image](https://github.com/user-attachments/assets/0f331e96-9c81-453f-baa4-0910043f9a12)

### Reading XML in Data Weave

<img width="1906" height="887" alt="image" src="https://github.com/user-attachments/assets/604715f4-96cc-44a8-8ac4-5fb8f511e93f" />

### XML Name space & attribute Vlaue Selector Examples

A namespace helps to avoid naming conflicts when an XML document combines elements or attributes from different XML vocabularies or schemas.

A namespace is declared using the xmlns attribute, optionally with a `prefix`, and assigned a unique URI. Prefixed Namespace Declaration.

```
    <root xmlns:prefix="http://example.com/namespaceURI">
        <prefix:elementName>...</prefix:elementName>
    </root>
 ```

In XML, attributes are used to add metadata to elements. For example, in `<book category="fiction">`, the category attribute provides additional information about the book element. 

To retrive uri `employees.Envelope.#.uri` & to retrive prefix `employees.Envelope.#.prefix` &  to retrive attribute value `employees.Envelope.@.encodingStyle`

<img width="1504" height="363" alt="image" src="https://github.com/user-attachments/assets/5b2823b0-851d-4ab3-9038-7a362031b123" />

<img width="1797" height="809" alt="image" src="https://github.com/user-attachments/assets/1abd28f3-e2e9-4c56-b859-eae2131aeef9" />

### Dynamic Vlaue Selector Examples

<img width="1151" height="432" alt="image" src="https://github.com/user-attachments/assets/d3f6394b-6ed8-45dc-9529-25d1bd5e12a6" />
