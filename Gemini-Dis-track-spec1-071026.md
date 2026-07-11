TECHNICAL SPECIFICATION DOCUMENT
Project Sentinel-Trace: Next-Generation Agentic Medical Device Traceability & Compliance Platform for Regulatory Enforcement
1. Executive Vision & System Architecture
1.1 Product Concept
Project Sentinel-Trace is an enterprise-grade, agentic regulatory intelligence web application designed exclusively for Food and Drug Administration (FDA/TFDA) enforcement officers, medical device specialists, and border control auditors. The platform ingests heterogeneous supply chain datasets—covering entry-port purchase logs, secondary distribution manifests, and geographic hospital networks—to instantly reconstruct end-to-end device lifecycles, detect systemic structural anomalies, flag compliance evasions, and draft legal-grade enforcement reports.

At its core, the application shifts medical device tracking from reactive database querying to proactive agentic reasoning. Powered by advanced Large Language Models (LLMs), the platform acts as a virtual co-investigator, analyzing raw data, reasoning through temporal and geospatial anomalies, and generating high-fidelity, regulatory-compliant documentation tailored to specific agency standards.

1.2 System Topology
The platform implements a decoupled, event-driven microservices architecture built for high-throughput data processing and sub-second agentic feedback loops. The system layout consists of four core tiers:

[ Data Ingestion Layer ]  --> Multi-Format Parsing Engine (CSV, MD, JSON)
             |
             v
[ Orchestration Layer ]  --> Agentic Workflow State Machine & Vector Memory Cache
             |
             v
[ Processing Layer ]     --> LLM Model Router & RAG Semantic Query Hub
             |
             v
[ Presentation Layer ]   --> Dual-Pane Interactive Workspace & GIS Spatial Analytics Panel
Data Ingestion Layer: An asynchronous multi-format streaming parser that accepts untrusted files, normalizes unstructured markdown tables, handles messy delimiters, and builds deterministic data structures in temporary memory buffers.

Agentic Orchestration Layer: Powered by an active state-machine graph (e.g., built via LangGraph concepts), managing multi-turn planning, verification loops, short-term session state, and persistent data-frame caching.

LLM Processing Layer: A modular model routing hub natively optimized for gemini-3.1-flash-lite as the high-throughput, low-latency reasoning engine, with dynamic configuration toggle options for flagship models like gemini-3.1-pro or alternative cloud-hosted LLM clusters.

Presentation Workspace: A dual-pane user interface implementing real-time streaming markdown editors, contextual text-to-code components, and native exports.

2. Data Ingestion & Normalization Engine
2.1 Multi-Format Data Ingestion Pipeline
Regulatory data is notoriously inconsistent, often distributed across legacy institutional mainframes, manual spreadsheets, or text-heavy email attachments. The ingestion pipeline provides a unified interface capable of processing file uploads or raw text copy-pasting across three distinct data shapes:

+--------------------+---------------------------------------------------------------+
| Input File Format  | Processing Pipeline Strategy                                  |
+--------------------+---------------------------------------------------------------+
| Comma-Separated    | - Asynchronous streaming chunk parser with sniffing.          |
| Values (.csv)      | - Auto-detects dialects, quotes, and encodings (UTF-8/Big5).  |
|                    | - Maps to typed memory vectors.                               |
+--------------------+---------------------------------------------------------------+
| JavaScript Object  | - Validates JSON schemas against OpenAPI structures.           |
| Notation (.json)   | - Normalizes nested structures, flatter maps arrays.          |
|                    | - Standardizes key names via semantic aliases.                |
+--------------------+---------------------------------------------------------------+
| Markdown Tables    | - Regular expression tabular extraction engine.               |
| (.md / .txt)       | - Strips decorative markers, structural pipes, alignments.     |
|                    | - Reconstructs rectangular tabular arrays from plain text.   |
+--------------------+---------------------------------------------------------------+
2.2 Schema Standardization & Semantic Mapping Matrix
Once raw text strings are extracted, they enter a semantic translation middleware layer. This layer uses deterministic dictionary mappings combined with fuzzy string matching to map user columns into the system's strict internal data models.

