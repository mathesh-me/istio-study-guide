## Circuit Breaking

Circuit breaking in istio help us to prevent the cascading failures in the service mesh. Circuit breaking is used to stop sending requests to a service that is failing. **It is used to prevent the service from getting overwhelmed by the requests**.<br>

### Why Circuit Breaking?

Let's consider a scenario where a service is failing and the client is sending requests to the failing service. If the client keeps sending requests to failing service, it will overwhelm the service and the service will fail completely. To prevent this we can use circuit breaking.
We can limit the number of requests sent to the failing service. If the number of requests exceeds the limit, the circuit will break and the client will stop sending requests to the failing service. This will prevent the service from getting overwhelmed and failing completely. 

### How to set Circuit Breaking in Istio?

We can set circuit breaking in Istio using the `connectionPool` field in the DestinationRule. Below is an example of setting circuit breaking in Istio:

```yaml
apiVersion: networking.istio.io/v1alpha3
kind: DestinationRule
metadata:
  name: httpbin
spec:
  host: httpbin
  trafficPolicy:
    connectionPool:
      tcp:
        maxConnections: 1 
      http:
        http1MaxPendingRequests: 1 
        maxRequestsPerConnection: 1 
        maxRetries: 1
```

In the above example, we are setting circuit breaking for the service `httpbin`. We are limiting the number of connections to 1, the number of pending requests to 1, the number of requests per connection to 1, and the number of retries to 1. If the number of connections, pending requests, requests per connection, or retries exceeds the limit, the circuit will break and the client will stop sending requests to the service `httpbin`.<br>

**Some of the important fields in the `connectionPool` are:**

1. `maxConnections`: The maximum number of connections to the service.
2. `http1MaxPendingRequests`: The maximum number of pending requests to the service.
3. `maxRequestsPerConnection`: The maximum number of requests per connection to the service.
4. `maxRetries`: The maximum number of retries for the requests to the service.

Now we can test how our application behaves when there are circuit breaking in the request/response.

Date of notes: 23/06/2024