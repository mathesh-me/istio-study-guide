## Authorization in Istio

![istio-authorization](https://github.com/mathesh-me/istio-study-guide/assets/144098846/b07e236a-e115-4926-b370-b2e48dfb2297)


**Authorization helps us to control access to services in the mesh**. For example, Consider a scenario where we have a product service, details service, and ratings service. Now we want only our details service can be able to access the ratings service. If we try to access the ratings service from the product service, it should not be allowed. This is where the authorization comes into the picture. We can define the authorization policies in the Istio to control the access to the services. We can also restrict the methods like GET, POST, PUT, DELETE, etc. for the services. For example, we can allow only the GET method for the details service to access the ratings service. These authorization mechanisms are implemented in the sidecar proxies by authorization engine. When a request comes to the service, authorization engine will check the request against the authorization policies defined in the Istio.

### How to Create Authorization Policies

We can create the authorization policies in the Istio using the `AuthorizationPolicy` resource. The `AuthorizationPolicy` resource is used to define the authorization policies in the Ist

```yaml
apiVersion: security.istio.io/v1beta1
kind: AuthorizationPolicy
metadata:
  name: ratings-policy
  namespace: default
spec:
  selector:
    matchLabels:
      app: ratings
  action: ALLOW
  rules:
  - from:
    - source:
        principals: ["cluster.local/ns/default/sa/details"]
    to:
    - operation:
        methods: ["GET"]
```

In the above policy, We are only allowing access to the ratings service from the details service. We are allowing only the GET method to access the ratings service.

Date of notes: 24/06/2024
