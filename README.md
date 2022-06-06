## How to deploy web service in Kubernetes ?
Firstly, make sure that Kubernetes and Docker are installed locally into your machine.

**For Security Reasons, the secret api key for Alphavantage not included within this repository. Without proper API KEY the program will not run.**

To put a real API KEY follow instruction below:
1. Encode the plain text API KEY to it is base64 encoded value by running command:

````
echo -n 'API KEY CONTENT' | base64
````

2. Replace the content of ``secret.yaml`` fields:
````
data:
  apikey: HERE_REPLACE_WITH_OUTPUT_OF_STEP_1
````

3. After following above instructions then, please run the following command to deploy web service

````

kubectl apply -f namespace.yaml -f secret.yaml -f config-map.yaml -f service.yaml -f ingress.yaml  -f deployment.yaml

````

4. Ingress has host which must be tunneled locally with the help of minikube, by following below instructions.

Add ``127.0.0.1 forgerock-app.local`` in the end of file ``/etc/hosts`` by running the following command

````
sudo vim /etc/hosts
````

Installing Minikube and running tunel
````
https://minikube.sigs.k8s.io/docs/start/

minikube start

minikube tunnel
````

Tunnel creates a route to services deployed with type LoadBalancer and sets their Ingress to their ClusterIP