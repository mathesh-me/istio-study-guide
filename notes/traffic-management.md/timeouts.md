## Timeouts in Istio

### Why Timeouts?

Let's consider a Scenario where we have a microservices application running in our cluster. We have a product page, details page, and reviews page. The product page will call the details page and the reviews page. Now let's say the details page is down. It will make my request to the details page from product page to wait for a long time. This will make my product page to wait for a long time. This is not a good user experience. To overcome this problem, we can use timeouts in Istio.

### What is Timeout?

Timeout is the maximum time a service or client will wait for a response from the another service or server. If the response is not received within the specified time, the request will be considered as failed.

### How to set Timeout in Istio?

We can set timeouts in Istio using the `timeout` field in the Virtual Service. Below is an example of setting a timeout in Istio:

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
    timeout: 5s
```

In the above example, we are setting a timeout of 5 seconds for the service `details.prod.svc.cluster.local`. If the service `details.prod.svc.cluster.local` does not respond within 5 seconds, the request will be considered as failed.

Date of notes: 23/06/2024