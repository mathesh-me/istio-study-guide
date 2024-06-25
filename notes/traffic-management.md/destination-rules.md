## Destination Rules

**Destination rules are used to apply policies to the traffic after the traffic has been routed to a service by a virtual service**. Destination rules are used to configure the load balancing, mutual TLS, connection pool size, outlier detection, etc. Destination rules are used to configure the traffic policies for the services within the service mesh. Also there is `subset` concept in destination rules which is used to route the traffic to specific versions of the service to do A/B testing, canary deployments, etc.

### How to create a Destination Rule?

We can create a Destination Rule using a YAML file.

1. **For Load Balancing:**

```yaml
apiVersion: networking.istio.io/v1
kind: DestinationRule
metadata:
  name: bookinfo-ratings
spec:
  host: ratings.prod.svc.cluster.local
  trafficPolicy:
    loadBalancer:
      simple: LEAST_REQUEST
```

In the above example, we are creating a Destination Rule named `bookinfo-ratings`. The Destination Rule will apply the load balancing policy `LEAST_REQUEST` to the service `ratings.prod.svc.cluster.local`. Default load balancing policy is `ROUND_ROBIN`.

2. **For a Client-side TLS(It will make the client to send the request to the server using TLS):**

```yaml
apiVersion: networking.istio.io/v1
kind: DestinationRule
metadata:
  name: bookinfo-ratings
spec:
  host: ratings.prod.svc.cluster.local
  trafficPolicy:
    tls:
      mode: SIMPLE # We can Specify MUTUAL to configure mutual TLS
```

In the above example, we are creating a Destination Rule named `bookinfo-ratings`. The Destination Rule will apply the TLS mode `SIMPLE` to the service `ratings.prod.svc.cluster.local`. The `SIMPLE` mode will make the client to send the request to the server using TLS.

3. **For A/B Testing:**

Let's consider the Bookinfo application by Istio. It have a services called productpage, details, reviews, ratings, etc. Let's say we have two versions of the reviews service, version v1 and version v2. We want to route 80% of the traffic to v1 and 20% of the traffic to v2. We can use destination rules to do this.

Now we are going to start from Virtual Service and Destination Rule for the A/B Testing.

```yaml
apiVersion: networking.istio.io/v1
kind: VirtualService
metadata:
  name: reviews-route
spec:
  hosts:
  - reviews.prod.svc.cluster.local
  http:
  - name: "reviews-v2-routes"
    match:
    - uri:
        prefix: "/wpcatalog"
    - uri:
        prefix: "/consumercatalog"
    rewrite:
      uri: "/newcatalog"
    route:
    - destination:
        host: reviews.prod.svc.cluster.local
        subset: v2
      weight: 80
  - name: "reviews-v1-route"
    route:
    - destination:
        host: reviews.prod.svc.cluster.local
        subset: v1
       weight: 20
```

In the above example, we are creating a Virtual Service named `reviews-route`. The Virtual Service will route 80% of the traffic to the subset `v1` and 20% of the traffic to the subset `v2`.

Now we are going to create a Destination Rule for the subsets.

```yaml
apiVersion: networking.istio.io/v1
kind: DestinationRule
metadata:
  name: reviews-destination
spec:
  host: reviews.prod.svc.cluster.local
  subsets:
  - name: v1
    labels:
      version: v1
  - name: v2
    labels:
      version: v2
```

In the above example, we are creating a Destination Rule named `reviews`. The Destination Rule will create two subsets `v1` and `v2` for the service `reviews.prod.svc.cluster.local`. The subset `v1` will have the label `version: v1` and the subset `v2` will have the label `version: v2`.<br>

Now our traffic between the reviews service will be routed to the subsets v1 and v2 based on the weights we defined in the Virtual Service(80% to v1 and 20% to v2). This is how we can do A/B Testing using Virtual Service and Destination Rule.<br>

These are just few examples of Destination Rules. We can do many more things using Destination Rules like setting connection pool size, outlier detection, etc.<br>

**Reference**: [Istio Documentation](https://istio.io/latest/docs/reference/config/networking/destination-rule/)

Date of notes: 23/06/2024