2.2.1 Purchase Dataset Core Data Model
Internal Key: purchase_id | Type: String | Allowed Mappings: 序號, Index, ID

Internal Key: filer_id | Type: String | Allowed Mappings: 申報業者, FilerCode, InstitutionID

Internal Key: receive_date | Type: ISO-Date | Allowed Mappings: 收貨日期, ReceptionDate

Internal Key: supplier_id | Type: String | Allowed Mappings: 供應商, SupplierCode

Internal Key: license_number | Type: String | Allowed Mappings: 許可證號, LicenseNo

Internal Key: product_name | Type: String | Allowed Mappings: 中文品名, 品名, DeviceName

Internal Key: udi_di | Type: String | Allowed Mappings: UDI_DI, UDID, DeviceIdentifier

Internal Key: sub_category | Type: String | Allowed Mappings: 醫療器材次類別, Category

Internal Key: batch_number | Type: String | Allowed Mappings: 產品批號, LotNumber, BatchNo

Internal Key: serial_number | Type: String | Allowed Mappings: 產品序號, SerialNo, SN

Internal Key: model_number | Type: String | Allowed Mappings: 產品型號, ModelNo, Type

Internal Key: quantity | Type: Integer | Allowed Mappings: 數量, Qty

Internal Key: unit | Type: String | Allowed Mappings: 單位, Unit

Internal Key: expiry_date | Type: ISO-Date | Allowed Mappings: 有效期間, 保存期限, ExpirationDate

2.2.2 Distribution Dataset Core Data Model
Internal Key: distribution_id | Type: String | Allowed Mappings: 序號, Index

Internal Key: distributor_id | Type: String | Allowed Mappings: 申報業者, DistributorCode

Internal Key: delivery_date | Type: ISO-Date | Allowed Mappings: 交貨日期, 出貨日期, DeliveryDate

Internal Key: recipient_id | Type: String | Allowed Mappings: 供應對象, 收貨院所, RecipientCode

Internal Key: license_number | Type: String | Allowed Mappings: 許可證號, LicenseNo

Internal Key: udi_di | Type: String | Allowed Mappings: UDID, UDI_DI

Internal Key: serial_number | Type: String | Allowed Mappings: 產品序號, SN, SerialNo

2.3 Contextual Memory Caching Mechanism
To preserve ultra-low latency profiles during interactive agent querying, uploaded datasets are processed into standard data structures and loaded into an in-memory database instance (e.g., Redis or DuckDB in-WASM for client-side deployments) pinned to the officer's active browsing session.

Large volumetric strings are converted into optimized compressed memory configurations, allowing the downstream Agentic Framework to execute lightning-fast relational operations (joins, analytical filters, temporal comparisons) via code execution tools without executing full-text context re-injection overhead inside the core LLM prompt loop.

3. Agentic Workflow Engine & Reasoning Framework
3.1 Orchestration State Machine
The core intelligence engine operates as a deterministic finite state machine wrapped around non-deterministic LLM reasoning capabilities. The system guarantees that the agent does not simply generate an unverified narrative, but systematically verifies every analytical claim against the structured datasets.

[State: INGESTION] ---> [State: STRATEGY_PLANNING] ---> [State: DATA_ANALYSIS]
                                                                  |
                                                                  v
[State: REPORTE_COMPILATION] <--- [State: CRITIQUE_LOOP] <--- [State: ANOMALY_EXTRACTION]
State: INGESTION: Data structures verified, schemas mapped, context keys generated.

State: STRATEGY_PLANNING: The agent analyzes user runtime instructions, inspects the target device selection criteria, reads the template layout, and constructs a structured analytical blueprint.

State: DATA_ANALYSIS: The agent executes programmatic query scripts against the session cache to compute baseline statistics, volume metrics, and categorical distributions.

