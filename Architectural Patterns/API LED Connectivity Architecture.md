
# API-Led Connectivity

_**`API-led connectivity`**_ is a modern approach to integrating applications and data using reusable APIs, replacing point-to-point integrations for a more flexible, scalable, and agile architecture. It focuses on creating well-defined APIs that can be managed, secured, published, and monetized, enabling faster and more efficient integrations. 

![image](https://github.com/user-attachments/assets/fa01b382-77f2-4b16-9f35-191910c54bde)

## Key Principles:

![Benefits_ - visual selection (1)](https://github.com/user-attachments/assets/9c9720d0-7090-48d2-a355-0b4a8c785e2c)

**_Bottom-up approach:_**

APIs are created at the system layer and then reused to build higher-level APIs for processes and experiences.

## Three-layer approach:

- **System Layer:** `Building Blocks of Integration`

  APIs access backend systems. This layer involves creating APIs that expose the functionalities of individual systems, applications, or data sources. These APIs serve as the building blocks for integration and can be reused across various projects. An additional responsibility of System APIs is to expose the data in a common data model so that it can be reused within the enterprise.
  
- **Process Layer:** `Orchestrating Business Goals`

  These APIs interact with system APIs, providing aggregation, orchestration, and encapsulating business capabilities.

- **Experience Layer:** `Crafting User-Centric Interfaces`

  These APIs abstract the complexities of underlying systems and provide a user-friendly interface for consuming services. Where APIs are exposed and consumed by their intended audience. The gateway to user interaction, this layer encompasses user interfaces, web browsers, and mobile apps, focusing on presenting information and gathering input. 

_**API Management:**_ APIs are managed, secured, published, and monetized using API management software.

_**Data Transformation and Enrichment:**_ APIs can act as intermediaries, enabling data transformation, enrichment, and validation. 

> **The Pros outsmarts the cons**

### Cons

- Network calls there by incurring network latency because of multiple layers ( Creates multiple nodes of API Network ).

### Benefits:

- Moving for Legacy to Digital Enablement.
- Abstraction ( Abstracting protocols, security & transformation. All the complex overhead that has to be done to get the data. Consumer knows about the experience API. System API & Process API implementation is abstracted)
-  Innovation - Experience API is driving this. Multiple consumers can use this


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

## Legacy Bank -Problems

![image](https://github.com/user-attachments/assets/4e2d0e96-c4ae-4c0f-a35e-ff47d16a07d6)

![image](https://github.com/user-attachments/assets/a8296c9d-0d51-4131-ae5c-b759b0543338)

![image](https://github.com/user-attachments/assets/ed11523a-731f-4bc9-81ef-634c992ff872)

![image](https://github.com/user-attachments/assets/82152140-bcdb-4578-9536-bdd8f23e97cb)

![image](https://github.com/user-attachments/assets/c57bcf9e-63ee-4055-9ef2-147c966db349)


