# Strategic Capability Map

## Cross-Cutting North Star
**Primary Evaluation Lens:** Can we determine the business impact when there is a production incident?

---

### 1. Business Observability Requirements
- **Description:** A structured interface and backend system of record for capturing flows, steps, signals, and associated business impacts.
- **Capability Owners:** `Central SRE Team`
- **Adopting Teams:** `Product Team`, `Development Team`

---

### 2. Service Registry Platform
- **Description:** System to register and expose service metadata with business flow mapping and telemetry tagging for automation.
- **Capability Owners:** `Central SRE Team`
- **Adopting Teams:** `Development Team`, `Product Team`

---

### 3. Business Playbook Generator
- **Description:** Generator that transforms structured observability metadata into consumable business playbooks (e.g., UI card, Markdown, PDF).
- **Capability Owners:** `Central SRE Team`
- **Adopting Teams:** `Product Team`, `Development Team`, `Platform SRE Team`

---

### 4. Alert Rule Generator
- **Description:** Translates structured observability metadata into platform-specific alert rules, enabling consistent and reusable alert logic across teams.
- **Capability Owners:** `Central SRE Team`
- **Adopting Teams:** `Development Team`, `Platform SRE Team`

---

### 5. Dashboard Blueprint Generator
- **Description:** Transforms structured observability metadata into reusable dashboard specifications, enabling consistent visual telemetry across systems and teams.
- **Capability Owners:** `Central SRE Team`
- **Adopting Teams:** `Product Team`, `Development Team`

---

### 6. Alert & Dashboard Deployment Engine
- **Description:** Automates the deployment and lifecycle management of alerts and dashboards using infrastructure-as-code practices with version control and rollback capabilities.
- **Capability Owners:** `Central SRE Team`
- **Adopting Teams:** `DevSecOps Tooling Team`

---

### 7. Agile Integration Toolkit
- **Description:** Toolkit that integrates observability deliverables into Agile workflows, treating observability as a first-class artifact in planning and delivery.
- **Capability Owners:** `Central SRE Team`
- **Adopting Teams:** `Product Team`, `Development Team`, `Platform SRE Team`

---

### 8. Observability as Code & CICD Integration
- **Description:** Enables version-controlled observability configurations to be validated, promoted, and deployed through CI/CD pipelines with the same rigor as application code.
- **Capability Owners:** `Central SRE Team` + `DevSecOps Tooling Team`
- **Adopting Teams:** `Development Team`

