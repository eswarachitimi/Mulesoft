
## Mule Soft Deployment Options 

Mule applications that run in the `Anypoint Studio` or `Anypoint Code Builder` IDEs deploy to an embedded test server in within the IDE. When we create `Mule applications` using Anypoint Studio or Anypoint Code Builder, we must deploy them using one of the deployment options supported by `Anypoint Runtime Manager`.

A Deployment model defines the cloud services you are consuming and the responsibility model for who manages them.

It defines the architecture, scalability of the computing resources, what you can change, the services provided to you, and how much of the build you own.

The deployment models also define relationships between the cloud infrastructure and users.

Before we start with deployment model lets understand the basics concept to understand the distinguishing factors , Control plane and Runtime plane.

![image](https://github.com/user-attachments/assets/16f576fe-5424-4a2b-8cfe-63c53cf43de5)

![image](https://github.com/user-attachments/assets/e8eeaaee-e38e-44a9-9a2c-1c2aa1729ba4)

> **Control plane**

this is the component of Anypoint platform that is used to design, deploy and manage the APIs and the mule applications.
This includes the Design center , Management center(API manager — helps in managing policies , Runtime manager — helps in scaling out or scaling up , access management — helps in managing access ) , exchange where the assets are publish for reusability purpose.

> **Runtime plane**

the component of Anypoint platform used for deployment of applications and made available to users.
this includes the Mule runtime server and supporting services ,for example : environment to run the applications , Anypoint MQ , object store , persistent queues(available on-premise).
Based on the location of control plane and runtime plane , the deployment models are as follows:
### Cloudhub 1.0

### Cloudhub 2.0

CloudHub 2.0 is the latest version of CloudHub, and it offers improved manageability and functioning as a containerized integration platform as a service (iPaaS). It also scales up or down based on client requirements and ensures flexibility in the applications. It is highly secure, protecting sensitive data and services with secret codes. Additionally, it provides an isolation boundary by running each instance in a separate container.

CloudHub 2.0 is a fully managed, containerized integration platform as a service (iPaaS) where you can deploy APIs and integrations as lightweight containers in the cloud.

You can deploy your applications from the Anypoint PlatformLeaving the Site Runtime Manager cloud console and host them in CloudHub 2.0.

![image](https://github.com/user-attachments/assets/8c185e70-be9e-4faf-8787-439dd4a4941d)

### Hybrid

![image](https://github.com/user-attachments/assets/62629586-eed4-4f7d-9653-b157f8bc9780)

### RTF ( Run time Fabric )

### PCE ( Private Cloud Edition )

### PCF ( Pivotal Cloud Founcry )
