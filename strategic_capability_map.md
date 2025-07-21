# Strategic Capability Map

## Cross-Cutting North Star
**Primary Evaluation Lens:** Can we determine the business impact when there is a production incident?

All tier-based capabilities and ownership expectations should be evaluated against this cornerstone question.

---

## Tier: Strategic

### 1. Business Observability Requirements Authoring System
- **Description:** A structured interface and backend system of record for capturing flows, steps, signals, and associated business impacts.
- **Primary Owners:** Product Teams, Development Teams
- **Responsible Contributors:** Central SRE Team
- **Industry Mapping:** Aligns conceptually with "Service Catalog Management" (e.g., Atlassian Compass, Backstage) but focused on business observability metadata rather than just services.

---

### 2. Service Registry Platform
- **Description:** Enterprise-wide system to standardize, register, and expose metadata for all business and technical services. This includes mapping services to business flows, stages, and steps, supporting inter-service dependency awareness (for tracing and silent failure detection), and exposing telemetry tagging metadata (`app_id`, `stage_id`, `customer_type`) to enable downstream automation and correlation.
- **Primary Owners:** Enterprise Observability Team
- **Fallback Ownership:** Central SRE Team (if enterprise declines)
- **Industry Mapping:** Expands on tools like Backstage, Consul, or ServiceNow CMDB by layering in business observability metadata and dependency models for enhanced telemetry traceability.

---

### 3. Business Playbook Composer
- **Description:** Generator that transforms structured observability metadata into consumable business playbooks (e.g., UI card, Markdown, PDF).
- **Design Constraint:** Must only consume upstream observability metadata; it does not define or own alert logic, telemetry tagging, or dashboard implementation. This maintains strict separation of concerns.
- **Primary Owners:** Central SRE Team
- **Supporting Teams:** Product Teams
- **Industry Mapping:** Closely resembles Runbook generation or context-rich Incident Response Docs (e.g., PagerDuty Business Context Cards, Atlassian Runbooks), but specialized for proactive business insight rather than incident handling alone.

---

### 4. Alert Rule Generator
- **Description:** Logic engine that translates structured observability metadata (e.g., business signals, process expectations, performance thresholds) into actionable, platform-specific alert rules. It serves as the bridge between declarative observability requirements (defined at the `Step` level) and executable alert logic (e.g., Splunk SPL, Prometheus expressions, New Relic workflows). It enables consistency, reuse, and traceability of alert logic across teams.
- **Implied Capabilities:**
  - Input normalization for varied signal definitions (e.g., SLI thresholds, error codes, absence-of-signal cases).
  - Translation templates for multiple monitoring platforms (e.g., Splunk, Prometheus, Datadog).
  - Integration with version control to track rule evolution over time.
  - Optionally generates metadata needed to register the alert into the deployment system (e.g., tags, ownership, dashboard linkage).
- **Primary Owners:** Central SRE Team
- **Supporting Teams:** Development Teams (for signal specification and validation)
- **Industry Mapping:** Closely aligned with the **Signal-to-Alert pipeline** model found in tools like:
  - Splunk ITSI Notable Events / Correlation Searches
  - Prometheus AlertManager rules
  - Terraform-based alert modules (e.g., Datadog, SignalFx)
  - New Relic workflows

  Also resonates with the architectural practice of **"Alert Rule as Code"**, part of broader observability as code strategies.

---

### 5. Dashboard Blueprint Generator
- **Description:** Component that transforms structured observability metadata into reusable, standards-based dashboard specifications. It decouples dashboard logic from implementation, enabling consistent visual telemetry across systems and teams. The output may include layout, widget definitions, data source mappings, thresholds, and business signal annotations.
- **Implied Capabilities:**
  - Normalized input from the observability requirements system (flows, steps, signals).
  - Reusable visual templates tailored to monitoring platforms.
  - Support for traceability (e.g., widget ↔ business signal ↔ KPI mapping).
  - Platform-specific output formats (e.g., Splunk Simple XML, Grafana JSON, Datadog JSON).
