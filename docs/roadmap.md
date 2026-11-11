# Roadmap: usage-billing-engine

- [x] 1. **Problem statement**: paragraph + target numbers in `README.md`.
- [ ] 2. **Build**: the developer designs, AI types. Design in `architecture.md`, choices in `decisions.md`. Done when the happy path works end to end and has tests.
- [ ] 3. **Containerize**: multi-stage Dockerfile, small image, non-root; `docker compose up` brings up the whole thing.
- [ ] 4. **Deploy**: local k8s (kind/k3d), probes, requests/limits; CI (GitHub Actions) → CD (ArgoCD).
- [ ] 5. **Observe**: OTel traces + metrics → Prometheus + Grafana (RED dashboard), structured logs with trace IDs, consumer-lag panel.
- [ ] 6. **Load**: k6: ramp, soak, spike. Record p50/p95/p99, error rate, throughput, CPU/mem, consumer lag.
- [ ] 7. **Scale**: more replicas / partitions; find the next bottleneck.
- [ ] 8. **Break**: kill a consumer mid-batch, kill Postgres, apply the same top-up twice, duplicate events.
- [ ] 9. **Fix**: idempotency, retries, timeouts, backpressure, whatever the break tests exposed.
- [ ] 10. **Conclude**: one page in `findings.md`: numbers before/after, what broke, why, what next.
