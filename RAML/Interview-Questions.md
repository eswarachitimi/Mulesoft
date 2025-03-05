#### What is RAML?

The RESTful API Modeling Language is a YAML-based language that is used to describe RESTful APIs. It contains all of the information required to describe or practically describe RESTful APIs. Although RAML was designed with RESTful APIs in mind, it is suitable to describe APIs that do not adhere to all REST constraints.


#### What are the different HTTP methods that RAML supports?

The HTTP methods that RAML supports are as below:

**GET:** used to describe retrieval of data.
**PUT:** used to describe updating the data.
**PATCH:** used to describe to partial Update/Modify
**POST:** used to describe to add new record
**DELETE:** used to describe to delete record

#### What is Resource Types?

A resource type is a template that may be used by numerous resources to specify methods, descriptions, and parameters without having to write the same code again and over.

#### How to define Resource Types with HTTP methods?

We can define Resource Types with HTTP methods as below:

![image](https://github.com/user-attachments/assets/1403fd2a-b9f5-4e67-8b7a-19c04ef34999)

Under the resource type "collection", we've created two methods. Define the methods responses and descriptions now.
Note: We can provide any name to resource type, in this example we have given name as "collection".

#### How to call Resource Types from Resources?

To reduce duplicate code will utilize the resource types defined in API Spec. In resources //fixed_pay and //variabl_pay, we'll get resource type "collection".

You could see that the fixed_pay and variable_pay resources are both calling our resourceType collection, implying that both resources now have POST and GET methods.

![image](https://github.com/user-attachments/assets/a2ba9558-64ed-4222-851c-3120ed71947a)

#### How to add security in RAML?

The root level of the.raml file defines security. So, let us define our HTTP basic security scheme:

![image](https://github.com/user-attachments/assets/2b6abdeb-435c-48a9-ba54-fd142ac7cb61)

#### How to define Data Types in a .raml file?

We will define the data types used .raml file:

types:
  Foo:
    type: object
    properties:
      id:
        required: true
        type: integer
      name:
        required: true
        type: string
      ownerName:
        required: false
        type: string
Q: What is the difference between Raml and swagger?
Ans:

RAML
Swagger
The goal of creating RAML is to provide crucial information to RESTful APIs in order to make API design easier.

Swagger's purpose is to maintain documentation, client libraries, and source code all in sync.

RAML was founded in the year 2013.

Swagger, previously known as OpenAPI, is a specification that was created in 2010.

Current version of RAML is RAML1.0(2017-07-06)

The current version of Swagger is 3.0.1(2017-12-17)

RAML is supported by Mulesoft, Intuit, AngulasJs, PayPal, Programmable Web and API service, Cisco, VMWare, etc

Swagger is supported by Google, IBM, Atlassian and Microsoft.

Tools and Editors for RAML, API Workbench IDE based on Atom.

Tools and Editors for Swagger are CodeGen, UI and Editor.

RAML is preferred by developers due to its API specification, design patterns, and code reusability, as well as the fact that it is human readable.

Swagger was chosen because it is open-source, free to use, flexible, and capable of executing API calls directly from documentation.

Mulesoft is the primary sponsor of RAML.

SmartBear is the primary sponsor of Swagger.

RAML allows the user to view how the API looks while designing simple text that is easy to read.

Swagger is a developer-only documentation tool, which means that the project can only be documented by the user who writes the API.

The primary motivation for creating RAML is that it appeals to programmers.

Swagger is based on JSON and has format and data serialization limitations.

RAML supports JSON schema and W3C XML.

Swagger does not support XML, and version 1.2 uses only a subset of JSON.

Q: What is Traits in raml?
Ans:
Traits are similar to functions in that they allow you to declare common properties for HTTP methods.



Q: How to Declare Traits in raml?
Ans:
We can either define the traits in the root section or build a fragment and import it into the API Spec.

traits:
  client-id-required:
    headers:
      client_id:
        type: string
      client_secret:
        type: string
Q: How to call Traits from Resources in RAML?
Ans:
The traits can be referred to by the term "is". For example, is: [trait_name]

traits:
  client-id-required:
    headers:
      client_id:
        type: string
      client_secret:
        type: string

resourceTypes:
      collection:
          get:
            is: [client-id-required]
            responses:
              200:
                body:
                 application/json:
                    example: |
                      <<exampleReference1>
/fixed_pay:
   type:
     collection:
         exampleReference1: !include /examples/fixedPay.json


Q: How do I define an API resource and it's parameters in a .raml file?
Ans:
First define the top-level resource (URI) of API :

/foos:
Then, we can expand other resource and parameters given below:
/foos:
  /{id}:
  /name/{name}:
URI parameter defines inside {}.
Q: How to declare method definition in .raml file?
Ans:
We can provide the HTTP methods that should be used for each resource.

/foos:
  get:
  post:
  /{id}:
    get:
    put:
    delete:
  /name/{name}:
Q: How to declare Query Parameters, with its response and status structure?
Ans:

/foos:
  get:
    description: List all Foos matching query criteria, if provided;
                 otherwise list all Foos
    queryParameters:
      name?: string
      ownerName?: string
    responses:
      200:
        body:
          application/json:
            type: Foo[]
            example: |
              [
                { "id" : 1, "name" : "XYZ" },
                { "id" : 2, "name" : "ABC" }
              ]
Q: Is it possible to use the same HTTP methods multiple times for a single request path?
Ans:
No, In RAML, we could only use one HTTP method for a single request path. For example, if the request url is "/users/user," the GET, PUT, POST, PATCH, or DELETE HTTP methods can only be defined once.