- **Primary Owners:** Central SRE Team
- **Supporting Teams:** Development Teams
- **Industry Mapping:** Strong alignment with tools like:
  - **Grafana provisioning**
  - **Datadog Dashboard-as-Code**
  - **Splunk dashboard generators**

---

### 6. Alert & Dashboard Deployment Engine
- **Description:** Automates the provisioning and lifecycle management of alerts and dashboards in enterprise monitoring platforms. This engine consumes the output of blueprint generators (e.g., alert rules, dashboard specifications) and applies them to production environments via infrastructure-as-code practices. It ensures version control, repeatability, rollback capability, and traceability of deployed observability assets.
- **Implied Capabilities:**
  - Accepts standardized alert and dashboard specifications (e.g., YAML, JSON, HCL).
  - Applies configurations to monitoring platforms using APIs or declarative provisioning tools.
  - Supports dry-run validation, staged rollout, and rollback.
  - Integrates with CI/CD workflows (e.g., GitHub Actions, Jenkins, Azure DevOps) to automate promotion through environments.
- **Primary Owners:** Development Teams
- **Supporting Teams:** Central SRE Team
- **Industry Mapping:** Strong alignment with:
  - **Terraform modules** for observability (e.g., Datadog, New Relic, Grafana dashboards).
  - **Splunk API-based** content deployment.
  - **Grafana provisioning** via configuration files or automation scripts.
  - General **"Observability as Code"** practices common in platform engineering.

---

### 7. Agile Integration Toolkit for Observability
- **Description:** Embedded toolkit and supporting guidance that connects observability deliverables with Agile workflows. It ensures that observability metadata (e.g., signal definitions, alert requirements, dashboards) is treated as a first-class artifact in Agile planning, delivery, and review. This includes story templates, backlog taxonomy, and alignment with Program Increment (PI) objectives.
- **Implied Capabilities:**
  - Standardized user story templates for observability artifacts (e.g., “As a Product Owner, I want a business signal for…”).
  - Sprint-ready acceptance criteria for observability deliverables (e.g., dashboards deployed, alert thresholds defined).
  - Workflow guidance for backlog refinement and prioritization of observability needs.
  - Optionally integrates with Agile tooling (e.g., Jira custom issue types, automation rules).
  - Reinforces alignment with SAFe principles (e.g., Tech Enablers in Program Increments).
- **Primary Owners:** Product Teams
- **Supporting Teams:** Development Teams
- **Industry Mapping:**
  - **Jira SRE templates** and **observability-focused issue types**
  - **SAFe Enabler Stories** for technical observability work
  - **Backstage Scaffolder workflows** that generate tickets for observability requirements
  - Industry-aligned with **Platform Product Management** practices that bake SLOs and telemetry ownership into delivery plans

---

### 8. Observability as Code & CICD Integration
- **Description:** Enables version-controlled observability configurations to be automatically validated, promoted, and deployed through CI/CD pipelines alongside application code. This ensures observability artifacts (e.g., alert rules, dashboards, telemetry processors) are governed, tested, and released with the same rigor as software delivery.
- **Implied Capabilities:**
  - Repository-based source of truth for observability assets (e.g., YAML, HCL, JSON).
  - Integration with CI tools to perform validation, linting, and preview deployments of observability configurations.
  - Promotion workflows across dev/test/prod environments via GitOps or declarative pipelines.
  - Automated rollback and change tracking tied to Git commits and PRs.
  - Coordination with development pipeline owners to support deployment hooks for metrics, tracing config, and alert registration.
- **Primary Owners:** Central SRE Team, Development Teams
- **Supporting Teams:** Enterprise Integrated Development Platform Team
- **Note:** Platform SRE teams are **not** expected to contribute here due to current maturity limitations.
- **Industry Mapping:**
  - Strong alignment with:
    - **Terraform Observability Modules**
    - **GitOps practices** for observability (e.g., ArgoCD, Flux)
    - **CI-integrated observability validation tools** (e.g., Prometheus rule testers, Splunk SPL checkers)
    - **OpenTelemetry Collector** pipelines deployed via IaC
    - General **“Observability as Code”** approaches within Platform Engineering and SRE disciplines

