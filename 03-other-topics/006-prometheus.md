---
category: cloud-platform
expires: 2019-01-01
---
# Using the Cloud Platform Prometheus, AlertManager and Grafana
## Introduction
Prometheus, AlertManager and Grafana have been installed on Live-0 to ensure the reliability and availability of the Cloud Platform. This document will briefly outline how to access the monitoring tools and where to find further information.

## What is Prometheus

Prometheus is an open-source systems monitoring and alerting toolkit originally built at SoundCloud. The Cloud Platform uses [Prometheus Operator from CoreOS](https://github.com/coreos/prometheus-operator) which allows a number of Prometheus instances to be installed on a cluster.

Prometheus scrapes metrics from instrumented jobs, either directly or via an intermediary push gateway for short-lived jobs. It stores all scraped samples locally and runs rules over this data to either aggregate and record new time series from existing data or generate alerts. Grafana or other API consumers can be used to visualize the collected data.

## What is AlertManager

The Alertmanager handles alerts sent by client applications such as the Prometheus server. It takes care of deduplicating, grouping, and routing them to the correct receiver integration such PagerDuty. It also takes care of silencing and inhibition of alerts.

## What is Grafana

Grafana allows you to query, visualize, alert on and understand your metrics no matter where they are stored. Create, explore, and share dashboards with your team and foster a data driven culture.

### Creating dashboards
Grafana is set up as a stateless app, managed entirely through code. This also helps achieve better availability. However, it means that dashboards will not persist in its database. To create a dashboard:

1. Login to grafana (see the links below) with your GitHub account. All users are able to edit dashboards but cannot save the changes. Find the dashboard titled 'Blank Dashboard' and modify it as you see fit.

2. Once happy with your dashboard, click the share icon on the top right corner, select the `Export` tab and `View JSON`. Copy the JSON string into a `ConfigMap` according to the example below.

```YAML
---
apiVersion: v1
kind: ConfigMap
metadata:
  name: <my-dashboard>
  namespace: <my-namespace>
  labels:
    cloud-platform.justice.gov.uk/grafana-dashboard: ""
data:
  blank-dashboard.json: |
    {
      [ ... ]
    }
```

Make sure you've included the `label` and that the JSON string is properly indented. Also, name of the key in the `ConfigMap` must end in `-dashboard.json`. Please note that you can have multiple dashboards exported in a single `ConfigMap` as well.

3. Use `kubectl` to apply the `ConfigMap` above, your dashboard should be visible in Grafana shortly.

## How to access monitoring tools

All links provided below require you to authenticate with your Github account.

Prometheus: [https://prometheus.apps.cloud-platform-live-0.k8s.integration.dsd.io](https://prometheus.apps.cloud-platform-live-0.k8s.integration.dsd.io)

AlertManager: [https://alertmanager.apps.cloud-platform-live-0.k8s.integration.dsd.io](https://alertmanager.apps.cloud-platform-live-0.k8s.integration.dsd.io/)

Grafana: [https://grafana.apps.cloud-platform-live-0.k8s.integration.dsd.io](https://grafana.apps.cloud-platform-live-0.k8s.integration.dsd.io)


## Further documentation

[Prometheus querying](https://prometheus.io/docs/prometheus/latest/querying/basics)

[AlertManager](https://prometheus.io/docs/alerting/alertmanager)

[Architecture](https://prometheus.io/docs/introduction/overview/#architecture)
