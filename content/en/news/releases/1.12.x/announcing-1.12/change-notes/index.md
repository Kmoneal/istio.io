---
title: Change Notes
linktitle: 1.12.0
subtitle: Minor Release
description: Istio 1.12.0 release notes.
publishdate: 2021-11-16
release: 1.12.0
weight: 10
aliases:
    - /news/announcing-1.12.0
---

  ([Issue #](https://github.com/istio/istio/issues/))

## Traffic Management

- **Improved** TCP probes now working as expected: When using TCP probes with older versions of istio the check was always successful, even if the application didn't open the port.
  ([Issue #35578](https://github.com/istio/istio/issues/35578))

- **Added** validator for empty regex match.
  ([Issue #34066](https://github.com/istio/istio/issues/34066))

- **Fixed** an issue in which ADS would hang due to the wrong `syncCh` size being provided.
  ([Pull Request #34633](https://github.com/istio/istio/pull/34633))

- **Fixed** `DestinationRule` updates not triggering an update for `AUTO_PASSTHROUGH` listeners on gateways.
  ([Issue #34944](https://github.com/istio/istio/issues/34944))

- **Added** support for sourceip hash loadbalancing in TCP proxy.
  ([Issue #33558](https://github.com/istio/istio/issues/33558))

- **Added** support for envoy to track active connections during drain and quit if active connections become zero instead of waiting for entire drain duration. This is disabled by default and can be enabled by setting `EXIT_ON_ZERO_ACTIVE_CONNECTIONS` to true.
  ([Issue #34855](https://github.com/istio/istio/issues/34855))

- **Fixed** an issue when creating a Service and Gateway at the same time, causing the Service to be ignored.
  ([Issue #35172](https://github.com/istio/istio/issues/35172))

- **Added** support for `trafficPolicy.loadBalancer.consistentHash` in `DestinationRule` for proxyless gRPC clients.
  ([Pull Request #35333](https://github.com/istio/istio/pull/35333))

- **Added** the ability for users to specify Envoy's LOGICAL_DNS as a connection type for a cluster using 'DNS_ROUND_ROBIN' in ServiceEntry.
  ([Issue #35475](https://github.com/istio/istio/issues/35475))

## Security

- **Added** support to istiod to notice cacerts file changes via the `AUTO_RELOAD_PLUGIN_CERTS` env var.
  ([Issue #31522](https://github.com/istio/istio/issues/31522))

- **Added** `VERTIFY_CERT_AT_CLIENT` environmental variable to istiod. Setting `VERTIFY_CERT_AT_CLIENT` to `true` will verify server certificates using the OS CA certificates when not using a `DestinationRule` `caCertificates` field.
  ([Issue #25652](https://github.com/istio/istio/issues/25652))

- **Added** Auto mTLS support for workload level peer authentication. You no longer need to configure destination rule when servers are configured with workload level peer authentication policy. This can be disabled by setting `ENABLE_AUTO_MTLS_CHECK_POLICIES` to "false".
  ([Issue #33809](https://github.com/istio/istio/issues/33809))

- **Fixed** Gateway API xRoute does not forward the traffic to that backend when weight `0`.
  ([Issue #34129](https://github.com/istio/istio/issues/34129))

- **Fixed** the `EnvoyExternalAuthorizationHttpProvider` to match HTTP headers in a case-insensitive way.
  ([Issue #35220](https://github.com/istio/istio/issues/35220))

- **Added** the support of integrating with GKE workload certificates.
  ([Issue #35385](https://github.com/istio/istio/issues/35385))

## Telemetry


## Networking


## Installation

- **Fixed** a bug where specifying same port number with different protocols (TCP and UDP) lead to incorrect merging and rendered erroneous manifest.
  ([Issue #33841](https://github.com/istio/istio/issues/33841))

- **Added** labels on pod level for istio-operator and istiod.
  ([Issue #33879](ttps://github.com/istio/istio/issues/33879))

- **Fixed** Istioctl does not wait on CNI DaemonSet update.
  ([Issue #34811](https://github.com/istio/istio/issues/34811))

- **Fixed** No Permission to list ServiceExport from remote clusters in primary cluster.
  ([Issue #35068](https://github.com/istio/istio/issues/35068))

- **Added** pilot service annotations on helm chart
  ([Issue #35229](https://github.com/istio/istio/issues/35229))

- **Fixed** VMs are able to use a revisioned control plane specified by `--revision` on the `istioctl x workload entry` command.
  ([Issue #35290](https://github.com/istio/istio/issues/35290))

- **Added** Support arm64 api for operator, add nodeAffinity arm64 expression.
  ([Pull Request #35648](https://github.com/istio/istio/pull/35648))

## istioctl

- **Added** `istioctl install` will now do `IST0139` analysis on webhooks.
  ([Issue #33644](https://github.com/istio/istio/issues/33644))

- **Fixed** an issue where the `default` profile name was missing in the `istioctl install` confirmation prompt message.
  ([Issue #33857](https://github.com/istio/istio/issues/33857))

- **Added** `istioctl x remote-clusters` to list the remote clusters each `istiod` instance has API Server credentials for, and the service registry sync status of each cluster.
  ([Issue #33799](https://github.com/istio/istio/issues/33799))

- **Fixed** `istioctl profile diff` and `istioctl profile dump` have unexpected info logs.
  ([Pull Request #34325](https://github.com/istio/istio/pull/34325))

- **Added** the pod alias `po` for users to use `istioctl x describe po`, which is consistent with `kubectl` command.
  ([Pull Request #34802](https://github.com/istio/istio/pull/34802))

- **Fixed** `istioctl analyze` has the unexpected [IST0132] message when analyzing the gateway of the virtual service.
  ([Issue #34653](https://github.com/istio/istio/issues/34653))

- **Fixed** the deployment analyzer is ignoring service namespaces during the analysis process.
  ([Issue #34830](https://github.com/istio/istio/issues/34830))

- **Fixed** `istioctl operator` subcommands now support remote URLs specified in the `--manifests` argument.
  ([Issue #34896](https://github.com/istio/istio/issues/34896))

- **Fixed** `istioctl admin log` format.
  ([Issue #34982](https://github.com/istio/istio/issues/34982))

- **Improved** Analyzers reports output to match the naming scheme expected by the API, i.e `<ns>/<name>` instead of `<name>.<ns>`.
  ([Issue #35405](https://github.com/istio/istio/issues/35405))

- **Added** precheck now detects usage of Alpha Annotations.
  ([Pull Request #35483](https://github.com/istio/istio/pull/35483))

- **Added** `istioctl operator dump` now supports the `watchedNamespaces` argument to specify the namespaces the operator controller watches.
  ([Issue #35485](https://github.com/istio/istio/issues/35485))

- **Fixed** APP pods (such as httpbin) can not be created if not using 'istio-system' as the Istio namespace to install Istio at the first time. And `istioctl install`, `istioctl tag set` and `istioctl tag generate` will be influenced. For example, user can set a specified namespace (`mesh-1` as an example) to install Istio via `istioctl install --set profile=demo --set values.global.istioNamespace=mesh-1 -y`
  ([Issue #35539](https://github.com/istio/istio/issues/35539))

- **Fixed** `istioctl bug-report` has the extra default system namespaces displayed when `--exclude` is not set.
  ([Issue #35593](https://github.com/istio/istio/issues/35593))

## Documentation
