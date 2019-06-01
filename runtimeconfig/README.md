# Cloud Runtime Configuration template

## Overview

This is a [Google Cloud Deployment Manager](https://cloud.google.com/deployment-manager/overview) template that deploys a [RuntimeConfig](https://cloud.google.com/deployment-manager/runtime-configurator/) resource, and a [Variables](https://cloud.google.com/deployment-manager/runtime-configurator/set-and-get-variables) list.

![Google DM Screenshot](./img/runtimeconfig.png)

## Notes for API explorer Runtime Configurator

To create a configuration ressource:

* parent: `projects/[PROJECT ID]`
* name: `projects/[PROJECT ID]/configs/[CONFIG NAME]`

To create a variable in a configuration ressource:

* parent: `projects/[PROJECT ID]/configs/[CONFIG NAME]`
* name: `projects/[PROJECT ID]/configs/[CONFIG NAME]/variables/[VARIABLE NAME]`

To check the deployment use the [runtimeconfig.projects.configs.variables.list](https://developers.google.com/apis-explorer/#p/runtimeconfig/v1beta1/runtimeconfig.projects.configs.variables.list) with the parent exported as an output in the deployment.

![Google DM Screenshot](./img/variables.png)

## Deploy the template

Use `runtimeconfig.yaml` to deploy this example template. When ready, deploy with the following command:

```
gcloud deployment-manager deployments create test-run-1 --config runtimeconfig.yaml
```

**`runtimeconfig.yaml`**

```
#  title: Runtime Config
#  author: osm.hammami@gmail.com
#  description: |
#    Creates a RuntimeConfig resource.
#  version: 0.1

imports:
  - path: runtimeconfig.jinja

resources:
  - name: test-deployment-1
    type: runtimeconfig.jinja
    properties:
      variables:
      - name: var1
        value: 192.168.1.1
      - name: var2
        value: 192.168.1.2
      - name: var3
        value: 192.168.1.3
```

### Deployment

```
# gcloud deployment-manager deployments create test-run-1 --config runtimeconfig.yaml
The fingerprint of the deployment is XXXXXXXXXXXXXXXXXXXXX
Waiting for create [operation-XXXXXXXXXXXXXXXXXXXXX]...done.
Create operation operation-XXXXXXXXXXXXXXXXXXXXX completed successfully.
NAME                                  TYPE                            STATE      ERRORS  INTENT
test-deployment-1-runtimeconfig       runtimeconfig.v1beta1.config    COMPLETED  []
test-deployment-1-runtimeconfig-var1  runtimeconfig.v1beta1.variable  COMPLETED  []
test-deployment-1-runtimeconfig-var2  runtimeconfig.v1beta1.variable  COMPLETED  []
test-deployment-1-runtimeconfig-var3  runtimeconfig.v1beta1.variable  COMPLETED  []
```



### References

* [API reference RuntimeConfig](https://cloud.google.com/deployment-manager/runtime-configurator/reference/rest/)
* [API explorer RuntimeConfig v1beta1](https://developers.google.com/apis-explorer/#p/runtimeconfig/v1beta1/)