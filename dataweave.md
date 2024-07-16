# Dataweave Expressions

- Flow name in an API	👉🏼 #[flow.name]
- Client/Caller to an API		👉🏼 #[authentication.properties.clientName]
- Correlation ID 		👉🏼 #[correlationId]
- Loading a file 		👉🏼 ${file::properties-file.txt}
- Extracting the underlying java exception class		👉🏼 #[if (error.exception.cause.^class == null) error.cause.^class else error.exception.cause.^class]
- Extracting the underlying exception message		👉🏼 #[if (error.exception.cause.message == null) error.cause.message else error.exception.cause.message]
- Extracting error type and description		👉🏼 #[error.errorType.namespace], #[error.errorType.identifier], #[error.description]
- Extracting the error payload		👉🏼 #[error.errorMessage.payload]
- Accessing Global Functions maintained in a Dataweave Script		👉🏼 #[global::functions::urlEncode("sample value")]
- Accessing fields in Web Service Response 		👉🏼 payload.body
- Status Code pertaining to a HTTP Response received		👉🏼 #[message.attributes.statusCode]
- Soap Fault Code		👉🏼 #[error.exception.faultCode.localPart]
- Soap Fault String		👉🏼 #[error.exception.message]
- Coercing raw data to string		👉🏼 #[payload.^raw as String]
- Removing multiple elements from an object		👉🏼 #[payload - <key1> - <key2>]

```
In Transformer:
%dw 2.0
output application/json
---
{aa: "a", bb: "b", cc: "c"} - "bb" - "cc"
Removing a record from a list	#[(message.payload - message.payload[index]) as Array]
Forming dynamic keys	%dw 2.0 
output application/json 
--- 
{ 
     (vars.input1 ++ vars.input2): { 
                               ........ 
     } 
}
```

- Use the expression within () to be evaluated to a dynamic key
- namic SQL Queries	truncate table ${table.name} drop storage
  
- Dynamically loading DWL files	

```
%dw 2.0
output application/java
var load = readUrl("classpath://somepath/" ++ vars.fileName ++ ".dwl","application/dw")
---
load(payload)
```
- Loading SQL script from SQL Files in Database Connector	Place below line in SQL Query Text in the database connector

```
#[output text/plain --- readUrl("classpath://somepath/ ++ vars.filename ++ ".sql" ,"text/plain")]
```

- Get/Remove Extension from filename
```
%dw 2.0
import java!org::apache::commons::io::FilenameUtils
//Custom functions to handle file extensions
fun removeExtension(filename: String) = (FilenameUtils::removeExtension(filename))
fun getExtension(filename:String) = (FilenameUtils::getExtension(filename))
Note: Apache Commons Dependency needs to be added.
```
- Munit assertion for json,csv,xml		👉🏼 Ex: #[MunitTools::equalTo(readUrl('classpath://somepath/abc.json', 'application/json'))]
- GMT Time Zone
```
%dw 2.0
output application/json
fun format(d: DateTime) = d as String {format: "yyyy-MM-dd'T'HH:mm:ss'Z'"}
---
{
    "CreatedDateTime" : format((now()) >> "GMT"),
    "CreatedDateTimeLessthan4Hours" : format((now() - |PT4H|) >> "GMT"),
    "currentDate" : now()
}
```

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


📝 Sources
```
https://developer.mulesoft.com/tutorials-and-howtos/dataweave/learn-dataweave-with-the-dataweave-playground-getting-started/
https://medium.com/@myid535/dataweave-100-solved-practice-interview-problems-275fa654a143
https://docs.mulesoft.com/dataweave/latest/dataweave-selectors
https://www.prostdev.com/post/dataweave-2-0-core-functions-cheatsheet
https://docs.mulesoft.com/dataweave/latest/dw-functions
https://docs.mulesoft.com/dataweave/latest/dw-operators
https://docs.mulesoft.com/dataweave/latest/dataweave-system-properties
https://docs.mulesoft.com/dataweave/latest/dataweave-flow-control-precedence
https://docs.mulesoft.com/dataweave/latest/dw-core

```
