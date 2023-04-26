# clubwind-helmcharts

The Lucdoe.de application runs on a Kubernetes cluster on the Google Cloud Platform (GCP). The cluster consists of three nodes hosting multiple Kubernetes objects, including a MongoDB database, a Redis cache, an Express.js application, and an NGINX ingress controller. The application is accessible through the domain name https://lucdoe.de.

The Express.js applications are deployable using a Helm chart running in its namespace. The chart includes a deployment object that specifies the number of replicas, a service object that exposes the application to the Kubernetes cluster, and a network policy object that restricts traffic to and from the application. The chart also includes a role object that defines the permissions required by the application.
The MongoDB and Redis databases are deployed using Helm charts in the same namespace as the Express.js application.

The NGINX ingress controller is deployed using a Helm chart in its namespace. The chart includes a deployment object that specifies the number of replicas and a service object that exposes the controller to the Kubernetes cluster. Each outward-facing service uses this Ingress controller with its specific settings.
Cert Manager is deployed using a Helm chart in its namespace. The applications each also include a cluster issuer object defining the TLS certificates' issuer.

When an ingress object is created for the Express.js application, Cert Manager automatically creates a certificate object and requests a TLS certificate from the issuer defined in the cluster issuer object. The TLS certificate is then used to secure the traffic to and from the application (HTTPS).
The Sonarqube instance is deployed using a Helm chart in its namespace. The chart includes
a deployment,
a service object that exposes the Sonarqube instance to the Kubernetes cluster, and
a PostgreSQL database that stores the Sonarqube data.
The Sonarqube instance is accessible through the domain name https://sonarqube.lucdoe.de.

The documentation for the express codebase application is hosted on a Google Cloud Storage bucket under the domain name https://docs.lucdoe.de. The documentation is generated using Typedoc, and copied to the bucket as part of the deployment process.
Overall, the Lucdoe.de application is deployed using multiple Helm charts, each defining the Kubernetes objects required to run the application. The charts are deployed to their namespaces to provide isolation and simplify the management of the application. A running example of the application are accessible through the domain names https://lucdoe.de and https://sonarqube.lucdoe.de, respectively, while the documentation is accessible through https://docs.lucdoe.de.

## Prerequisites

1. [Install gcloud CLI](https://cloud.google.com/sdk/docs/install)
2. Authenticate running: `gcloud auth login`
3. Set current project: `gcloud config set project express-kubernetes-384308`

## Installing the charts

helm install express-release . -n express --create-namespace
helm install sonar-release . -n sonar --create-namespace

## Updating the charts

helm upgrade express-release . -n express --create-namespace
helm upgrade sonar-release . -n sonar --create-namespace

## Uninstalling the charts

helm uninstall express-release -n express
helm uninstall sonar-release -n sonar

## Architecture

Here is an Diagramm of the cloud architecture:

![Architecture](https://github.com/lucdoe/clubwind-helmcharts/blob/main/Cloud-Diagramm.png?raw=true)
