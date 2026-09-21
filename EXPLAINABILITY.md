# EXPLAINABILITY — Forge Line Sentinel Agent

> **Admissibility & Transparency Report for OpenGAP / Agent Passport**  
> *Agent Name:* Forge Line Sentinel Agent (`forge-line-sentinel-agent`)  
> *Specification:* OpenGAP v0.1.0  
> *Domain:* Manufacturing & supply chain / Shop-Floor Execution & Industrial Operations  

---

## 1. Overview & Industrial Purpose

Forge Line Sentinel Agent is an autonomous operational intelligence designed for discrete manufacturing facilities, assembly lines, and metal-forming plants. Built upon a modular Java/Maven MES architecture, the underlying platform unifies production counting, work order lifecycle execution, material flow ledgers, multi-tier component genealogy, and computerized maintenance management (CMMS).

The agent's primary industrial purpose is to maximize Overall Equipment Effectiveness (OEE) while maintaining uncompromising quality standards (ISO 9001 and ISA-95). By analyzing live workstation throughput, tracking scrap deviations, and scheduling maintenance intervals, the agent converts raw factory sensor streams into actionable supervisory guidance.

---

## 2. How the Agent Decides (Decision-Making Logic)

Forge Line Sentinel Agent executes decisions through a deterministic, four-stage manufacturing pipeline:

```
[Shop-Floor Telemetry & Work Orders] ──> [Schema & Routing Validation] ──> [OEE & Bottleneck Analysis]
                                                                                          │
                                                                                          ▼
[Dispatch Advice & Maintenance Alerts] <── [ISA-95 Safety & Quality Gate] <── [Genealogy & Batch Tracking]
```

### 2.1 Shop-Floor Ingestion & State Validation
- **Decision:** Determines whether incoming workstation cycle counts, operator logs, and material lot codes meet schema requirements.
- **Rules:**
  - Validates station IDs against the active plant layout topology.
  - Rejects duplicate cycle pulses and filters out electrical sensor noise.
  - Confirms raw material lot IDs exist in the active warehouse ledger before authorizing line consumption.

### 2.2 Production Scheduling & OEE Routing
- **Decision:** Optimizes work order queue sequencing across active machines to minimize changeover delays.
- **Rules:**
  - Computes OEE components: Availability (runtime / planned production time), Performance (total count / target count), and Quality (good units / total units).
  - Flags workstations operating at < 75% efficiency and dynamically recalculates line bottleneck shifts.

### 2.3 Genealogy Lineage & Anomaly Detection
- **Decision:** Assembles multi-tier material genealogy trees for serialized assemblies.
- **Rules:**
  - Links parent serial numbers with child component lot numbers at each progressive assembly stage.
  - When a quality deviation is reported, immediately executes reverse tracing to isolate all affected batches in the supply chain.

### 2.4 Maintenance Triggering & Equipment Safety Gate
- **Decision:** Generates preventative work orders based on run hour thresholds and machine part wear cycles.
- **Rules:**
  - Compares cumulative operating hours against CMMS maintenance intervals.
  - Escalates preventative alerts when tooling cycle counts exceed 85% of rated fatigue limits.

---

## 3. Data Sources & Inputs Used

| Data Input | Source | Purpose | Data Handling & Privacy |
|---|---|---|---|
| **Work Order Records** | MES database / ERP sync | Order priority, target quantities, planned cycle times, and customer delivery windows | Ingested via JDBC/REST; stored in internal transactional relational store |
| **Workstation Sensor Pulses** | PLC controllers / IoT sensors | Production counts, cycle durations, spindle speeds, and downtime intervals | Processed ephemerally in active memory; aggregated into 15-minute rollups |
| **Material Lot Ledgers** | Warehouse Management System (WMS) | Raw material batch identifiers, supplier certifications, and inventory quantities | Validated in memory; mapped to active work orders |
| **CMMS Maintenance Logs** | Maintenance records module | Equipment runtime hours, lubrication schedules, spare parts inventory | Read-only access for scheduling and wear predictions |

Forge Line Sentinel Agent complies with industrial security standards:
- **ISA-95 Boundary Compliance:** Operates strictly within Level 3 (MES operations) without bypassing Level 1/2 PLC safety limits.
- **Data Confidentiality:** Proprietary tooling dimensions, customer part designs, and internal cost formulas are strictly partitioned.
- **Stateless Inference:** LLM reasoning queries contain only abstracted anonymized telemetry without proprietary cad drawings.

---

## 4. Known Limitations & Failure Modes

Reviewers, plant managers, and line operators should note the following operational constraints:

1. **Hardware Telemetry Latency & PLC Disconnects:**
   - *Limitation:* Industrial network drops or legacy serial PLC communication lags may delay real-time cycle pulse ingestion.
   - *Mitigation:* Workstation edge buffers locally cache production events and resynchronize upon reconnect with exact timestamp reconciliation.

2. **Unreported Material Scrappage:**
   - *Limitation:* If an operator manually discards defective parts without scanning the defect code, production counts will deviate from physical inventory.
   - *Mitigation:* The agent flags discrepancies between consumed raw material weight and finished output counts during shift-end reconciliation audits.

3. **Complex Metallurgical & Chemical Wear:**
   - *Limitation:* Tool wear is estimated based on empirical hours and cycle counts; sudden thermal shock or material impurities causing micro-fractures cannot be predicted without dedicated ultrasonic telemetry.
   - *Mitigation:* Operators are mandated to perform physical visual inspections at each shift changeover regardless of automated green indicators.

4. **Non-Autonomous Plant E-Stop:**
   - *Limitation:* The agent operates as an advisory supervisory system and cannot directly trigger mechanical emergency stops (E-Stops) on physical machine motors.
   - *Mitigation:* Safety remains hardwired into physical safety relays and operator-accessible emergency pushbuttons per OSHA/CE regulations.

---

## 5. Verification, Safety & Human Oversight

- **Operator Workstation Confirmation:** Production dispatches and shift order changes require explicit supervisor sign-off before line changeover commences.
- **Deterministic Quality Gates:** Assemblies failing automated tolerance checks are physically diverted to rework bays by pneumatic gates.
- **Immutable Production Audit Trail:** Every status change, lot assignment, and operator intervention is logged with millisecond timestamps in compliance with ISO 9001.
- **Kill Switch:** Full agent processing can be paused immediately from the supervisory MES dashboard without affecting active PLC machine routines.
