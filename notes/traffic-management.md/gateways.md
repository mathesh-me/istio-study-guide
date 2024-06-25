## Gateways

***Gateways are used to serve outside traffic into the service mesh.*** It acts as an entry point for the traffic. Istio supports two types of gateways:

1. **Kubernetes Ingress Gateway**: It is a Kubernetes resource that exposes HTTP and HTTPS routes from outside the cluster to services within the cluster. We can use the Kubernetes Ingress Gateway to route traffic to services within the cluster. 

2. **Istio Gateway**: When we install Istio, it installs two types of gateways: Ingress Gateway and Egress Gateway along with istiod in the Control Plane.

    - **Ingress Gateway**: It is used to manage incoming traffic from outside the cluster to services within the cluster. It is similar to Kubernetes Ingress Gateway but it is managed by Istio.
    
    - **Egress Gateway**: It is used to manage outgoing traffic from services within the cluster to outside the cluster. It is used to manage the traffic that is leaving the service mesh.


### Why Istio Gateway over Kubernetes Ingress Gateway?

Istio Gateway provides more features than Kubernetes Ingress Gateway. Some of the features are:

1. **Traffic Management**: Istio Gateway provides more advanced traffic management features like traffic splitting, traffic shifting, fault injection, etc.

2. **Security**: Istio Gateway provides more advanced security features like mutual TLS, rate limiting, etc.

3. **Observability**: Istio Gateway provides more advanced observability features like distributed tracing, monitoring, etc.


### How Istio Gateway works?

Let's understand how Istio Gateway works with an example:

- Consider a scenario where we have a microservices application running in the Kubernetes cluster. We have a frontend service, product service, and order service. We want to expose the frontend service to the outside world. We can use the Istio ingress gateway to expose the frontend service to the outside world.
- When a request comes from the outside world, it will first hits the Istio ingress gateway. The Istio ingress gateway will capture the traffic and route it to the frontend service with the help of Virtual Service and Destination Rule. Similarly, If any traffic is leaving the service mesh, it will hit the Istio egress gateway and the Istio egress gateway will manage the traffic.


### How to create an Istio Gateway?

Just like any other Kubernetes resource, we can create an Istio Gateway using a YAML file. Below is an example of an Istio Gateway:

```yaml
apiVersion: networking.istio.io/v1alpha3
kind: Gateway
metadata:
  name: httpbin-gateway
spec:
  # The selector matches the ingress gateway pod labels.
  # If you installed Istio using Helm following the standard documentation, this would be "istio=ingress"
  selector:
    istio: ingressgateway
  servers:
  - port:
      number: 80
      name: http
      protocol: HTTP
    hosts:
    - "httpbin.example.com"
```

In the above example, we are creating an Istio Gateway named `httpbin-gateway`. The gateway will serve traffic on port 80 and the host `httpbin.example.com`. Now, we can create a Virtual Service to route the traffic to the respective service.


Date of notes: 23/06/2024