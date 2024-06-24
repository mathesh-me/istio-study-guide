## Kiali

**Kiali is a web-based console for Istio.** It provides us with a visual representation of the service mesh. Kiali helps us to understand the structure of the service mesh, the traffic flow between the services, and the health of the services. We can consider Kiali as a monitoring tool for Istio and also as a visualization tool for Istio.

### Installating Kiali

- Run the below command to install Kiali:

```bash
kubectl apply -f samples/addons
kubectl rollout status deployment/kiali -n istio-system
```

- Run the below command to access the Kiali dashboard:

```bash
istioctl dashboard kiali
```
It will open the Kiali dashboard in the browser.

### Kiali Dashboard

To see the full capabilities of Kiali, we need to send some traffic to the services in the service mesh. We can use the Bookinfo application to send some traffic to the services. We must need to send atleast 100 requests to our application.

- To send 100 requests to the Bookinfo application Product page, run the below command:

```bash
for i in $(seq 1 100); do curl -s -o /dev/null "http://$GATEWAY_URL/productpage"; done
```

Now we can see the Kiali dashboard with the traffic flow between the services. 

Date of Notes: 23/06/2024