State: ANOMALY_EXTRACTION: The agent targets anomalies using pre-built operational code definitions, identifying date inversions, mismatched ID strings, and orphaned tracking indices.

State: CRITIQUE_LOOP: The agent critiques its own generated findings against the raw facts in the cache. If a hallucination or numerical mismatch is detected, it re-runs the data analysis state.

State: REPORT_COMPILATION: The agent maps verified findings directly into the markdown target template structures, resolving dynamic variables and formatting inline typography.

3.2 Dynamic Context Engineering Protocol
To maximize the reasoning efficacy of gemini-3.1-flash-lite, the system uses an optimized prompt architecture. Instead of dumping raw data files straight into the LLM context, it structures data efficiently.

┌────────────────────────────────────────────────────────────────────────┐
│ SYSTEM SYSTEM PROMPT (Role: Lead Regulatory Auditor)                  │
├────────────────────────────────────────────────────────────────────────┤
│ USER AUDIT PARAMETERS (Target License, Category, Supplier Filters)     │
├────────────────────────────────────────────────────────────────────────┤
│ STRUCTURED CONTEXT DATA BUFFERS                                        │
│ - Compact JSON Meta-Summary (Record counts, Date ranges, Active IDs)   │
│ - Critical Datatable Truncations (Top anomalous items detected by code) │
├────────────────────────────────────────────────────────────────────────┤
│ ENFORCEMENT REPORT TEMPLATE ARCHITECTURE                               │
└────────────────────────────────────────────────────────────────────────┘
The system injects explicit analytical boundaries, instructing the model to focus on structural discrepancies, date validation, and tracking exceptions, while outputting final responses strictly in Traditional Chinese (zh-TW).

3.3 The Verification Loop & Anti-Hallucination Guardrails
To enforce absolute statistical reliability, the application deploys a programmatic validation middleware layer called the Verification Loop. When the agent completes the draft report, the system runs an automated code execution block that parses all numbers, dates, and serial codes generated in the text, cross-checking them against the underlying datasets via exact string matching.

If the agent claims that a device experienced a "36-day delay" but the calculated delta between delivery_date and receive_date in the dataset is exactly 14 days, the verification gate fails, blocks user delivery, and automatically returns a correction instruction block to the orchestration state machine.

4. User Interface Architecture & Workspace Design
4.1 Interface Layout Matrix
The user workspace is engineered to maximize productivity for regulatory specialists, minimizing navigation friction by laying out all primary operational windows within a clean, dual-pane screen layout.

+----------------─────────────────────────┼─────────────────────────────────────────+
| CONTROL & INGESTION COLUMN              | LIVE AGENTIC AUDIT WORKSPACE            |
|                                         |                                         |
| [Upload Area: Drag & Drop Ingestion]    | [Dynamic Prompt Stream & Directives]    |
| - Target Selection Filters Dropdown     |                                         |
| - Model Configuration Controller Selector| +----------------────────────────-----+ |
| - Template Manager Selection Area       | | Streaming Markdown Editor Pane       | |
|                                         | | (Real-Time Document Synthesis Output) | |
| [Interactive Global GIS Spatial Map]    | +----------------────────────────-----+ |
|                                         |                                         |
|                                         | [Download Panel Actions: MD | PDF]      |
+----------------─────────────────────────┴─────────────────────────────────────────+
4.2 Interactive Layout Components Specification
4.2.1 Data Control & Configuration Sidebar
Dropzone Core: Supports concurrent uploading of multiple files with real-time visual progress trackers and file schema validation indicator badges.

Target Selection Filters: Grouped parameter filters allowing user isolation based on Medical Device Classification (e.g., Class III), License Number (e.g., 衛部醫器輸字第030747號), Supplier Code, and Product Model Number.

Model Router Interface: A clean dropdown menu to dynamically toggle runtime model assignments (gemini-3.1-flash-lite [Default Optimization Priority], gemini-3.1-pro, etc.).

