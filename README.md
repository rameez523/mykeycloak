# mykeycloak

Reference:- https://medium.com/@rahul.soni_3674/how-to-deploy-keycloak-with-postgres-on-gke-5d660329a1dc

In this blog, we will se how we can deploy Keycloak with Postgres database on kubernetes here, Postgres database is to persist keycloak data. Without Postgres Keycloak will use it’s internal embedded databse H2.

Keycloak is an open-source Identity and Access management application. It can be used for authentication applications and it has many providers like google to provide sign-in from your google account. It has many security services like SSO, Social logins, Identity brokering, LDAP & active directory, and much more.

Scope — Keycloak with Postgres
We will deploy Keycloak with the Postgresql database to persist data. We will deploy all workloads on Google Kubernetes Engine.

Prerequisites — Keycloak with Postgres
Kubernetes cluster
Basic Knowledge of Postgresql Learn about Postgres from here https://www.postgresqltutorial.com/
Basic Knowledge of Keycloak Learn about Keycloak from here https://www.keycloak.org/guides

# Deploy Postgresql YAMLs
# Create 2 directories postgres/ & keycloak/ and place yaml files in these directories then deploy the workloads on cluster.

1. Create local storageclass for dynamic storage provisioning
mykeycloak/persistentvolumes/storageClass.yaml

2. (i) Go to any workerNode i.e, worker1 and give label to this node name=keycloak
command:- kubectl edit node worker1
   
   (ii) Create two directories for mounting local storage pv to that worker node and give all permissions to that directories:-
        mkdir -p /mnt/disk/vol1
        mkdir -p /mnt/disk/vol2
        chmod 777 /mnt/disk/*


3. Create pv and pvc for postgres & keycloak in mykeycloak/persistentvolumes

4. Create secret and statefulset yaml files in mykeycloak/postgres
command:- kubectl create -f mykeycloak/postgres/ -n keycloak

5. Create secret and statefulset yaml files in mykeycloak/keycloak
command:- kubectl create -f mykeycloak/keycloak/ -n keycloak





conclusion
So we successfully deployed Keycloak on kubernetes. If you want to migrate form H2 database to postgres database to persist all data.
