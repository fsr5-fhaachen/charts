# Strichlistensystem Helm Chart

This chart deploys the Strichlistensystem application to a Kubernetes cluster.

## Install

You can install the chart with the following command:

```sh
helm repo add fsr5-fhaachen https://fsr5-fhaachen.github.io/charts/
helm upgrade --install strichlistensystem fsr5-fhaachen/strichlistensystem --namespace strichlistensystem --create-namespace -f values.yaml
```

## Database and Redis

The chart does not install a database or redis. You have to install them yourself. 

You could use the [postgresql operator](https://cloudnative-pg.io/) and [redis operator](https://ot-container-kit.github.io/redis-operator/) for kubernetes.

If you want a deployment example, view [our deployment guide](https://github.com/fsr5-fhaachen/portals/blob/main/deploy/README.md) inside the portals repo. (This guide is written for portals but can be adapted for the strichlistensystem because they are both laravel applications installed via helm.)

## Values

You can find the default values in the [values.yaml](values.yaml) file.

You can override the default values but there are some values that need to be changed. The (minimum) required values are:

```yaml
environment: 
  APP_NAME: Gerolstein FB5
  APP_KEY: # insert app key here
  APP_URL: https://strichlistensystem.fsr5.de
  APP_VPN_IP: # insert vpn ip here
  CSV_EXPORT_PW: password # insert secret password here
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
    - strichlistensystem.fsr5.de
  tls: true
```
