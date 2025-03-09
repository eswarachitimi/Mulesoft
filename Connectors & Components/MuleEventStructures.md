## Mule Events
A Mule event contains the core information processed by the runtime. It travels through components inside your Mule app following the configured application logic.

Note that the Mule event is immutable, so every change to an instance of a Mule event results in the creation of a new instance.

A Mule event is composed of these objects:

- A Mule Message contains a message payload and its associated attributes.
- Variables are Mule event metadata that you use in your flow.

![image](https://github.com/user-attachments/assets/8c913a41-5d91-4baa-bb5a-5d7fdaa98025)

![image](https://github.com/user-attachments/assets/01f8b3b2-e575-4331-848b-b4e2e9bf95b9)


##### Example: HTTP Response Attributes

```
{
   Status Code=200
   Reason Phrase=OK
   Headers=[
      date=Sun, 20 Jan 2019 19:13:51 GMT
      content-type=text/html;
      charset=UTF-8
      transfer-encoding=chunked
      connection=keep-alive
      set-cookie=__cfduid=d03462713a0b2c57c8d2ad3bf311287041548011631;
      expires=Mon, 20-Jan-20 19:13:51 GMT;
      path=/;
      domain=.typicode.com;
      HttpOnly
      x-powered-by=Express
      vary=Origin, Accept-Encoding
      access-control-allow-credentials=true
      cache-control=public, max-age=14400
      last-modified=Tue, 15 Jan 2019 18:17:15 GMT
      via=1.1 vegur
      cf-cache-status=HIT
      expires=Sun, 20 Jan 2019 23:13:51 GMT
      expect-ct=max-age=604800,
      report-uri="https://report-uri.cloudflare.com/cdn-cgi/beacon/expect-ct"
      server=cloudflare
      cf-ray=49c3dc570c2f281c-SJC
   ]
}
```

- attributes.statusCode to select an HTTP status code like 200.
- attributes.headers.date to select Sun, 20 Jan 2019 18:54:54 GMT from the header of an HTTP response.
- attributes.headers.'content-type' to select the HTTP content type application/json

# Correlation ID

When Mule creates a new event, it generates a unique identifier string called a correlation ID before sending the event to the next processor in the flow. This ID enables you to correlate different log entries with a particular execution.

To change how Mule generates the correlation ID:

- Add the <configuration> component to your application XML.
- Set the correlationIdGeneratorExpression attribute to specify the expression that generates the correlation ID:

```
<configuration correlationIdGeneratorExpression="#[<custom_generator_expression>]"/>

<logger level="INFO" message="#[correlationId]"/>
```

# Variables in Mule Apps

Variables are used to store per-event values for use within a flow of a Mule app. The stored data can be any supported data type, such as an object, number, or string. It is also possible to store -

- the current message (using the message keyword)
- the current message payload (using the payload keyword) or
- just the current message attributes (using the attributes keyword).
- However, the keyword *vars* (for example, vars.someOtherVar) is not allowed.

You can create, or update, variables in these ways:

- Using the Set Variable component.
- Using a Target Variable from within an operation, such as the Read operation to the File connector or the Store operation to the Database connector.
- Using the DataWeave Transform Component (EE-Only)
- Using Scripting Component (in scripting module)

You can also delete/remove:

- Using the Remove Variable component.

If the name of your variable is myVar, you can access it like this: vars.myVar
