
> ## _Mule Soft Deployment Options_ 

Mule applications that run in the `Anypoint Studio` or `Anypoint Code Builder` IDEs deploy to an embedded test server within the IDE. When we create `Mule applications` using Anypoint Studio or Anypoint Code Builder, we must deploy them using one of the deployment options supported by `Anypoint Runtime Manager`.

A Deployment model defines the cloud services you are consuming and the responsibility model for who manages them.

It defines the architecture, scalability of the computing resources, what you can change, the services provided to you, and how much of the build you own.

Before we start with deployment model lets understand the basics concept to understand the distinguishing factors , Control plane and Runtime plane.

![image](https://github.com/user-attachments/assets/fb84e3a7-0c18-4604-9069-4d3c4f7174a8)

> #### _Control plane_

This is the component of Anypoint platform that is used to design, deploy and manage the APIs and the mule applications. This includes -

- Design center
- Management center
  -  API manager — helps in managing policies
  -  Runtime manager — helps in scaling out ( Horizantal Scaling - Adding more workers/Replicas) or scaling up ( Vertical Scaling - Adding more vCores/Replica Count )
  -  access management — helps in managing access (Assigning roles and access privileges to users )
-  Exchange where the assets are publish for reusability purpose.

> #### _Runtime plane_

The component of Anypoint platform that is used for deployment of applications and made available to users. This includes -

 - Mule runtime engine/server
   - environment to run the applications 
 - Mule runtime services
   - Anypoint MQ
   - object store
   - persistent queues(available on-premise)
   - Enterprise Security

Based on the location of control plane and runtime plane , the deployment models are as follows:

> ### _Cloudhub Deployment Model_

> #### _Cloudhub 1.0_

> #### _Cloudhub 2.0_

CloudHub 2.0 is the latest version of CloudHub, and it offers improved manageability and functioning as a containerized integration platform as a service (iPaaS). It also scales up or down based on client requirements and ensures flexibility in the applications. It is highly secure, protecting sensitive data and services with secret codes. Additionally, it provides an isolation boundary by running each instance in a separate container.

CloudHub 2.0 is a fully managed, containerized integration platform as a service (iPaaS) where you can deploy APIs and integrations as lightweight containers in the cloud.

You can deploy your applications from the Anypoint PlatformLeaving the Site Runtime Manager cloud console and host them in CloudHub 2.0.

![image](https://github.com/user-attachments/assets/8c185e70-be9e-4faf-8787-439dd4a4941d)

> ### _Hybrid_

![image](https://github.com/user-attachments/assets/62629586-eed4-4f7d-9653-b157f8bc9780)

> ### _RTF ( Run time Fabric )_

> ### _PCE ( Private Cloud Edition )_

> ### _PCF ( Pivotal Cloud Founcry )_

![image](https://github.com/user-attachments/assets/e8eeaaee-e38e-44a9-9a2c-1c2aa1729ba4)
