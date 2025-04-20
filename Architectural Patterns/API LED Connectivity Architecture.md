
# API-Led Connectivity

_**`API-led connectivity`**_ is a modern approach to integrating applications and data using reusable APIs, replacing point-to-point integrations for a more flexible, scalable, and agile architecture. It focuses on creating well-defined APIs that can be managed, secured, published, and monetized, enabling faster and more efficient integrations. APIs can act as intermediaries, enabling data transformation, enrichment, and validation.

![image](https://github.com/user-attachments/assets/fa01b382-77f2-4b16-9f35-191910c54bde)

## Key Principles:

![Benefits_ - visual selection (1)](https://github.com/user-attachments/assets/9c9720d0-7090-48d2-a355-0b4a8c785e2c)

**_Bottom-up approach:_**

APIs are created at the system layer and then reused to build higher-level APIs for processes and experiences.

## Three-layer approach:

API Led Connectivity talks about three layers like Experience API, Process API and System API. Each layer has its own roles, responsibility and functionality. API Led Connectivity comprises three layers mentioned but every time it is not necessary we require all three layers.

### System Layer: 

> `Building Blocks of Integration`

 System API allows you to fetch the raw data from the system of records like JDBC, SAP, Salesforce, AS400 etc. Data fetch from backend systems can be exposed to upstream API in a secure and reliable way. These APIs serve as the building blocks for integration and can be reused across various projects. An additional responsibility of System APIs is to expose the data in a common data model so that it can be reused within the enterprise.

- System API responsible for connecting backend systems and fetching required raw data.
- Transforming the data fetch from backend systems.
- Cleaning the raw data from backend systems.
- Exposing the data to the upstream API (Process or Experience API) in a secure and reliable way.
- Error Handling. Mapping the errors from backend systems.
- Below questions needs to be addressed for designing right System APIs

**What will be the core functionality of System API?**

- Do we require System API?
- How many systems are involved? Do we need to create a System API for each backend system?
- What kind of security measures need to be taken care of for System APIs?
- Do we need wrapper around existing System API that is written in non MuleSoft?

**Below list of things needs to be taken care while designing the System API**

- System API generally not exposed publicly and it should be deployed within a private network or private port (e.g. On CloudHub, System API can be deployed on a private port within Anypoint Virtual Private Cloud).
- Always provide an internal URL to upstream API to communicate with System APIs.
- There must be one System API for one backend System. In case, if you follow Domain Driven Design there can be multiple system API for one system (e.g. You have a monolithic web service which has operations related to multiple domains, in such a case you can group operations related to domains and create multiple system API as per number of domains).
- There might be some backend systems that are not ready to pick up heavy traffic. In such cases, guard System API with Spike Control or Rate Limiting policies.

### Process Layer:

> `Orchestrating Business Goals`

 Process API is responsible for orchestrating multiple downstream API (i.e. Collecting the data from multiple downstream API). The core functionality of Process API is to implement business logic, data aggregation, routing etc.

- Exposing the data to the upstream API (Experience) in a secure and reliable way.
- Responsible for handling business logic, data aggregation, routing etc.
- Error Handling. Mapping the errors from System APIs.
- Responsible for orchestration of call to System API (i.e. use of scatter gather components, choice router etc.)
- Line of Business is responsible for Process API. It is also known as layer of innovation and agility.

**Below questions needs to be addressed for designing right Process APIs**

- What will be the core functionality of the Process API?
- Do we require Process API?
- Does Business Logic already exist in backend service (e.g. Stored Procedure on Database having Business Logic)? Do we need to implement Business Logic in the Process Layer? (It is always good best practices to have most of the complex business logic in the backend system if they are capable. In case if backend systems are not able to handle business logic, MuleSoft provides all required components to implement any kind of business logic).
- Who will be consumers of the Process API? (e.g. Most of the time Process API will be consumed by multiple User Experience API to promote reusability).
- What security measures need to be taken care of a Process API

**Below list of things needs to be taken care while designing the Process API**

- Process API generally is not exposed publicly and it should be deployed within a private network or private port (e.g. On CloudHub, Process API can be deployed on a private port within Anypoint Virtual Private Cloud). In case, if you want to expose Process API to consumers, you can create API Proxy on top of Process API and ask consumers to connect through API Proxy. In this way, we can stop exposing Process API implementation directly.
- Always provide an internal URL to upstream internal API to communicate with Process APIs.
- Process API must be secured by applying security policies like Client Id Enforcement Policies.
  
### Experience Layer:

> `Crafting User-Centric Interfaces`

Experience API is the user facing API and it can be reused by different channels like mobile applications, web applications or any other channels. Generally, Experience APIs are channel specific (for example, mobile application can consume mobile API, web application can consume web API etc.). These APIs abstract the complexities of underlying systems and provide a user-friendly interface for consuming services. 

- Error Handling. Mapping the errors from Process or System APIs.
- Consumes Process or System APIs.
- Perform data transformation according to need to consumers.
- Expose channel specific API.

**Below questions needs to be addressed for designing right Experience APIs**

- What will be the core functionality of the Experience API?
- Does Experience API have multiple consumers?
- Do we require Experience API?
- What security measures need to be taken care of at Experience API?
- How to secure APIs from DoS or DDoS attacks?
- Do different consumers have different security requirements?

**Below list of things needs to be taken care while designing the Experience API**

- Experience API must be not responsible for orchestration, routing or any business logic.
- Experience API must be enabled with strong Authentication and Authorization like OAuth 2.0
- Experience API must have extra security to avoid DoS, DDoS or any API attacks.

> `pros outsmart the cons`

### Disadvantages

- Network calls there by incurring network latency because of multiple layers ( Creates multiple nodes of API Network ).

### Advantages:

- Moving from Legacy to Digital Enablement.
- Abstraction ( Abstracting protocols, security & transformation. All the complex overhead that has to be done to get the data. Consumer knows about the experience API. System API & Process API implementation is abstracted)
- Innovation - Experience API is driving this. Multiple consumers can use this.

![Benefits_ - visual selection](https://github.com/user-attachments/assets/4cd785d1-1486-4a6e-9281-f8121893ce3d)

## What’s Permitted and What’s Not

By working with customers over the past few years I realised that there is still a lot of misunderstanding or confusing related to the API-led connectivity network. Hence, it is not rare that following question arises:

**“Am I allowed to call a System API from an Experience API? “**

> The simple answer is “Yes”. There is no need to always create a Process API if no logic is required. Experience APIs are allowed to directly call System APIs.

**I often tell my customers following:**

> “There are some ground rules in the API-led methodology that should not be broken — everything else can be defined based on individual requirements”

### What’s Permitted?

The rulebook of API-led methodology offers clarity:

![image](https://github.com/user-attachments/assets/fa48c46d-50c1-4baa-96b0-9b8f1fe4beb4)

### What’s Not Permitted?

Outlined in the visual below are the fundamental rules that define the boundaries of the API-led network.

![image](https://github.com/user-attachments/assets/ac1e0195-d676-4b7e-999a-117b89eb304c)

### Customise Your API-Led Architecture

Beyond the ground rules, a company often necessitates custom requirements. The landscape of API-led connectivity thrives on adaptability. Consider the example of a Utils Service. This service is supposed to be used within all different APIs and hence it has to be called from anywhere (Experience, Process and System APIs). We know from our ground rules that the the service should not to be called from anywhere, right?

This is not fully true. We can place a Utils Service in our API-led network. I recommend to place it outside of the API-led landscape and name it differently. It has to be clear that this is a Utils Service and not belonging to one of the API layers.

![image](https://github.com/user-attachments/assets/7182f3dc-73e2-4156-8923-f14e64741d61)

The Utils Service is not the only example of how you can customise the API-led methodology. As you probably know MuleSoft applications doesn’t always have to be APIs. They can also be services, micro-services or for instance batch process applications. Here a few more ideas how you can adapt the rules of the API-led methodology as long as you don’t change the ground rules.

![image](https://github.com/user-attachments/assets/94f2eac1-4d2a-41b0-bb7b-db7c1b7af821)

![image](https://github.com/user-attachments/assets/63475221-35c7-4d80-ac22-28a2e368dbcf)

![image](https://github.com/user-attachments/assets/940b2e39-382b-41ab-808e-00fca736ff37)

![image](https://github.com/user-attachments/assets/77a222e0-7cb7-4ec8-8172-4cf49e02c40f)

![image](https://github.com/user-attachments/assets/dce4f0b4-e921-42db-8ed5-b5020148aba2)

## Legacy Bank -Problems

![image](https://github.com/user-attachments/assets/4e2d0e96-c4ae-4c0f-a35e-ff47d16a07d6)

![image](https://github.com/user-attachments/assets/a8296c9d-0d51-4131-ae5c-b759b0543338)

![image](https://github.com/user-attachments/assets/ed11523a-731f-4bc9-81ef-634c992ff872)

![image](https://github.com/user-attachments/assets/82152140-bcdb-4578-9536-bdd8f23e97cb)

![image](https://github.com/user-attachments/assets/c57bcf9e-63ee-4055-9ef2-147c966db349)


