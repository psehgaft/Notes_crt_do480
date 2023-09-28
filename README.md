# Notes_crt_do480
Notes_crt_do480

# Multicluster Application Resource Management with RHACM


# Customizing resources with Kustomize for RHACM

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
- route.yml

#Production
images:
  - name: mysql-db-image
    newName: quay.io/example/todo-single
    newTag: v1.1

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
