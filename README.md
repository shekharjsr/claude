# CloudCarbon — Multi-cloud emission tracking and workload optimization

Large cloud deployments generate a lot of carbon. Most teams don't know how much, or where it's coming from. This platform fixes that.

Built initially for Volkswagen Group's infrastructure running across AWS and Azure, CloudCarbon pulls real-time energy and workload telemetry from both clouds, maps it against live regional carbon intensity grids, and gives engineering and sustainability teams a shared view of what's actually happening — per workload, per region, per hour.

After six months in production across Volkswagen Group's fleet, it has contributed to a 20% reduction in cloud infrastructure carbon emissions.

---

## The problem it solves

Running workloads across AWS and Azure means dealing with two different billing models, two different monitoring stacks, and zero unified visibility into carbon footprint. Most cloud cost tools treat emissions as a reporting checkbox — a number that appears somewhere in a dashboard but doesn't connect to any actual decision.

That gap is what this project addresses. When a workload is running in a high-carbon region during peak grid hours, the platform identifies it and generates a specific recommendation: which region to shift to, what the estimated emission saving looks like, and what the latency or cost trade-offs are. The output is readable by both an infrastructure engineer and a sustainability officer.

---

## How it works

The platform sits as a layer across both clouds. It ingests:

- Energy consumption metrics per instance/service (AWS CloudWatch, Azure Monitor)
- Regional carbon intensity data (live grid feeds, updated hourly)
- Workload metadata — runtime, region, instance type, scheduling patterns

From that, it produces:

- A unified emission footprint view across both clouds
- Workload-level carbon cost alongside financial cost
- Shift recommendations ranked by emission saving vs. operational impact
- Plain-language weekly summaries for non-technical stakeholders, generated with Claude

---

## Current status

In production at Volkswagen Group. Core emission-mapping and recommendation engine are being prepared for open-source release (planned Q1 2027). The first public components will cover the cross-cloud telemetry ingestion layer and the carbon intensity grid integration — the parts most likely to be useful to other teams running multi-cloud infrastructure.

---

## Architecture overview

```
AWS CloudWatch  ──┐
                  ├──► Telemetry Aggregator ──► Carbon Intensity Mapper ──► Recommendation Engine
Azure Monitor   ──┘                                      ▲
                                               Regional Grid APIs
                                           (electricityMap / WattTime)
```

Claude is used at two points: summarizing aggregated emission reports into readable weekly briefs, and generating the reasoning behind workload shift recommendations.

---

## Roadmap

- [x] Multi-cloud telemetry ingestion (AWS + Azure)
- [x] Carbon intensity grid integration
- [x] Workload-level emission attribution
- [x] AI-generated shift recommendations
- [ ] Open-source release of telemetry ingestion layer (Q1 2027)
- [ ] GCP support
- [ ] Terraform module for self-hosted deployment
- [ ] Public API for carbon intensity lookups

---

## Contributing

The project is not yet publicly open for contributions, but will be ahead of the open-source release. Watch this repo for updates.

---

## License

To be determined ahead of open-source release. Likely Apache 2.0.
