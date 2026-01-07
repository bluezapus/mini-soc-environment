# Mini SOC Environment Architecture
## System Components
### Server (Ubuntu 22.04 LTS)
Acts as a **centralized SIEM server**, running the following stack:
- **Elasticsearch** (log storage and indexing)
- **Logstash** (log parsing and enrichment)
- **Kibana** (visualization and analysis)

### Windows Victim
A Windows 10 endpoint that generates security telemetry:
- **Sysmon** (event-level telemetry)
- **Winlogbeat** (log shipping agent)

---
## Architecture Diagram (Conceptual)
Windows 10  (Sysmon + Winlogbeat)  -> Logstash (Ubuntu)  -> Elasticsearch -> Kibana
## Design Principles
- **Centralized logging**
- **Clear separation of roles** (endpoint vs SIEM)
- **Scalable and production-like architecture**
