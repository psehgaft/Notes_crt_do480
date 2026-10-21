# Study Notes — Multicluster Management (DO480 Track)

Personal study notes for multicluster application resource management with Red Hat Advanced Cluster Management (RHACM): RBAC for multicluster users, customizing RHACM resources with Kustomize, importing clusters, and supporting integrations.

> [!IMPORTANT]
> This is an independent study repository. It is not an official Red Hat course, exam guide, or exam dump. Run privileged commands only against a disposable lab cluster you are authorized to administer.

## Table of contents

- [Multicluster Application Resource Management with RHACM](#multicluster-application-resource-management-with-rhacm)
- [Customizing resources with Kustomize for RHACM](#customizing-resources-with-kustomize-for-rhacm)
- [ACS — how to import cluster](#acs---how-to-import-cluster)
- [Integrations](#integrations)
- [License](#license)

## Multicluster Application Resource Management with RHACM

### Users

Granting cluster roles to users, including RHACM managed-cluster-set roles:

```sh
oc adm policy add-cluster-role-to-user view user

oc adm policy add-cluster-role-to-user open-cluster-management:managedclusterset:admin:prod user
oc adm policy add-cluster-role-to-user open-cluster-management:managedclusterset:view:prod user
```

## Customizing resources with Kustomize for RHACM

Kustomize from scratch:

- Override the image for a specific environment
- Add a `namePrefix`
- Deploy an application from git, from 2 different branches (dev and prod)

```yaml
# Development
apiVersion: kustomize.config.k8s.io/v1beta1
kind: Kustomization
# Development
commonLabels:
  app: dev-todolist.js

# path to base directory
bases:
  - ../../base

resources:
  - pvclaim.yml
  - route.yml

# Development
images:
  - name: mysql-db-image
    newName: quay.io/example/todo-single
    newTag: v2.0-beta

# Add name prefix "dev"
namePrefix: dev-
```

Render an overlay to verify before applying:

```sh
kubectl kustomize overlays/development/
```

## ACS — how to import cluster

(Section reserved for the cluster-import procedure.)

## Integrations

- Create and configure Syslog integration
- Make image show up via "Scanning via watch tag"

## License

This repository is licensed under the GNU General Public License v3.0 — see [LICENSE](LICENSE).
