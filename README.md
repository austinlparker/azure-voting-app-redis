# Azure Voting App (With OpenTelemetry and Ambassador)

This is a sample application that demonstrates using several technologies (Azure Kubernetes Service, OpenTelemetry, Ambassador) in conjunction to help you understand tracing via ingress.

To run this demo yourself, you'll need to perform the following steps:

1. Create an AKS cluster.
2. Use the [K8s Initializer](https://app.getambassador.io/initializer/) to bootstrap your new cluster with Ambassador and OpenTelemetry.
3. Deploy the application and it's route mapping using the manifests in `./kubernetes`
4. View traces in Jaeger (or Lightstep)

## What's happening here?

As you may know, Kubernetes offers isolated network namespaces and IP ranges for pods that are running inside a cluster. This makes it somewhat simpler to create and manage applications, but also leads to its own share of challenges as well. Managed Kubernetes clusters will typically use a load balancer external to the cluster (operating at layer 4, or TCP) to route traffic to various service endpoints that are defined by an ingress controller (which operates at layer 7, or HTTP). The ingress controller then routes traffic to pods on the cluster. 

Tools such as Ambassador fulfill the role of an ingress controller, but offer more features and functionality than the built-in Ingress resource. For example, it can manage TLS termination, handle timeouts and rate limiting, and perform authentication for APIs. It performs this using tools like Envoy, an open source proxy server. In addition to the aforementioned features, Envoy is capable of initiating or continuing distributed traces. A distributed trace is a form of application telemetry, which you can use to pinpoint performance problems or bugs - a trace records every step in a request, from service to service, pinpointing exactly how long each step takes.

In this example, we're using Ambassador to originate our traces. This means that every incoming request will start a new trace. The _trace context_ is then embedded in the HTTP headers of the request as it's forwarded from Envoy to our frontend voting service. The service code is then _instrumented_ using [OpenTelemetry](https://opentelemetry.io). Instrumentation is the process of adding telemetry code to an application. In this case, we're taking advantage of automatic instrumentation - libraries that will automatically add tracing code to the frameworks and clients that we're using.

