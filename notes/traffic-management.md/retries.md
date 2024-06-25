## Retries 

Retries are used to retry the failed requests. We can configure the number of retries, timeout between the retries, etc. in the Virtual Service. For example, if a request to a service fails, we can retry the request for a specified number of times. 

### How to set Retries in Istio?

We can set retries in Istio using the `retries` field in the Virtual Service. Below is an example of setting retries in Istio:

```yaml
apiVersion: networking.istio.io/v1alpha3
kind: VirtualService
metadata:
  name: productpage
spec:
  hosts:
  - productpage.prod.svc.cluster.local
  http:
  - route:
    - destination:
        host: details.prod.svc.cluster.local
    retries:
      attempts: 3
      perTryTimeout: 2s
```

This Virtual Service will make our service `productpage.prod.svc.cluster.local` to retry the request to the service `details.prod.svc.cluster.local` for 3 times with a timeout of 2 seconds between each retry. Now we can test how our application behaves when there are retries in the request/response.

Date of notes: 23/06/2024