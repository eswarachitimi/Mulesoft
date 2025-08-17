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

<img width="1230" height="521" alt="image" src="https://github.com/user-attachments/assets/a1105c90-53bf-414d-a381-6f84cc0b17b8" />

<img width="1521" height="711" alt="image" src="https://github.com/user-attachments/assets/8caafb3c-cfc6-41f3-9c02-0d22195b2766" />

### Descendant Selector Example

<img width="1524" height="538" alt="image" src="https://github.com/user-attachments/assets/e797815a-785e-4fd6-aced-5073b79958c6" />

### Key-Value pair Selector Example

<img width="1242" height="676" alt="image" src="https://github.com/user-attachments/assets/2baa3768-b597-46a5-a52a-d38e96e23e08" />

### Range Selector Example

<img width="1233" height="635" alt="image" src="https://github.com/user-attachments/assets/54420da1-948d-4c80-bb6c-452e39e887a8" />

### Key Present Selector Example

<img width="1126" height="540" alt="image" src="https://github.com/user-attachments/assets/efb4e0fc-b20c-42af-b631-1a0097a3137f" />

### Key Assert Selector Example

<img width="1223" height="647" alt="image" src="https://github.com/user-attachments/assets/d4a85a12-acf0-48b9-a436-b8386cf4a252" />

### Filter Selector Example

if condition not satisfied, filter selector returns the `null` value.

<img width="1278" height="656" alt="image" src="https://github.com/user-attachments/assets/7d7e18fa-9327-4a68-91db-97072c905c55" />

