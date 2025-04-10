#### What is the difference between CloudHub and CloudHub 2.0 ?

- The main difference is CloudHub is using EC2 instance in AWS for application deployment and CloudHub 2.0 is using EKS (Elastic Kubernetes Service) in AWS for application deployment.
- CloudHub has maximum of 16 vCores with 32gb memory, but CloudHub 2.0 has maximum of 4 vCores 15gb memory.
- The Minimum memory that CloudHub has is 0.1 vCores 512Mb memory, while CloudHub 2.0’s minimum memory is 0.1 vCores with 1.2gb memory.
- As EKS is known to be fast, applications deployed in CloudHub 2.0 are faster than CloudHub applications.
- In CloudHub we have the instance as workers and worker size, where in CloudHub 2.0 are named as Replicas and Replica size.
- CloudHub we have Persistent queue option, where CloudHub 2.0 doesn't have the Persistent queue option. Instead we use MQ in CloudHub 2.0.
- When deployed to CloudHub, application's connection is http as default, where CloudHub 2.0 has https connection by default.
- Only CloudHub 2.0 has Ingress option and 2 Deployment model options namely Rolling update, Recreate.
- CloudHub use VPC's, while CloudHub 2.0 use Private spaces to provide isolations and control while deploying applications.
