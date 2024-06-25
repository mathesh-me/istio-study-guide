## Why do we need Istio?

Before getting into istio, let's understand Monolithic and Microservices architecture.

### Monolithic Architecture

In Monolithic architecture, **Developers build a single large application. In simple words, Monolithics architecture include all the functionalities built into a single application.** The application is deployed as a single unit.<br>

**Example:**

Let's say I have a e-commerce application. My application will have functionalities like login, product listing, product details, add to cart, checkout, payment etc. If I want to develop my app in monolithic architecture, I will code all these functionalities in a single application. Now if I want to deploy my application, I will deploy the entire application as a single unit. Now the problem with this approach is if one functionality fails, the entire application will fail. Like if the add to cart functionality fails, the entire application will fail. Also if I want to scale my application, I have to scale the entire application. And also If I want to fix this, I have to redeploy the entire application. To Overcome these problems, we have Microservices architecture. Also remember that, all the other required services like load balancing, service discovery, monitoring, tracing, networking etc., are built into the application itself in a single unit.


### Microservices Architecture

In Microservices architecture, **Developers will build a collection of small services. Each service is built to serve a specific functionality**. Each service is deployed independently.

**Example:**

Consider the same scenario of e-commerce application. In Microservices architecture, I will build separate services for login, product listing, product details, add to cart, checkout, payment etc. Now if I want to deploy my application, I will deploy each service independently. Now if the add to cart functionality fails, only the add to cart service will fail, the entire application will not fail. Also, if I want to scale my add to cart functionality, I can scale only the add to cart service. And also If I have to fix errors, I have to redeploy only the add to cart service. This is the advantage of Microservices architecture. In this architecture, all the other required services like load balancing, service discovery, monitoring, tracing, networking etc. are built separately for each single service. For example, I have to include load balancing, service discovery, monitoring, tracing, networking etc. for each service.

### Reference Diagram for Monolithic Architecture and Microservices Architecture
**Look at the diagram below to get good Understanding Monolith and Microservices**
![monolith_1-monolith-microservices 70b547e30e30b013051d58a93a6e35e77408a2a8](https://github.com/mathesh-me/istio-study-guide/assets/144098846/51f6d593-a56f-4931-b443-f3ded5fa8528)

Now, I have my application built in Microservices architecture. Now I want to make my application more secure, more reliable, more observable, more manageable etc. This is where Service Mesh comes into the picture.

**Diagram Credit:** AWS



### Service Mesh

**Service Mesh help us to move the communication logic out of the application code from Microservice Architecture**. Communication logic means, service discovery, load balancing, traffic management, security, observability etc. **Service Mesh provides a separate layer for all these functionalities which means, all these communication logic are going to built into single layer and not into the application code. That single layer will be deployed as a sidecar container along with the application container. This sidecar container is called as Proxy**. This Proxy will intercept all the incoming and outgoing traffic of the application container. This Proxy will take care of all the communication logic. This is the advantage of Service Mesh. 

The idea behind service mesh is to have a separate layer for all the communication logic. Also if I have to build the same communication logic in each service in microservices architecture, most of the time the logic will be duplicated. So now, I have a separate layer for all these communication logic and deployed as a sidecar container along with the application container. This is the advantage of Service Mesh.

**Now let's get into Istio**

Date of Notes: 23/06/2024
