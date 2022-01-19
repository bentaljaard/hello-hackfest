# Pre-requisites

## Install multiarch deamonset on OpenShift

In order for this application to run on OpenShift, please be sure to install the qemu-user-static deamonset from the https://github.com/qiot-project/qiot-multiarch-ocp repo. This will enable the platform to run multiarch containers.


## Notes on Storage Classes

In order for MVN dependencies to be cached properly, persistent volumes need a storage class that allows volumes to be retained. Create a new strage class on your target environment that specifies the reclaimPolicy as Retain and update the Persistent Volume Claim manifests with your new storage class. The exmaples in this repo assumes you are using the local storage operator and therefore references a local storage class. Typically when you deploy on OpenShift running on AWS you would need to create a GP2 storage class that specifies the retain policy as mentioned above.


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

* Run either the hello-hackfest or hello-hackfest-native pipeline. When initiating the pipeline, specify the appropriate persistent volume claims as parameters.
* Find the route for the application
* Call the /hello endpoint

