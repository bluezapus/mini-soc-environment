
## Roadmap Progress

This roadmap reflects the **actual implementation status** of the Mini SOC environment, aligned with the current **Detection Engineering phase**.

---
### Phase 1 — Core SOC Infrastructure (COMPLETED)

Focus: **Foundation & telemetry reliability**
- ELK Stack installation (Elasticsearch, Logstash, Kibana)
- TLS enabled across the entire stack
- Sysmon deployment on Windows endpoint
- Winlogbeat / Elastic Agent configuration
- Secure log ingestion (Winlogbeat → Logstash)
- Sysmon event parsing and ECS field normalization
- Centralized log storage in Elasticsearch
- Event visibility and validation in Kibana (Discover)

Outcome:  
**Stable, secure, and production-like SOC logging pipeline**

---
### Phase 2 — Detection Engineering (IN PROGRESS)
Focus: **Turning telemetry into detections**
- Custom detection rules based on Sysmon Event IDs
    - Process creation (Event ID 1)
    - Network connections (Event ID 3)
    - Image load (Event ID 7)
- Event tagging and classification
- Basic event correlation using normalized fields
- Initial alerting mechanisms (Kibana-based)

📌 Current Status:  
**Detection rules under active development and testing**

---
### Phase 3 — SOC Operations & Validation (PLANNED)
Focus: **Operational SOC workflow**
- Attack simulation using Kali Linux
- Validation of detection rules against real attack scenarios
- SOC investigation workflow
    - Event triage
    - Context enrichment
    - Incident documentation
- Ticket creation and tracking via internal ticketing system (Armbian)

Outcome Goal:  
**End-to-end SOC workflow from attack → detection → investigation**

---
Kalau mau **naik satu level lagi**, roadmap ini bisa ditambah:

- **Phase 4 — Optimization & Hardening**  
    (false positive reduction, dashboards, reporting)