## Virtual Service

**Virtual service is a custom resource in Istio that defines a set of rules for routing the incoming traffic to the appropriate destination within the service mesh. It is used to configure the routing rules for the incoming traffic.** It has many features like traffic management, fault injection, retries, timeouts, etc. When a virtual service is created, control plane will configure the sidecar proxies to route the traffic according to the rules we defined in the virtual service.

### How to create a Virtual Service?

We can create a Virtual Service using a YAML file.

```yaml
apiVersion: networking.istio.io/v1alpha3
kind: VirtualService
metadata:
  name: httpbin
spec:
  hosts:
  - "httpbin.example.com"
  gateways:
  - httpbin-gateway # To associate the Virtual Service with the Gateway
  http:
  - match:
    - uri:
        prefix: /status
    - uri:
        prefix: /delay
    route:
    - destination:
        port:
          number: 8000
        host: httpbin
```

In the above example, we are creating a Virtual Service named `httpbin`. The Virtual Service will route the traffic with the host `httpbin.example.com` to the destination service `httpbin` on port `8000`. It will match the URIs with prefixes `/status` and `/delay` and route the traffic accordingly. The Virtual Service is associated with the Gateway `httpbin-gateway`(must be created before creating the Virtual Service).

Date of notes: 23/06/2024