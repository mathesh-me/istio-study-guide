## Installing Istio

For installing istio, We need to install `istioctl` which is the command line utility for Istio. `istioctl` is used to install, manage, and configure Istio.

### Installing istioctl

Run the below commands to download and install `istioctl`:

```bash
curl -L https://istio.io/downloadIstio | sh -
cd istio-1.22.0
```
This installation will contain the `istioctl` client in the `bin` directory of the Istio installation directory.

Add the `istioctl` client to your PATH:

```bash
export PATH=$PWD/bin:$PATH
```

### Install Istio

Now, we can install Istio using the `istioctl` command. Run the below command to install Istio:

```bash
istioctl install --set profile=demo -y
```
We are installing the `demo` profile of Istio. The `demo` profile is used for demonstration purposes. It is not recommended for production use. There are separate profiles available for production and testing.

### Verify the installation

Run the below command to verify the installation:

```bash
istioctl verify-install
```

### Add a namespace label

If we want istio to add sidecar containera to our pods automatically, we need to add a label to the namespace where we want to deploy our application. This label will instruct Istio to automatically inject the sidecar proxy into the application pods.

```bash
kubectl label namespace default istio-injection=enabled
```

### Deploying the Bookinfo sample application

- Bookinfo is a sample application by Istio. It is a simple application that consists of four microservices. The application is used to demonstrate the features of Istio.

```bash
kubectl apply -f samples/bookinfo/platform/kube/bookinfo.yaml
```

- Run the below command to verify the running of application:

```bash
kubectl exec "$(kubectl get pod -l app=ratings -o jsonpath='{.items[0].metadata.name}')" -c ratings -- curl -sS productpage:9080/productpage | grep -o "<title>.*</title>"
```

- Open the application to outside traffic

```bash
kubectl apply -f samples/bookinfo/networking/bookinfo-gateway.yaml
```

-  Now, we have to determine the ingress IP and ports to access the application. There are different ways to determine the ingress IP and ports based on the platform you are using. Refer to the [Istio documentation](https://istio.io/latest/docs/tasks/traffic-management/ingress/ingress-control/#determining-the-ingress-ip-and-ports) for more information.

- Once you have determined the ingress IP and ports, open the application in the browser using the below URL:

```bash
http://<INGRESS_IP:PORT>/productpage
```

Now, We can see the Bookinfo application running successfully.

Date of notes: 23/06/2024