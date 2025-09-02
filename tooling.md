# Practical tooling & patterns

A short checklist of the tools, libs and operational patterns I use or discuss when running AI product projects. Focus is on pragmatic, testable practices rather than theoretical stacks.

## Experiment & data lifecycle
- **Experiment tracking:** *Weights & Biases* or *MLflow* — track runs, hyperparams, datasets, and reproducibility.
- **Data/versioning:** *DVC* or Git + object store for larger datasets — pin dataset versions for experiments.
- **Feature store:** *Feast* (or simple internal feature registry) — single source for production features.

## Serving & deployment
- **Model serving:** *BentoML / Seldon / TorchServe* for containerized model endpoints.  
- **Containers & orchestration:** Docker + Kubernetes for repeatable deploys.  
- **CI/CD:** GitHub Actions / GitLab CI for build/test/deploy pipelines (include model validation stages).

## Observability & monitoring
- **Metrics & logging:** Prometheus + Grafana for metrics; structured logging for inference traces.  
- **Data/model drift:** *Evidently* or custom checks to detect input distribution changes / prediction shifts.  
- **Error & crash reporting:** Sentry for app errors; alerts on abnormal model behaviour.

## Explainability & testing
- **Explainability libs:** LIME, SHAP, Captum (PyTorch) — expose lightweight explanations in product UI or internal dashboards.  
- **Unit & regression tests:** model unit tests, schema checks (Great Expectations), and integration tests for pipelines.  
- **Scenario tests:** targeted tests that simulate edge use-cases or adversarial inputs.

## Safety, fairness & privacy
- **Fairness toolkits:** IBM AIF360 or in-house checks — measure group performance gaps.  
- **Differential privacy / DP tools:** PyDP / OpenDP when privacy guarantees are required.  
- **Anonymisation & minimisation:** strip PII early in pipelines; keep personal info out of training sets where possible.

## UX & human in the loop
- **Human review:** review queues for high-impact decisions (HITL) and easy override paths.  
- **Feedback capture:** in-app “Why was this wrong?” flows to gather correction signals.

## Release patterns & product controls
- **Feature flags:** LaunchDarkly / simple feature flag service — roll out model changes gradually.  
- **Canarying & shadowing:** run new models in shadow mode or to a small % of traffic; measure key trust metrics.  
- **Rollback & runbooks:** one-click rollback paths and runbooks for incidents.

## Lightweight dev utilities (that fit a PM tinkerer)
- **Small scripts:** data sanity checks, GPX timestamp injector (useful for demos), ETL smoke tests.  
- **Notebooks with guardrails:** test notebooks that include assertions and sample checks (not source of truth).  
- **Local mocking:** mock services for external APIs during integration tests.

---

## Quick product checklist for a model release
1. **Pre-release:** dataset provenance checked + model card drafted.  
2. **Safety gates:** automated fairness & safety tests pass.  
3. **Canary:** deploy to small segment; monitor business KPIs + trust metrics.  
4. **Feedback loop:** capture corrections/flags and surface to training pipeline.  
5. **Post-release:** scheduled drift checks, weekly review for first month, rollback if anomalies.

---

## Notes / opinions (from product POV)
- Prefer **small, measurable** changes over huge model swaps — easier to attribute and safer to operate.  
- Invest early in **observability** — it pays back far more than optimized latency in early stages.  
- Keep the stack minimal for demos and conferences — no one needs full infra for a convincing demo.
