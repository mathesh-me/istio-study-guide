## Authentication in Istio

![istio-authentication](https://github.com/mathesh-me/istio-study-guide/assets/144098846/5c1a7088-b490-4682-a9dc-19bb3f499fdf)


We know in Microservices architecture, Multiple services are communicating with each other. One service must know that the service it is communicating with is the correct service. To make sure that the services are communicating with each other securely, we need to implement some authentication mechanism.<br>

Istio Support two types of authentication mechanisms:

1. **Mutual TLS Authentication for Sevices**: We can enable mutual TLS authentication for the services in the mesh. In this mechanism, each service will have a identity and a certificate. The service will use the certificate to authenticate itself to the other services in the mesh. 

2. **Request Authentication for End Users**: We can enable request authentication for the end users. In this mechanism, we can authenticate the end users before they access the services in the mesh. We can use JWT and OpenID Connect to authenticate the end users.

### How to enable Mutual TLS Authentication in Istio?

We can enable mutual TLS authentication in Istio using the `PeerAuthentication` resource. Below is an example of enabling mutual TLS authentication in Istio:

1. **Workload-Specific PeerAuthentication**:

```yaml
apiVersion: security.istio.io/v1beta1
kind: PeerAuthentication
metadata:
  name: reviews-peer-authentication
  namespace: default
spec:
  selector:
    matchLabels:
      app: reviews
  mtls:
    mode: STRICT
```

The above manifest is a example of `Workload-Specific` PeerAuthentication policy. It will enable mutual TLS authentication for the service `reviews`. The `mode: STRICT` will enforce the mutual TLS authentication for the service `reviews`. It will only act on the services with the label `app: reviews` which means if the service `reviews` is communicating with other services, it will enforce the mutual TLS authentication. But not the other service have a need to enforce the mutual TLS authentication.

2. **Namespace-Wide PeerAuthentication**:

```yaml
apiVersion: security.istio.io/v1beta1
kind: PeerAuthentication
metadata:
  name: reviews-peer-authentication
  namespace: default
spec:
  mtls:
    mode: STRICT
```

It will be applied to all the services in the namespace `default`. It will enforce the mutual TLS authentication for all the services in the namespace `default`.

3. **Mesh-Wide PeerAuthentication**:

```yaml
apiVersion: security.istio.io/v1beta1
kind: PeerAuthentication
metadata:
  name: default
  namespace: istio-system
spec:
  mtls:
    mode: STRICT
```

Date of notes: 24/06/2024
