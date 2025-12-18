# Warehouse Inbound & Inventory Accuracy (SQL Server) — BRD to KPI Reporting

## Overview
This project models and implements a warehouse inbound receiving workflow and KPI reporting layer, covering:
- **BP-2:** Inbound shipment capture
- **BP-3:** GRN (Goods Receipt Note) creation
- **BP-4:** Inventory posting job/system behavior
- **BP-5:** Inbound & delayed shipments dashboard metrics
- **BP-6:** Inventory accuracy KPI reporting using physical counts

The repository includes **BA artifacts (BRDs, wireframes, data dictionaries, UAT)** and a **SQL Server implementation (schema, seed data, and T-SQL queries)**.

---

## Business Problem
Inbound receiving and inventory updates were spreadsheet-driven, leading to:
- data entry errors and duplicate records,
- low visibility into delayed inbound shipments,
- inventory mismatches between system stock and physical counts.

---

## What I Built (Scope)
### BP-2 — Record Inbound Shipment Details
- Captured inbound shipment header details with validation rules (mandatory fields, duplicate Shipment ID prevention, numeric/date checks)
- Standardized shipment status tracking for inbound visibility

### BP-3 — Capture Received Quantity and Create GRN
- Created GRN header + line item capture (SKU-level)
- Supported discrepancy classification: **Short / Over / Damaged / OK**
- Defined Draft vs Complete lifecycle and exception handling

### BP-4 — Inventory Update Job (System Behavior)
- Defined posting rules: process only **Complete + unposted** GRNs
- Updated `inventory_on_hand` and created auditable entries in `stock_movement`
- Prevented double-posting via idempotency rules

### BP-5 — Inbound & Delayed Shipments Dashboard
- Defined KPIs and drill-down logic for delayed shipments
- Supported filtering by date range / supplier / warehouse
- Included trend and supplier delay analysis requirements

### BP-6 — Inventory Accuracy KPI
- Calculated accuracy using `physical_count_snapshot` vs `system_qty`
- Reported accuracy by **location/category**
- Produced mismatch action list with variance (physical − system)

---

## Tools & Skills Demonstrated
- **Business Analysis:** BRD, user stories & acceptance criteria, wireframes, data dictionary
- **Delivery Tracking:** Jira (**Epics / Stories / Subtasks**)
- **Testing:** UAT test case design and traceability
- **Data & SQL:** SQL Server schema design, seeded dataset, T-SQL KPI/query development

---

## Repository Map
- `sql/` → SQL Server schema, seed data, KPI/dashboard queries  
- `docs/` → BRDs, wireframes, data dictionaries, UAT artifacts  
- `assets/` → diagrams and supporting visuals (wireframes / flows / screenshots)

---

## How to Run (SQL Server)
Run scripts in this order:
1. `sql/01_schema.sql`
2. `sql/02_seed_data.sql`
3. `sql/03_bp5_inbound_dashboard_queries.sql` (Inbound dashboard KPIs + delayed shipment drill-down)
4. `sql/04_bp6_inventory_accuracy_queries.sql` (Accuracy KPIs + mismatch reports)

> Recommended: execute in **SQL Server Management Studio (SSMS)** or **Azure Data Studio**.

---

## Key Outputs
- **Delayed Shipments:** delayed shipment identification + drill-down details (aligned to BRD logic)
- **Inbound Performance:** on-time delivery %, inbound trends, supplier delay analysis
- **Inventory Control:** inventory accuracy % by location/category + mismatch variance action list

---

## Notes / Limitations
This repo focuses on requirements + SQL implementation for KPI reporting and traceability. Items such as carrier integrations, detailed QC workflows, and financial valuation are intentionally out of scope per the BRDs.
