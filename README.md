# Deploying Application to OpenShift

```
oc new-project hello-hackfest
oc apply -f src/main/openshift/manifests
oc new-app -i hello-hackfest/hello-hackfest:latest --allow-missing-imagestream-tags=true --as-deployment-config=true
oc new-app -i hello-hackfest/hello-hackfest-native --allow-missing-imagestream-tags=true --as-deployment-config=true
oc expose dc hello-hackfest --port 8080
oc expose dc hello-hackfest-native --port 8080
oc expose svc hello-hackfest
oc expose svc hello-hackfest-native
```

# Verifying on OpenShift

* Run either the hello-hackfest or hello-hackfest-native pipeline
* Find the route for the application
* Call the /hello endpoint