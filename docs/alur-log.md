# Alur Log & Telemetry

## 1. Event Generation at the Endpoint
Windows generates security events through Sysmon, including:

- Process Create (Event ID 1)
- Network Connection (Event ID 3)
- Image Load (Event ID 7)
---
## 2. Pengiriman Log
Winlogbeat reads Sysmon events from the Windows Event Log and forwards them to Logstash.

---
## 3. Parsing & Enrichment
Logstash performs the following tasks:

- **Field normalization** (process, parent, hashes)
- **Data preparation** for SOC-level analysis
---
## 4. Storage & Visualization
The processed data is stored in Elasticsearch and analyzed through Kibana (Discover).

---
## Validation
- Sysmon Event IDs are visible in Kibana
- Fields are parsed as expected
- Timestamps and hostnames are correctly recorded

