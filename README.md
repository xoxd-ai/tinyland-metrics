# @tummycrypt/tinyland-metrics (retired)

> **Retired 2026-10-10.** This package was merged into
> [xoxd-ai/tinyland-otel](https://github.com/xoxd-ai/tinyland-otel) as the
> `./metrics` subpath export, shipped in `tummycrypt_tinyland_otel` 1.2.0 and
> later. This repository is archived and gets no further changes.

## Migration

- Bazel: remove `bazel_dep(name = "tummycrypt_tinyland_metrics", ...)` and
  depend on `bazel_dep(name = "tummycrypt_tinyland_otel", version = "1.2.0")`
  (or later) from [xoxd-ai/bazel-registry](https://github.com/xoxd-ai/bazel-registry).
- Imports: change `@tummycrypt/tinyland-metrics` to
  `@tummycrypt/tinyland-otel/metrics`. The API is the same
  (`configureMetrics`, `getMetricsConfig`, `resetMetricsConfig`,
  `MetricsCollector`, `createMetricsCollector`, `getMetricsCollector`,
  `resetMetricsCollectorSingleton`, `EventStreamManager`,
  `getEventStreamManager`, and the types `MetricsConfig`, `MetricsLogger`,
  `ResolvedMetricsConfig`, `MetricsData`, `PageMetrics`, `RealtimeEvent`,
  `RequestDurationBuckets`, `SerializedPageMetrics`, `SessionMetrics`,
  `TopPage`, `TrafficSource`).
- The otel package root also re-exports the same names unchanged.
- One behavior fix ships with the merge: `MetricsCollector` now classifies
  referrers against the known social, search and internal domains by hostname
  (the domain itself or a subdomain) instead of by substring, so hosts such as
  `notfacebook.com` are classed as `Referral`.

## Distribution

Bazel is the only distribution path for in-house packages. Nothing is published
to npm from this repository any more, and the publish workflow has been removed.
The Bazel module `tummycrypt_tinyland_metrics` (0.2.2, 0.2.3) is marked
deprecated in the registry but stays resolvable; nothing is yanked. Earlier npm
releases of `@tummycrypt/tinyland-metrics` remain on the npm registry.

## What it was

An in-memory collector for page views, sessions, request and error counts
(with periodic JSON persistence under a configurable data directory), plus a
server-sent events stream manager for broadcasting realtime metrics, logs,
alerts and system status to connected clients.
