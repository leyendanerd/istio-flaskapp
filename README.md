# istio-flaskapp

## Proceso de configuracion istio service + Cert-Manager en Deployment flaskci app 

## Concepts Gateway, VirtualService, DestinacionRule

![image](Screenshot_4.png)

### A Virtual Service: 

Defines how requests for a service are routed within an Istio service mesh. Can use routing rules to determine the destination 
to which a request should be sent, Can use rules to route traffic based on things like request headers, target host name, 
url path, etc.

### The Destination Rule: 

Defines how traffic aimed at a particular destination gets handled.Can break a single service into multiple subsets - in other words, subcollections of pods using labels to select. The VirtualService can then route to the subset Can specify load balancing behavior 
within the destination - random, round robin, weighted, etc. And it can specify TLS security mode, circuit breaker settings, etc.

### Gateways:

Gateways are used to manage inbound and outbound traffic for the mesh. The configuration settings are applied to a deployment on Envoy poxy pods running on the edge of the mesh, not as sidecars to particular workloads. A gateway can, for instance, allow incoming HTTP traffic for a specific host. You then bind a VirtualService to the Gateway, and the Gateway uses the VirtualService information to route the incoming request to the correct destination.

## Getting Started


### 1 Go to the Istio release page to download the installation file for your OS, or download and extract the latest release automatically (Linux or macOS):

curl -L https://istio.io/downloadIstio | sh -

### 2 Move to the Istio package directory. For example, if the package is istio-1.14.3:

cd istio-1.14.3

### 3 Add the istioctl client to your path (Linux or macOS):

export PATH=$PWD/bin:$PATH


# Install Istio

## Installation Configuration Profiles

This page describes the built-in configuration profiles that can be used when installing Istio. The profiles provide customization of the Istio control plane and of the sidecars for the Istio data plane.

You can start with one of Istio???s built-in configuration profiles and then further customize the configuration for your specific needs. The following built-in configuration profiles are currently available:

1.default: enables components according to the default settings of the IstioOperator API. This profile is recommended for production deployments and for primary clusters in a multicluster mesh. You can display the default settings by running the istioctl profile dump command.

2.demo: configuration designed to showcase Istio functionality with modest resource requirements. It is suitable to run the Bookinfo application and associated tasks. This is the configuration that is installed with the quick start instructions.

3.minimal: same as the default profile, but only the control plane components are installed. This allows you to configure the control plane and data plane components (e.g., gateways) using separate profiles.

4.external: used for configuring a remote cluster that is managed by an external control plane or by a control plane in a primary cluster of a multicluster mesh.

5.empty: deploys nothing. This can be useful as a base profile for custom configuration.

6.preview: the preview profile contains features that are experimental. This is intended to explore new features coming to Istio. Stability, security, and performance are not guaranteed - use at your own risk.

![image](https://user-images.githubusercontent.com/66542754/183929719-12c6b391-bd52-469d-8972-eb50e94c13e3.png)


### 1 Install isitio with profile

istioctl install --set profile=default -y


### 2 Add a namespace label to instruct Istio to automatically inject Envoy sidecar proxies when you deploy your application later:

kubectl label namespace default istio-injection=enabled

### Ensure that there are no issues with the configuration:

istioctl analyze 

istioctl analyze -namespace ns
