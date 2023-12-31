# Portals Helm Chart

This chart deploys the Portals application to a Kubernetes cluster.

## Install

You can install the chart with the following command:

```sh
helm repo add fsr5-fhaachen https://fsr5-fhaachen.github.io/charts/
helm upgrade --install portals fsr5-fhaachen/portals --namespace portals --create-namespace -f values.yaml
```

## Database and Redis

The chart does not install a database or redis. You have to install them yourself. 

You could use the [postgresql operator](https://cloudnative-pg.io/) and [redis operator](https://ot-container-kit.github.io/redis-operator/) for kubernetes.

If you want a deployment example, view [our deployment guide](https://github.com/fsr5-fhaachen/portals/blob/main/deploy/README.md) inside the portals repo.

## Values

You can find the default values in the [values.yaml](values.yaml) file.

You can override the default values but there are some values that need to be changed. The (minimum) required values are:

```yaml
environment: 
  APP_NAME: Erstiwoche FB5
  APP_KEY: # insert app key here
  APP_URL: https://portals.fsr5.de
  TUTOR_PASSWORD: password # insert secret password here
  ADMIN_PASSWORD: admin # insert secret password here
  APP_PUBLIC_API_SECRET: secret # insert secret password here
  AWS_ACCESS_KEY_ID: secret # insert aws data here
  AWS_SECRET_ACCESS_KEY: secret # insert aws data here
  AWS_DEFAULT_REGION: eu-central-1 # insert aws region here
  AWS_BUCKET: fsr5-fhaachen-portals # insert bucket name here
  AWS_USE_PATH_STYLE_ENDPOINT: false
  DB_CONNECTION: pgsql
  DB_HOST: # insert db host here
  DB_PORT: "5432"
  DB_DATABASE: postgres
  DB_USERNAME: postgres
  DB_PASSWORD: # insert db password here
  REDIS_HOST: # insert redis host here
  REDIS_PASSWORD: # insert redis password here
  REDIS_PORT: "6379"
ingress:
  enabled: true
  className: "nginx"
  annotations:
    cert-manager.io/issuer: "letsencrypt-prod"
  hosts:
    - portals.fsr5.de
  tls: true
```
