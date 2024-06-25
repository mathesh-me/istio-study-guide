## Observability with Istio

**Istio provides a good observability feature to collect real telemetry data from the services in the mesh.** Since all the traffic in the mesh is controlled by the sidecar proxy, it can collect the telemetry data from the services. The telemetry data includes metrics, logs, and traces. The telemetry data can be used to monitor the services, troubleshoot the issues, and optimize the performance of the services.

1. **Visualization**: Istio provides support for collecting metrics and visualizing the metrics using tools like Grafana, Kiali, and Prometheus. By default, Istio standaed metrics will be exported by Prometheus. Integrating our servish mesh metrics with `Prometheus` and `Grafana` will provide a better visualization of the metrics.

2. **Tracing**: Istio provides support for distributed tracing using Jaeger, Zipkin, Datadog and Lightstep. Istio enable distributed tracing by envoy sidecar proxy. Distributed tracing tools will help us to individual requests, dependencies, and latencies of the services in the mesh.

![istio-observability](https://github.com/mathesh-me/istio-study-guide/assets/144098846/76aa229d-dd92-494c-b0ac-e57fb907b5af)


### Starting Observability

We can install the observability tools like Prometheus, Grafana, Jaeger, and Kiali using the addons manifest provided by Istio. The addons manifest will install the observability tools in the `istio-system` namespace.

```bash
$ kubectl apply -f https://raw.githubusercontent.com/istio/istio/release-1.9/samples/addons/prometheus.yaml
$ kubectl apply -f https://raw.githubusercontent.com/istio/istio/release-1.9/samples/addons/grafana.yaml
$ kubectl apply -f https://raw.githubusercontent.com/istio/istio/release-1.9/samples/addons/jaeger.yaml
$ kubectl apply -f https://raw.githubusercontent.com/istio/istio/release-1.9/samples/addons/kiali.yaml
```

### Accessing the Observability Tools

1. **Prometheus**:

```bash
istioctl dashboard prometheus
```

2. **Grafana**: 

```bash
istioctl dashboard grafana
```

3. **Jaeger**:

```bash
istioctl dashboard jaeger
```

4. **Kiali**:

```bash
istioctl dashboard
```

Date of notes: 24/06/2024
