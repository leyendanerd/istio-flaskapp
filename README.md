# istio-flaskapp

## Proceso de configuracion istio service + Cert-Manager en Deployment flaskci app 

## Getting Started


### 1 Go to the Istio release page to download the installation file for your OS, or download and extract the latest release automatically (Linux or macOS):

curl -L https://istio.io/downloadIstio | sh -

### 2 Move to the Istio package directory. For example, if the package is istio-1.14.3:

cd istio-1.14.3

### 3 Add the istioctl client to your path (Linux or macOS):

export PATH=$PWD/bin:$PATH


# Install Istio

### 1 Install isitio with profile

istioctl install --set profile=default -y


### 2 Add a namespace label to instruct Istio to automatically inject Envoy sidecar proxies when you deploy your application later:

kubectl label namespace default istio-injection=enabled

### Ensure that there are no issues with the configuration:

istioctl analyze 

istioctl analyze -namespace ns