## Dataweave Expressions

- _Flow name in an API_	👉🏼 `#[flow.name]`
- _API Name_  👉🏼 `#[api.name]`
- _Working directory path_ 👉🏼 **Example-** `${mule.home}/apps/${app.name}/.`
- _Correlation ID_ 		👉🏼 `#[correlationId]`
- _Loading a file_ 		👉🏼 `${file::properties-file.txt}`
- _Extracting the underlying java exception class_		👉🏼 `#[if (error.exception.cause.^class == null) error.cause.^class else error.exception.cause.^class]`
- _Extracting the underlying exception message_		👉🏼 `#[if (error.exception.cause.message == null) error.cause.message else error.exception.cause.message]`
- _Extracting error type and description_		👉🏼 `#[error.errorType.namespace], #[error.errorType.identifier], #[error.description]`
- _Extracting the error payload_		👉🏼 `#[error.errorMessage.payload]`
- _Accessing Global Functions maintained in a Dataweave Script_		👉🏼 `#[global::functions::urlEncode("sample value")]`
- _Accessing fields in Web Service Response_ 		👉🏼 `payload.body`
- _Status Code pertaining to a HTTP Response received_		👉🏼 `#[message.attributes.statusCode]`
- _Soap Fault Code_		👉🏼 `#[error.exception.faultCode.localPart]`
- _Soap Fault String_		👉🏼 `#[error.exception.message]`
- _Coercing raw data to string_		👉🏼 `#[payload.^raw as String]`
- _Munit assertion for json,csv,xml_		👉🏼 Ex: `#[MunitTools::equalTo(readUrl('classpath://somepath/abc.json', 'application/json'))]`
- _Removing multiple elements from an object_		👉🏼 `#[payload - <key1> - <key2>]`
- **In Transformer -**
  
```
%dw 2.0
output application/json
---
{aa: "a", bb: "b", cc: "c"} - "bb" - "cc"
Removing a record from a list	#[(message.payload - message.payload[index]) as Array]
```

- **Forming dynamic keys -**
  
```
%dw 2.0 
output application/json 
--- 
{ 
     (vars.input1 ++ vars.input2): { 
                               ........ 
     } 
}
```

- Use the expression within `()` to be evaluated to a dynamic key
- namic SQL Queries	truncate table `${table.name}` drop storage
  
- **Dynamically loading DWL files -**

```
%dw 2.0
output application/java
var load = readUrl("classpath://somepath/" ++ vars.fileName ++ ".dwl","application/dw")
---
load(payload)
```
- **Loading SQL script from SQL Files in Database Connector.	Place below line in SQL Query Text in the database connector -**

```
#[output text/plain --- readUrl("classpath://somepath/ ++ vars.filename ++ ".sql" ,"text/plain")]
```

- **Get/Remove Extension from filename -**
```
%dw 2.0
import java!org::apache::commons::io::FilenameUtils
//Custom functions to handle file extensions
fun removeExtension(filename: String) = (FilenameUtils::removeExtension(filename))
fun getExtension(filename:String) = (FilenameUtils::getExtension(filename))
Note: Apache Commons Dependency needs to be added.
```

- **GMT Time Zone -**
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
