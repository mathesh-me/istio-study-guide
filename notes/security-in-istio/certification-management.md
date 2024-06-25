## Certification Management in Istio


### How Certification Management Done in Istio?

![Certification-Management](https://github.com/mathesh-me/istio-study-guide/assets/144098846/60f485d0-0e9b-4d53-b629-b8199c530025)


1. When a workload is started in the service mesh, it needs to prove its identity in the mesh. The `istio-agent` deployed along with sidecar proxy
will generate a key pair and CSR for Envoys. And it will send Certificate Signing Request(CSR) to the Istio Citadel in control Plane. 
2. The Citadel will validate the CSR and issue a certificate to the Envoy. Now if two services want to communicate with each other, the sidecar proxy will use the certificate to prove its identity to the other services in the mesh. Certificates expiration will be managed by repeating this process of certificate issuance.
3. The Citadel will also manage the keys and certificates for the services in the mesh. Then the `istio-agent` will load the certificate and key into the workload's sidecar proxy. The sidecar proxy will use the certificate to prove its identity to the other services in the mesh.
4. Certificates expiration will be managed by repeating this process of certificate issuance.

Date of notes: 24/06/2024
