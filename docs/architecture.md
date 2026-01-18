config_assessment_platform/
│
├── backend/
│   ├── app/
│   │   ├── main.py                  # FastAPI entrypoint
│   │   ├── api/
│   │   │   ├── __init__.py
│   │   │   ├── auth.py              # Login, session management
│   │   │   ├── assets.py            # CRUD for infra assets
│   │   │   ├── assessment.py        # Start compliance checks
│   │   │   ├── risk.py              # Risk calculation endpoints
│   │   │   ├── reports.py           # Generate/download reports
│   │   │
│   │   ├── core/
│   │   │   ├── config.py            # Config settings
│   │   │   ├── security.py          # Password hashing, session keys
│   │   │   └── logging.py           # Unified logging
│   │   │
│   │   ├── collectors/
│   │   │   ├── __init__.py
│   │   │   ├── ssh_collector.py     # Secure Linux SSH collection
│   │   │   ├── winrm_collector.py   # Windows read-only collection
│   │   │   ├── collector_factory.py # Return correct collector per asset type
│   │   │   └── file_registry.py     # Allow-list of config files per asset type
│   │   │
│   │   ├── parsers/
│   │   │   ├── __init__.py
│   │   │   ├── sshd_parser.py
│   │   │   ├── cron_parser.py
│   │   │   ├── nginx_parser.py
│   │   │   ├── windows_services_parser.py
│   │   │   └── generic_parser.py   # Common logic for all outputs
│   │   │
│   │   ├── models/
│   │   │   ├── __init__.py
│   │   │   ├── asset.py             # Asset metadata
│   │   │   ├── config_fact.py       # Parsed configuration facts
│   │   │   ├── finding.py           # Compliance finding per asset
│   │   │   └── risk_item.py         # Node/edge for misconfig graph
│   │   │
│   │   ├── compliance/
│   │   │   ├── __init__.py
│   │   │   ├── rule_engine.py       # Applies CIS/NIST rules to config facts
│   │   │   ├── cis_rules/           # YAML definitions for CIS
│   │   │   │   ├── ssh.yml
│   │   │   │   ├── cron.yml
│   │   │   │   └── nginx.yml
│   │   │   └── nist_mapping.py      # Map CIS findings to NIST controls
│   │   │
│   │   ├── scoring/
│   │   │   ├── __init__.py
│   │   │   ├── asset_score.py       # Compute % compliance
│   │   │   └── severity_weights.py  # Weighting scheme per misconfig
│   │   │
│   │   ├── risk/
│   │   │   ├── __init__.py
│   │   │   ├── misconfig_graph.py   # Build graph of misconfigurations
│   │   │   ├── scenario_generator.py # Generate plausible attack paths (rule-based)
│   │   │   └── risk_calculator.py   # Compute likelihood × impact per scenario
│   │   │
│   │   ├── llm/
│   │   │   ├── __init__.py
│   │   │   ├── client.py            # GPT API wrapper
│   │   │   ├── prompt_templates.py  # Safe, bounded prompts
│   │   │   └── explanation_engine.py # Generate textual explanation & mitigation
│   │   │
│   │   ├── reports/
│   │   │   ├── __init__.py
│   │   │   ├── report_builder.py    # Combine compliance + risk + graphs
│   │   │   └── templates/           # Markdown or HTML templates
│   │   │       └── report.md
│   │   │
│   │   └── storage/
│   │       ├── __init__.py
│   │       ├── database.py          # PostgreSQL connection
│   │       └── repositories.py      # Asset, findings, report CRUD
│   │
│   ├── requirements.txt
│   └── README.md
│
├── frontend/
│   ├── src/
│   │   ├── components/
│   │   │   ├── AssetCard.js
│   │   │   ├── AssessmentAccordion.js
│   │   │   ├── RiskGraph.js         # Cytoscape.js implementation
│   │   │   ├── ReportTable.js
│   │   │   └── ComplianceGauge.js
│   │   ├── pages/
│   │   │   ├── Login.js
│   │   │   ├── MyInfra.js
│   │   │   ├── Assessment.js
│   │   │   ├── Risk.js
│   │   │   └── Reports.js
│   │   └── utils/
│   │       └── api.js               # REST API calls to FastAPI backend
│   └── package.json
│
└── docs/
    ├── architecture.md
    ├── methodology.md
    └── evaluation.md