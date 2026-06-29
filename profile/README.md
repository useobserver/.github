<p align="center">
    <img src="https://raw.githubusercontent.com/useobserver/.github/main/assets/headline.png" alt="Observer" height="100%">
</p>

<p align="center">
  <a href="https://use.observer"><img src="https://img.shields.io/badge/Website-use.observer-1f6feb?style=for-the-badge" alt="Website"></a>
  <a href="https://docs.use.observer"><img src="https://img.shields.io/badge/Documentation-link-blue?style=for-the-badge" alt="Documentation"></a>
</p>

# Observer

**Status pages backed by real metrics.**

[Observer](https://use.observer) is a metrics-driven status page platform. You
define what "healthy" means as numeric thresholds on signals from your own
infrastructure. Observer evaluates them continuously and turns each verdict into
public status pages, SLOs, and incident timelines your customers can trust.

## Collect

Point Observer at the signals you already trust. Each check evaluates against
strict thresholds and produces one status.

- **Metrics.** Prometheus, OpenTelemetry (OTLP), CloudWatch, and direct active
  probes: HTTP, TCP, DNS, TLS certificate expiry, gRPC, WebSocket, ICMP, host.
- **Logs.** Turn log volume and patterns into status with Loki and
  Elasticsearch aggregations.
- **Databases.** Probe Postgres, MySQL, Redis, and MongoDB directly with a
  read-only query.
- **Agent.** A self-hosted data plane that runs the checks inside your network
  and pushes verdicts only.

## Deliver

Turn those verdicts into something people act on.

- **Status pages.** Public or access-controlled, with 30-day history and uptime.
- **SLOs.** Targets, error budgets, and burn-rate timelines per service.
- **Incidents.** Post updates your customers actually read.
- **Notifications.** Reach subscribers where they are.

Pages can be scoped per customer for customer-facing status, or kept private for
on-call and internal teams.

## How it fits together

Two properties shape the design:

- **Your telemetry stays yours.** The [agent](https://github.com/useobserver/agent)
  runs inside your network, evaluates each check locally, and pushes only the
  result (`metric_id`, `value`, `status`, `timestamp`). Query results,
  credentials, and connection strings never leave your network.
- **Your configuration lives in version control.** The
  [CLI](https://github.com/useobserver/cli) applies a single `observer.yaml`
  through a workflow you own, so your setup is reviewed in pull requests instead
  of locked inside a UI.

```
        your infrastructure                 open source (this org)            use.observer (cloud)

┌──────────────────────────────┐   probe +     ┌───────────────┐   push     ┌─────────────────────┐
│ Prometheus, OTLP, CloudWatch │   evaluate    │ Observer      │   verdict  │ Observer Cloud       │
│ HTTP, TCP, DNS, TLS, gRPC,   │ ─────────────▶│ Agent         │ ──────────▶│ status pages, SLOs,  │
│ databases, Loki, Elastic, …  │               └───────────────┘            │ incidents, alerts    │
└──────────────────────────────┘                                            └─────────────────────┘
                                               ┌───────────────┐   apply              ▲
  observer.yaml in your repo ─────────────────▶│ Observer CLI  │ ─────────────────────┘
                                               └───────────────┘
```

## Open components

| Repository                                        | What it is                                                                                                                                                                                               |
| ------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [**agent**](https://github.com/useobserver/agent) | The data plane. Probes every source above, evaluates each threshold locally, and pushes verdicts over a single outbound HTTPS connection. Apache-2.0.                                                    |
| [**cli**](https://github.com/useobserver/cli)     | Configuration as code. A dependency-free client over the Observer public API: plan changes on pull requests, apply on merge, export current state to bootstrap a repository. Ships a GitHub Action. ISC. |

## Get started

1. Create an account at [use.observer](https://use.observer).
2. Install the [agent](https://github.com/useobserver/agent) next to your signals
   and connect it with the key from the Agents page.
3. Define your first check, then publish a status page.

Full walkthroughs live in the [documentation](https://docs.use.observer). Prefer
config as code? Start with the [CLI](https://github.com/useobserver/cli) and
commit an `observer.yaml`.

## Links

- Product: [use.observer](https://use.observer)
- Documentation: [docs.use.observer](https://docs.use.observer)
- Agent: [github.com/useobserver/agent](https://github.com/useobserver/agent)
- CLI: [github.com/useobserver/cli](https://github.com/useobserver/cli)