Template Configurator: A selector that lets users choose between a default blueprint, an imported empty template file, or the system's pre-built Regulatory Audit Template.

4.2.2 Live Agentic Workspace
Prompt Input Engine: An executive text input field built for inputting custom analysis parameters (e.g., "Focus specifically on identifying potential shadow-log entries originating from southern distributor hubs during April").

Dual-Pane Stream Editor: A robust split editor canvas. The left side streams incoming markdown strings directly from the active LLM worker thread. The right side lets officers modify text using rich-text tools, standard markdown shortcuts, or inline manual overrides.

Download Bar Actions: Fixed utility buttons that instantly compile the active workspace text into standard raw markdown files or structurally paginated PDF reports complete with custom government headers.

5. Three Advanced "Wow" AI Features
5.1 Dynamic Spatial Anomaly Mapping & Supply Chain Visualizer
Instead of forcing investigators to manually cross-reference postal codes and hospital names to figure out where problematic shipments are going, the application natively connects spatial intelligence with agentic analysis.

The system intercepts the spatial metadata compiled by the ingestion layer and renders an interactive Global GIS Spatial map directly in the control sidebar.

[Raw Manifest Addresses] --> [Automatic Geo-Encoding Service] --> [Leaflet / Mapbox Canvas]
                                                                           |
                                                                           v
                                                         [Interactive Risk Heatmap Elements]
When the Agent identifies a tracking anomaly—such as a data inversion or an unmapped hospital code—the system places an active risk marker on the coordinate map.

Officers can hover over these markers to open diagnostic cards detailing the anomaly type, affected serial numbers, and calculated temporal delays. They can also use drawing tools to isolate specific high-risk zones, automatically filtering down the active dataset to focus on those regions.

5.2 Real-Time "Regulatory Deviation" Self-Critique Overlay
This feature operates as a real-time regulatory compliance specialist running alongside the primary report generator. Built as a specialized background thread, it continually scores the report's text draft against official regulatory frameworks (e.g., Taiwan's Medical Device Management Act articles).

[Drafting Stream Content] --> [Background Critique Parser Engine] --> [Real-Time Deviation Metric Score]
                                                                                |
                                                                                v
                                                              [Inline Error/Highlight Highlights]
If the agent mentions a missing expiration date but fails to cite the corresponding legal article governing tracking infractions, the system highlights the text in orange. It inserts a clickable citation overlay right next to the sentence, allowing the officer to insert the correct statutory reference with a single click.

5.3 Multi-Model Forensic Consensus Engine (Adversarial Audit)
For critical cases requiring absolute legal certainty before executing field seizures or administrative penalties, officers can trigger the Multi-Model Forensic Consensus Engine.

This sets up a structured, multi-agent debate between two distinct AI configurations:

                  +---> [Auditor Agent A (Optimized for Strict Compliance)] ---+
                  |                                                            |
[Input Datasets] -+                                                            v
                  |                                                  [Consensus Output Report]
                  +---> [Defense Agent B (Optimized for Operational Risk)] ---+
Auditor Agent A: Optimized for strict, literal compliance checking. It flags even minor variations in serial number styles as potential security risks.

Defense Agent B: Configured to evaluate operational realities. It searches for logical systemic explanations, such as common hospital barcode scanning behaviors or regional transit delays.

The two models review the datasets simultaneously, highlighting discrepancies in each other's reasoning and generating a combined forensic report. This output clearly highlights areas where both models agree on an issue, alongside sections detailing alternative system interpretations.

6. Enterprise Integration, Export Architecture & Legal Chain of Custody
6.1 Downstream Export Systems Engineering
The report compilation subsystem is engineered to meet strict institutional document standards, ensuring files transfer cleanly into existing agency records.

                         +---> [Markdown Engine] ---> Standard Unicode Markdown Output (.md)
                         |
[Active Workspace Text] -+
                         |
                         +---> [Bespoke PDF Pipeline] ---> Labeled Enterprise PDF Artifact (.pdf)
