Title: Warehouse Inbound & Inventory Accuracy (SQL Server) — BRD to KPI Reporting

Overview
This project models and implements a warehouse inbound receiving workflow and KPI reporting layer, covering inbound shipment capture (BP-2), GRN creation (BP-3), inventory posting job behavior (BP-4), inbound/delayed shipments dashboard (BP-5), and inventory accuracy KPI reporting from physical counts (BP-6).

Business problem
Inbound receiving and inventory updates were spreadsheet-driven, causing errors, low visibility into delays, and reduced inventory accuracy.

What I built (scope)
	•	BP-2: Inbound shipment capture rules (validations, duplicate prevention, status)
	•	BP-3: GRN header/line capture with discrepancy handling (Short/Over/Damaged/OK)
	•	BP-4: Inventory posting logic (Complete + unposted only, audit via stock movement, prevent double posting)
	•	BP-5: Inbound dashboard metrics and delayed shipment drill-down
	•	BP-6: Inventory accuracy KPI using physical_count_snapshot vs system_qty + mismatch report

Tools/skills demonstrated
Business analysis (BRD, user stories/AC, wireframes, data dictionary), Jira (Epics/Stories/Subtasks), SQL Server (schema design, seeded dataset, T-SQL queries), UAT design and traceability.

How to run (SQL Server)
	1.	Run sql/01_schema.sql
	2.	Run sql/02_seed_data.sql
	3.	Run dashboard queries in sql/03_bp5_inbound_dashboard_queries.sql
	4.	Run accuracy queries in sql/04_bp6_inventory_accuracy_queries.sql

Key outputs
	•	Delayed shipments (definition aligned to BRD)
	•	On-time delivery %, inbound trends, supplier delay analysis
	•	Inventory accuracy % by location/category + mismatch action list

Repo map
	•	/docs contains BRDs, wireframes, data dictionaries, and UAT
	•	/sql contains schema, seed data, and reporting queries

Limitations (as per BRDs)
Out-of-scope items such as carrier integrations, detailed QC workflows, and financial valuation are not implemented.

Future improvements
(Optional, keep realistic): Power BI dashboard built on these queries; automated posting stored procedure; role-based access; damaged stock location handling.