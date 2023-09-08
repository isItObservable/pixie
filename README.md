# Is it Observable
<p align="center"><img src="/image/logo.png" width="40%" alt="Is It observable Logo" /></p>

## Episode : WHat is Pixie
This repository contains the files utilized during the tutorial presented in the dedicated IsItObservable episode related Pixie.
<p align="center"><img src="/image/prixie_transparent.png" width="40%" alt="Pixie Logo" /></p>

This repository showcase the usage of Pixie  with :
* The OpenTelemetry demo
* Dynatrace


We will send all Telemetry data produced by Pixie to Dynatrace.

## Prerequisite
The following tools need to be install on your machine :
- jq
- kubectl
- git
- gcloud ( if you are using GKE)
- Helm


## Deployment Steps in GCP

You will first need a Kubernetes cluster with 2 Nodes.
You can either deploy on Minikube or K3s or follow the instructions to create GKE cluster:
### 1.Create a Google Cloud Platform Project
```shell
PROJECT_ID="<your-project-id>"
gcloud services enable container.googleapis.com --project ${PROJECT_ID}
gcloud services enable monitoring.googleapis.com \
    cloudtrace.googleapis.com \
    clouddebugger.googleapis.com \
    cloudprofiler.googleapis.com \
    --project ${PROJECT_ID}
```
### 2.Create a GKE cluster
```shell
ZONE=europe-west3-a
NAME=isitobservable-pixie
gcloud container clusters create "${NAME}" --zone ${ZONE} --machine-type=e2-standard-4 --num-nodes=2
```


## Getting started
### Dynatrace Tenant
#### 1. Dynatrace Tenant - start a trial
If you don't have any Dyntrace tenant , then i suggest to create a trial using the following link : [Dynatrace Trial](https://bit.ly/3KxWDvY)
Once you have your Tenant save the Dynatrace tenant url in the variable `DT_TENANT_URL` (for example : https://dedededfrf.live.dynatrace.com)
```
DT_TENANT_URL=<YOUR TENANT Host>
```

#### 2. Create the Dynatrace API Tokens
Create a Dynatrace token with the following scope ( left menu Acces Token):
* ingest metrics
* ingest OpenTelemetry traces
* ingest logs
<p align="center"><img src="/image/data_ingest.png" width="40%" alt="data token" /></p>
Save the value of the token . We will use it later to store in a k8S secret

```
DATA_INGEST_TOKEN=<YOUR TOKEN VALUE>
```

### 2.Clone the Github Repository
```shell
https://github.com/isItObservable/pixie
cd pixie
```

### 4. Create a Pixie Community Cloud account
Visit our [pixie's page](https://work.withpixie.ai/) and sign up.

### 5. Install the Pixie Cli
```shell
# Copy and run command to install the Pixie CLI.
bash -c "$(curl -fsSL https://withpixie.ai/install.sh)"
```

### 6. Deploy the otelDemo application 
d ..
chmod 777 deployment.sh
./deployment.sh  --dturl "${DT_TENANT_URL}" --dtingesttoken "${DATA_INGEST_TOKEN}"


### 7. Install Vizier
```shell
px deploy
```

### 7. Customize the OpenTelemetry Plugin