Markdown Export Pipeline: Converts the active workspace text into a standard Unicode markdown file (.md). It preserves standard header structures, inline data tables, blockquotes, and regulatory highlight callouts, ensuring full compatibility with external text editors.

Bespoke PDF Generation Engine: Renders the text into a clean, print-ready document layout. It automatically handles pagination, wraps long table rows to prevent clipping, applies page numbering, and adds formal agency header blocks.

6.2 Legal Chain of Custody & Forensic Security Architecture
Because these generated reports can be used as core evidence in administrative fines or criminal smuggling trials, maintaining data integrity is a critical requirement. The application implements a strict security framework across every interaction:

Cryptographic Data Hashing: The moment a user uploads a dataset, the system generates an immutable SHA-256 hash of the file. This hash is embedded into the report's metadata footer, proving the analysis is tied directly to an unaltered copy of the original evidence.

Stateless Local-Session Ingestion: To ensure maximum confidentiality, the ingestion layer operates on a stateless model. All uploaded records, parsed tables, and transient LLM session logs are held strictly in temporary volatile memory channels.

Automated Session Purging: Closing the browser tab or idling for 15 minutes triggers an automated session purge. This securely clears the memory buffers and prevents leaks of sensitive institutional tracking data.

7. 20 Comprehensive Technical Implementation & Validation Questions
To assist the engineering and deployment teams in verifying this system configuration prior to production launch, the following 20 technical architecture validation questions must be addressed:

Ingestion Pipeline & Parsing Architecture
How will the Multi-Format Ingestion Pipeline handle malformed or non-standard Markdown tables (e.g., lines with missing pipe delimiters or irregular row spacing) without dropping data rows or crashing the parser thread?

What fallback character-encoding detection rules should be implemented to ensure the system processes legacy files using older encodings like Big5 without corrupting Chinese characters during text extraction?

How will the ingestion engine scale when processing very large datasets containing tens of thousands of rows? What are the memory limits for client-side web assembly execution versus server-side caching?

When mapping data columns, what string distance algorithms (e.g., Levenshtein Distance) or semantic synonyms will be used to ensure variations like "序號碼" or "SN碼" map correctly to the standard serial_number field?

Agentic Controls & Workflow Management
How will the LangGraph state machine handle situations where the Verification Loop repeatedly fails due to persistent agent hallucinations or calculation errors? What thresholds will trigger an explicit system alert to the user instead of an infinite correction loop?

How will the system manage context limits when using models like gemini-3.1-flash-lite on very large files? What strategies will be used to summarize data and select only the most relevant sections for analysis?

How will the system extract custom instructions from the user prompt input field and translate them into actionable changes in the agent's core analysis rules?

What parameters will the system use to evaluate the structural quality of an uploaded report template file? If a template is missing critical analytical headers, how will the agent adapt?

Dynamic Interface Components & User Interaction
How will the system maintain seamless text synchronization between the incoming streaming markdown output and manual edits made by the user in the right-hand workspace pane?

What web technology will be used to build the interactive Global GIS Spatial map? How will the mapping component render thousands of active shipment data points without causing interface lag or high memory overhead?

If an investigator uses drawing tools to filter data on the map, how will that spatial filter interact with text-based parameter selectors in the sidebar? Which filter takes priority?

What design patterns will be used to ensure the dual-pane workspace remains highly readable and easy to navigate on standard agency field laptops with limited screen space?

Advanced AI Feature Security & Architecture
How will the background critique engine scan the report text for compliance issues without interfering with the primary generation thread or exceeding API rate limits?

What prompting strategies will be used to ensure the Multi-Model Forensic Consensus Engine maintains distinct analytical viewpoints between the auditing agent and the defense agent, rather than converging prematurely on a single viewpoint?

How will the system summarize the debate between the two adversarial agents into a cohesive document that clearly presents both perspectives without confusing the reader?

How will the system verify the legal accuracy of citations suggested by the critique engine? What measures will prevent the system from suggesting outdated or fabricated statutory 
