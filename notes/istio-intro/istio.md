## Istio Introduction

**Istio is an open-source service mesh that provides a uniform way to secure, connect, and monitor our microservices**. Istio provides key capabilities for service discovery, load balancing, traffic management, security, observability, etc. Istio is built on top of Envoy proxy which is a open-source service proxy designed for cloud-native applications.

### How Istio works?

As we discussed earlier, just like How Service Mesh works, **Istio will deploy a sidecar container called as Proxy along with the application container. Envoy proxy is the default proxy used by Istio.** This Proxy will intercept all the incoming and outgoing traffic of the application container.

### Istio Architecture

Istio architecture consists of the following components:

1. **Data Plane**: The data plane is responsible for handling the network traffic between the microservices. The communication between the proxies we deploy in our application containers is called as data plane.

2. **Control Plane**: The control plane is responsible for managing and configuring the proxies to route the traffic. The control plane is responsible for configuring the data plane.

#### Components of Istio Architecture

1. **Envoy Proxy**: Envoy is a high-performance proxy developed in C++. Envoy will intercept all the incoming and outgoing traffic of the application container. Envoy is the default proxy used by Istio.

2. **Istiod**: Istiod is the control plane component of Istio. Istiod is responsible for managing and configuring the proxies to route the traffic.
it contains the following components:
    - **Pilot**: Pilot is responsible for service discovery and traffic management. It is responsible for configuring the Envoy proxies.
    - **Galley**: For Validating configuration files.
    - **Citadel**: Citadel is responsible for certificate management.

Date of Notes: 23/06/2024