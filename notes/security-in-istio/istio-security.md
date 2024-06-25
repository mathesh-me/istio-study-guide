## Istio Security Introducton

When we consider about microservices, Each service in the microservices architecture is communicating with each other. The communication between the services should be secure. There is a possible chance of attackers to intercept the communication between the services. To overcome this problem, **we need to encrypt the communication between the services**. Also we need to implement some authorization to make sure that the services are communicating with each other securely.


### Istio Security Architecture

![Istio-Security-Architecture](https://github.com/mathesh-me/istio-study-guide/assets/144098846/dd9e261b-a6e9-4740-835d-c4e670accb53)


#### Components of Istio Security:

1. **Certificate Authority in `Istiod`**: Responsible for managing keys and certificates for the services in the mesh. It will also validate the CSR(Certificate Signing Request) from the services and issue the certificates to the services.

2. **API Server Configuration:** Responisble for distributing the authentication, authorization, and other security policies to the sidecar proxies.

3. **Envoys(Sidecars and Ingress/Egress Gateways):** Will acts as Policy Enforcement Points. Every Points will have some security check.a

Date of notes: 24/06/2024
