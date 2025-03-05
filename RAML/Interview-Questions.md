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

![image](https://github.com/user-attachments/assets/fdc9bb13-eda5-4fa2-9d88-a27d5d3b123a)

#### What is Traits in raml?

Traits are similar to functions in that they allow you to declare common properties for HTTP methods.

#### How to Declare Traits in raml?

We can either define the traits in the root section or build a fragment and import it into the API Spec.


![image](https://github.com/user-attachments/assets/f6365d38-5aab-4774-a5d3-bbdc43e036e5)

#### How to call Traits from Resources in RAML?

The traits can be referred to by the term "is". For example, is: [trait_name]

![image](https://github.com/user-attachments/assets/91e35047-5a43-47e3-b17f-ca9828454401)


#### How do I define an API resource and it's parameters in a .raml file?

![image](https://github.com/user-attachments/assets/77baa110-48a8-4755-91d4-bb171536908d)


#### How to declare method definition in .raml file?

We can provide the HTTP methods that should be used for each resource.

![image](https://github.com/user-attachments/assets/086c5419-eefd-4434-9063-639c8a40e392)


#### How to declare Query Parameters, with its response and status structure?

![image](https://github.com/user-attachments/assets/2f036837-0134-4d9d-9d28-37c247bf2019)


#### Is it possible to use the same HTTP methods multiple times for a single request path?

No, In RAML, we could only use one HTTP method for a single request path. For example, if the request url is "/users/user," the GET, PUT, POST, PATCH, or DELETE HTTP methods can only be defined once.
