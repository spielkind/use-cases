MCSPS use cases
===============

Demos and use cases for MCSPS

Simple demo app
---------------

* creates configmap for nginx content
* creates 2 pods from nginx image
* creates service
* creates ingress
* deploys DNS entry with external-dns app
* deploys LetsEncrypt cert with cert-manager and letsencrypt-prod issuer

Change cluster name and app name in CHANGEME lines!

Create:

```
kubectl create namespace demoapp
kubectl apply -f demoapp.yaml -n demoapp
```

Destroy:

```
kubectl delete -f demoapp.yaml -n demoapp
kubectl delete namespace demoapp
```

Storage demo
------------


Like Simple demo app

* creates SATA pvc
* mount pvc to pods

Create:

```
kubectl create namespace demoapp
kubectl apply -f demoapp_volume.yaml -n demoapp
POD=$(kubectl  get pods -n demoapp  --no-headers | tail -1 | awk '{print $1}')
kubectl cp README.md demoapp/$POD:/usr/share/nginx/html/
curl https://<app_name>/README.md
```

Delete:

```
kubectl delete -f demoapp_volume.yaml -n demoapp
kubectl delete namespace demoapp
```
