<div align="center">
  <img src="https://raw.githubusercontent.com/immune-medcloud/.github/main/assets/Immune-Medcloud-Logo-Small.png" width="110" alt="MedCloud Logo" />
  <h1>MedCloud</h1>
  <p><b>Zero-downtime clinical booking and teleconsultation platform engineered to survive cloud provider outages.</b></p>
</div>

---

### Architecture

| Role | Cloud & Region | Compute | Database |
| :--- | :--- | :--- | :--- |
| **Primary (Active)** | Azure (`spaincentral`) | AKS | Azure Database for PostgreSQL Flexible Server |
| **Secondary (Warm Standby)** | AWS (`eu-south-2`) | EKS | Amazon RDS for PostgreSQL |

* **Data Sync:** Native PostgreSQL Logical Replication (`PUBLICATION` $\rightarrow$ `SUBSCRIPTION` over TLS, $\text{RPO} < 1\text{s}$).
* **Failover:** Automated `/healthz` routing + GitHub Actions promotion pipeline ($\text{RTO} < 90\text{s}$).
* **Compliance:** Strict EU data residency (GDPR / LOPDGDD).

### Repositories

* [`medcloud-bootstrap`](https://github.com/immune-medcloud/medcloud-bootstrap) — GitHub Org setup, branch policies, and Azure/AWS OIDC federation
* [`medcloud-infra`](https://github.com/immune-medcloud/medcloud-infra) — Multi-cloud Terraform stacks, DB replication SQL, and DR failover workflows
* [`medcloud-app`](https://github.com/immune-medcloud/medcloud-app) — FastAPI clinical booking app, `/healthz` chaos probe, and portable K8s manifests