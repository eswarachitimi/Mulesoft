# Mule Errors

Mule execution failures result in an error. When a Mule app is running, both the Mule runtime engine and the module and connector operations configured in the app can throw errors that are represented by a Mule error object, which is associated with a Mule event

![image](https://github.com/user-attachments/assets/867cb366-694d-4825-b539-ca2184e31839)

### HTTP Request Error Example

For example, when an HTTP request fails with an HTTP:NOT_FOUND error (for a 404 status code), the values for each part of the Error Message are:

> #[error.description] returns: HTTP GET on resource 'http://jsonplaceholder.typicode.com:80/mybadrequest' failed: not found (404).

> #[error.detailedDescription] returns HTTP GET on resource 'http://jsonplaceholder.typicode.com:80/mybadrequest' failed: not found (404).

> #[error.errorType] returns HTTP:NOT_FOUND

> #[error.cause] returns org.mule.extension.http.api.request.validator.ResponseValidatorTypedException. If you print the return instance of ResponseValidatorTypedException, Mule prints the result of toString. When the error has an associated known HTTP status code (such as 404), the string representation of the ResponseValidatorTypedException instance is a human-readable description of the error.

> #[error.errorMessage] returns:

```
org.mule.runtime.core.internal.message.DefaultMessageBuilder$MessageImplementation
{
  payload=org.mule.runtime.core.internal.streaming.bytes.ManagedCursorStreamProvider@223d8f75
  mediaType=application/json; charset=UTF-8
  attributes=org.mule.extension.http.api.HttpResponseAttributes
{
   Status Code=404
   Reason Phrase=Not Found
   Headers=[
      date=Sat, 03 Aug 2019 04:28:29 GMT
      content-type=application/json; charset=utf-8
      content-length=2
      connection=keep-alive
      set-cookie=__cfduid=de19ed0b495b5b58e74fa0ee31a700d651564806509; expires=Sun, 02-Aug-20 04:28:29 GMT; path=/; domain=.typicode.com; HttpOnly
      x-powered-by=Express
      vary=Origin, Accept-Encoding
      access-control-allow-credentials=true
      cache-control=public, max-age=14400
      pragma=no-cache
      expires=Sat, 03 Aug 2019 08:28:29 GMT
      x-content-type-options=nosniff
      etag=W/"2-vyGp6PvFo4RvsFtPoIWeCReyIC8"
      via=1.1 vegur
      cf-cache-status=HIT
      age=96
      server=cloudflare
      cf-ray=50058b8add0a92fe-SJC
   ]
}
  attributesMediaType=*/*
}
```

The `errorMessage` element becomes available when a connector or component exposes the message that it has interpreted as an error. For example, when an HTTP request receives a status code that Mule treats as an error, the process fails and also populates the `errorMessage` with information about the error. You can then gain access to error message attributes (metadata) and to the payload itself with `#[error.errorMessage.payload]` for the payload and `#[error.errorMessage.attributes]` for the metadata. In the case of an HTTP request that returns an error, you can then use `#[error.errorMessage.attributes.statusCode]` to select the value of the status code (such as 404).

> #[error.childErrors] returns: []

Mule errors have a namespace (such as HTTP: and FILE:) and identifier (such as NOT_FOUND), and they belong to a hierarchy of error types.

- TRANSFORMATION : Error occurred involves Mule Runtime internal transformations and not DataWeave transformations.
- EXPRESSION : indicates an error occurred while evaluating a DataWeave expression.
- VALIDATION :  indicates a validation error occurred.
- REDELIVERY_EXHAUSTED : indicates that max attempts to reprocess a message from a source have been exhausted.
- CONNECTIVITY (RETRY_EXHAUSTED ) : indicates that there was a problem establishing a connection.
- ROUTING : indicates an error occurred while routing a message.
  - COMPOSITE_ROUTING : indicates that one or more errors occurred while routing a message. For example, using a Scatter Gather Router. )
- SECURITY :  indicates a security error occurred, like invalid credentials being received or an expired token being used.
- STREAM_MAXIMUM_SIZE_EXCEEDED :  indicates the maximum size allowed for a stream has been exceeded
- TIMEOUT :  indicates timeout occurred while processing a message.
- UNKNOWN : indicates an unknown or unexpected error occurred.
- CRITICAL : indicates a severe error occurred. These errors cannot be handled.
- OVERLOAD : indicates a problem of overloading occurred and the execution was rejected.
  - FLOW_BACK_PRESSURE : indicates a problem of overloading occurred at the source level. For example, using an HTTP listener as a source.
- FATAL_JVM_ERROR :  indicates that a fatal error occurred, such as stack overflow.
