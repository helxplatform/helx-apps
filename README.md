# Helx-Apps
Helx-Apps is used by HeLxPlatform to dynamically ingest various application combinations during deployments. The branches specify deployment contexts and should not be deleted. Presently, these branches and their contexts created within the [app-registry](https://github.com/helxplatform/helx-apps/blob/edu720-azure/app-registry.yaml) file also correspond with the settings of Appstore during deployment. See [djangoSettings](https://github.com/helxplatform/appstore-chart/blob/f508eab0990efb683951c1242b0914412f2f6698/values.yaml#L93) in the appstore chart. 

# App-Specs
This repo generally exists to collect "app" spec files in the [Compose](https://docs.docker.com/compose/compose-file/) format. However, to faciliate robust usage of the Kubernetes environments these applications are destined, slight deviations to the compose spec were necessary. 

See the Google doc ["App" Definition Proposal](https://docs.google.com/document/d/16IUgwDTlqsxn72NZZzwtrBNAi-4B4OjSA9r-QTFL5w0/edit) for more information.

## Overview

Spec files are created in an app specific directory under [app-specs](https://github.com/helxplatform/helx-apps/tree/develop/app-specs).

Each app should be represented via the Compose file format [version 3](https://docs.docker.com/compose/compose-file/compose-file-v3/)
containing the service image, ports etc.

> Please specify memory resources in [Megabytes](https://docs.docker.com/config/containers/resource_constraints/#limit-a-containers-access-to-memory)
> "M" for consistency across specs.

Each app should also provide a minimum resource constraint in the form of a
`reservation` along with a maximum in the form of a `limit`. If you are not sure
what to set the defaults are currently:

```yaml
version: '3'
...
deploy:
  resources:
    limits:
      cpus: '8'
      memory: 64000M
    reservations:
      cpus: '1'
      memory: 1000M 
```

Most apps will want access to a core and gig of memory while the limit is something
that many Kubernetes environments can support for an individual application.
