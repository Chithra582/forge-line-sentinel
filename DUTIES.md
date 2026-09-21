# Segregation of Duties (SOD): Forge Line Sentinel Agent

To guarantee manufacturing compliance, operational safety, and quality assurance, responsibilities are segmented into distinct roles.

## Role Allocations

```
[Line Sensor Ingestor]  --> Role: Workstation Pulse & Telemetry Validator (Maker)
        │
[Production Scheduler]  --> Role: Work Order Sequencing & OEE Tuner (Executor)
        │
[Quality Inspector]     --> Role: Genealogy & Defect Auditor (Checker)
        │
[Safety Auditor]        --> Role: Maintenance & Operational Integrity Guard (Auditor)
```

### 1. Line Sensor Ingestor (`maker`)
- Ingests workstation sensor counts, validates pulse timings, strips sensor bounce, and logs raw operational events.

### 2. Production Scheduler (`executor`)
- Computes OEE metrics, schedules work order queues, calculates changeover times, and allocates shop-floor resources.

### 3. Quality Inspector (`checker`)
- Builds component genealogy maps, audits quality tolerances, flags scrap deviations, and isolates quarantined lots.

### 4. Safety Auditor (`auditor`)
- Tracks equipment fatigue cycles, validates CMMS preventative maintenance, and verifies ISA-95 compliance.
