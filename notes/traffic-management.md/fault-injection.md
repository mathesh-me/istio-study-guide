## Fault Injection in Istio

**Fault Injections are used to test our application resiliency. We can inject faults like delays, aborts. To test how our application behaves in case of failures**. Fault Injection is a powerful tool to test our application resiliency by simulating failures.

### Types of Fault Injections

1. **Delay Injection**: Delays are used to delay the request/response. 

2. **Abort Injection**: Abort Injection is used to abort the request/response.

We can do the above two types of fault injections using to particular number of requests and also for a particular percentage of requests. 

### How to do Fault Injection in Istio?

1. **Delay Injection**:

```yaml
apiVersion: networking.istio.io/v1alpha3
kind: VirtualService
metadata:
  name: httpbin-delay
spec:
  hosts:
  - httpbin.example.com
  http:
  - route:
    - destination:
        host: httpbin
    fault:
      delay:
        percentage:
          value: 50
        fixedDelay: 7s
```

This Virtual Service will inject a delay of 7 seconds for 50% of the requests to the service `httpbin`. Now we can test how our application behaves when there is a delay in the request/response.

2. **Abort Injection**:

```yaml
apiVersion: networking.istio.io/v1alpha3
kind: VirtualService
metadata:
  name: httpbin-abort
spec:
  hosts:
  - httpbin.example.com
  http:
  - route:
    - destination:
        host: httpbin
    fault:
      abort:
        percentage:
          value: 50
        httpStatus: 500
```

Now if we apply this Virtual Service, 50% of the requests to the service `httpbin` will be aborted with the HTTP status code 500. Now we can test how our application behaves when there is an abort in the request/response.

### How to remove Fault Injection?

If we want to remove the fault injection, we have to delete the Virtual Service that we created for the fault injection.

Date of notes: 23/06/2024