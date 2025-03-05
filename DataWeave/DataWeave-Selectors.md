DataWeave has total 13 selectors. DataWeave selectors traverse the structures of objects and arrays and return matching values.


- Single-value   👉🏼  .keyName   👉🏼  Any type of value that belongs to a matching key

- Multi-value   👉🏼  .*keyName   👉🏼  Array of values of any matching keys

- Descendants   👉🏼  ..keyName   👉🏼  Array of values of any matching descendant keys

- Dynamic   👉🏼  See Dynamic Selector.

- Key-value pair   👉🏼  .&keyName   👉🏼  Object with the matching key

- Index   👉🏼  [<index>]   👉🏼  Value of any type at selected array index. Use negative numbers to index from the end of an array, for example, -1 for the last element in the array. Use of    
                                numbers beyond the array size returns null.

- Range   👉🏼  [<index> to <index>]   👉🏼  Array with values from selected indexes

- XML attribute   👉🏼  @, .@keyName   👉🏼  String value of the selected attribute

- Namespace   👉🏼  keyName.#   👉🏼  String value of the namespace for the selected key

- Key present   👉🏼  keyName?, keyName.@type?   👉🏼  Boolean (true if the selected key of an object or XML attribute is present, false if not)

- Assert present   👉🏼  keyName!   👉🏼  String: Exception message if the key is not present

- Filter   👉🏼  [?(boolean_expression)]   👉🏼  Array or object containing key-value pairs if the DataWeave expression returns true. Otherwise, returns the value null.

- Metadata   👉🏼  .^someMetadata    👉🏼  Returns the value of specified metadata for a Mule payload, variable, or attribute. The selector can return the value of class (.^class), content  
                                         length (.^contentLength), encoding (.^encoding), mime type (.^mimeType), media type (.^mediaType), raw (.^raw), and custom (.^myCustomMetadata) 
                                         metadata.
