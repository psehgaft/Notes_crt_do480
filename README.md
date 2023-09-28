# Notes_crt_do480
Notes_crt_do480

# Multicluster Application Resource Management with RHACM

## Users

Roles

open-cluster-management:managedclusterset:admin:clusterset_name
open-cluster-management:managedclusterset:view:clusterset_name

```sh
oc adm policy add-cluster-role-to-user open-cluster-management:managedclusterset:admin:prod user

oc adm policy add-cluster-role-to-user open-cluster-management:managedclusterset:view:dev user
```

# Customizing resources with Kustomize for RHACM

Kustomize from scratch
Override the image for a specific environment
Add a namePrefix
Deploy an application from git, from 2 different branches (dev and prod)

```yml
#Production
apiVersion: kustomize.config.ks8.io/v1beta1
kind: Kustomization
 commonLabels:
  app: prod-todolist.js

#path to base directory
bases:
- ../../base

resources:
- pvclaim,yml

#Add name prefix "prod"
namePrefix: prod-

#Production
patchesStrategicMerge:
  - pvc.yaml
```



```yml
#Development
apiVersion: kustomize.config.ks8.io/v1beta1
kind: Kustomization
#Development
commonLabels:
  app: dev-todolist.js

#path to base directory
bases:
  - ../../base

resources:
- pvclaim,yml
- route.yml

#Development
images:
  - name: mysql-db-image
    newName: quay.io/example/todo-single
    newTag: v2.0-beta

#Add name prefix "dev"
namePrefix: dev-
```

# ACS - how to import cluster

# Create and configure Syslog integration

#  Make image show up via "Scanning via watch tag"
