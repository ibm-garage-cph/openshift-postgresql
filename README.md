# openshift-postgresql

## 1. Ensure to have created a project

Create an openshift project, using your initials as suffix

```bash
oc new-project dev-<your-initials>
oc new-project dev-jd
```

## 2. Create a persistent volume claim

We'll be using a dynamic volume assignment. This means that we don't have to define the volume manually, but it will be assigned to us on demand, by the cloud provider.

```bash
oc apply -f ./01_postgres-pvc-dyn.yml
```

*Make sure to replace <your-initials> with your actual initials*

## 3. Create a secret

This `secret` will later be used to access postgres

```bash
oc apply -f ./02_postgres-pvc-dyn.yml
```

## 4. Create a pod

Create a pod using the official postgres image as source. Note that the persistent volume claim must be attached to this pod.

```bash
oc apply -f ./03_postgres-pod.yml
```

## 5. Create a service to expose your pod

```bash
oc apply -f ./04_service.yml
```

## 7. Validate 

Open the Openshift web console. Navigate to your namespace and find the postgres pod.

Connect to the busybox container and install pgcli

connect to the service 

```
pgcli -h postgres.svc.local -u postgres
```