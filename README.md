# Forge Line Sentinel

[![License: AGPL v3](https://img.shields.io/badge/License-AGPL_v3-blue.svg)](LICENSE.txt)
[![Java](https://img.shields.io/badge/Java-8%2B-orange.svg)](https://www.oracle.com/java/)
[![Maven](https://img.shields.io/badge/Build-Maven-C71A36.svg)](https://maven.apache.org/)

**Forge Line Sentinel** is a modular Manufacturing Execution System (MES) designed to optimize shop-floor operations, streamline production tracking, and connect manufacturing lines with enterprise planning workflows.

---

## 🚀 Key Modules & Capabilities

- **Production Tracking & Counting**: Monitor active workstations, track run times, output counts, and workstation efficiency.
- **Work Orders & Master Scheduling**: Schedule, execute, and monitor production orders with integrated Gantt planning and shift assignments.
- **Material Flow & Inventory**: Real-time management of warehouse materials, inventory allocations, batch tracking, and delivery supplies.
- **Genealogy & Quality Control**: Track material genealogy across assembly steps, record deviation causes, and ensure traceability.
- **Cost & Norm Calculations**: Compute labor costs, material cost norms, and operation times to analyze and improve line profitability.
- **CMMS & Maintenance**: Manage machine parts, maintenance routines, and minimize equipment downtime.

---

## 🏗 Project Architecture

Forge Line Sentinel uses a multi-module Maven structure:

- **`mes-application/`**: Web application runner and container configuration (`war`).
- **`mes-plugins/`**: Modular feature plugins:
  - `mes-plugins-orders`: Work order lifecycle and execution.
  - `mes-plugins-production-counting`: Production logging, tracking, and progress metrics.
  - `mes-plugins-material-flow`: Raw material, WIP, and finished goods movement.
  - `mes-plugins-technologies`: Bill of Materials (BOM), operation routing, and process definitions.
  - `mes-plugins-advanced-genealogy`: Traceability and component lineage.
  - `mes-plugins-cmms-machine-parts`: Maintenance and equipment spare parts management.

---

## 🛠 Prerequisites

- **Java JDK**: 8 or higher
- **Maven**: 3.6+
- **Database**: PostgreSQL / MySQL / HSQLDB

---

## 📦 Building from Source

To build all plugins and the main application package:

```bash
mvn clean install -DskipTests
```

---

## 📄 License

This project is licensed under the [GNU Affero General Public License v3 (AGPL-3.0)](LICENSE.txt).
