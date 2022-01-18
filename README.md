# Deploying Application to OpenShift

```
oc new-project hello-hackfest
oc apply -f src/main/openshift/manifests
oc new-app -i hello-hackfest/hello-hackfest:latest --allow-missing-imagestream-tags=true --as-deployment-config=true
oc new-app -i hello-hackfest/hello-hackfest-native --allow-missing-imagestream-tags=true --as-deployment-config=true
```