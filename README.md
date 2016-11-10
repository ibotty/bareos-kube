# Bareos containers to be used within a kubernetes cluster

Bareos is a centralized backup solution.
This set of containers will dynamically configure it to support it in a cloud environment.

It consists of the following containers.


## Bareos Director/Kubernetes Controller (required)

The Bareos director is the central controller for Bareos. It runs in it's own container, with only one pod being allowed to run at all times.

It needs a PostgreSQL (or maybe later a different database) it can access.
See the `BAREOS_POSTGRES_HOST`, `BAREOS_POSTGRESQL_PORT`, `BAREOS_POSTGRESQL_USER` and `BAREOS_POSTGRESQL_PASSWORD` environment variables.


The Kubernetes controller will watch the butter.sh/bareos thirdpartyresource to configure bareos.


## Bareos Storage Daemon (required)

The Bareos storage daemon is responsible for getting data from the file daemon, backing it up and eventually restore it.


## Bareos File Daemon

The Bareos file daemon will send data to the storage daemon to back up.


