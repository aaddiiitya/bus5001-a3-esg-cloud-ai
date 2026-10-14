# Q3 results – run 20261011T161818Z

Environment: python 3.13.15 | torch 2.11.0+cu130 | transformers 5.18.0
device: cuda Tesla T4
run id: 20261011T161818Z


Accuracy (%) on 8 messages; valid_json/json_only counts out of 8
| method                    |   category_acc |   urgency_acc |   team_acc |   valid_json |   json_only |
|:--------------------------|---------------:|--------------:|-----------:|-------------:|------------:|
| LLM v1 prompt             |              0 |            50 |          0 |            8 |           0 |
| LLM v2 prompt             |             75 |            50 |         75 |            8 |           0 |
| Zero-shot bart-large-mnli |             75 |            50 |        nan |          nan |         nan |
| Rule-based keywords       |             88 |            88 |        nan |          nan |         nan |

| id   | expected_cat          | v1_cat              | v2_cat                | zs_cat                | rule_cat              | expected_urg   | v1_urg   | v2_urg   | zs_urg   | rule_urg   | expected_team          | v1_team                    | v2_team                | expected_sens   | v1_sens   | v2_sens   | v2_review   |
|:-----|:----------------------|:--------------------|:----------------------|:----------------------|:----------------------|:---------------|:---------|:---------|:---------|:-----------|:-----------------------|:---------------------------|:-----------------------|:----------------|:----------|:----------|:------------|
| M1   | water_leak            | Infrastructure      | water_leak            | water_leak            | water_leak            | HIGH           | HIGH     | HIGH     | HIGH     | HIGH       | Facilities & Energy    | Facilities Management Team | Facilities & Energy    | LOW             | LOW       | LOW       | False       |
| M2   | waste_contamination   | Operational         | waste_contamination   | waste_contamination   | waste_contamination   | MEDIUM         | HIGH     | HIGH     | HIGH     | HIGH       | Waste & Environment    | Operations Team            | Waste & Environment    | LOW             | LOW       | MEDIUM    | False       |
| M3   | energy_waste          | Environmental       | energy_waste          | energy_waste          | energy_waste          | MEDIUM         | HIGH     | LOW      | LOW      | MEDIUM     | Facilities & Energy    | IT Support Team            | Facilities & Energy    | LOW             | LOW       | LOW       | False       |
| M4   | supplier_compliance   | Supplier Compliance | supplier_compliance   | governance_concern    | supplier_compliance   | MEDIUM         | HIGH     | CRITICAL | HIGH     | MEDIUM     | Procurement            | Sustainability Team        | Procurement            | MEDIUM          | MEDIUM    | HIGH      | True        |
| M5   | accessibility_barrier | Security            | accessibility_barrier | accessibility_barrier | accessibility_barrier | HIGH           | HIGH     | HIGH     | HIGH     | HIGH       | Facilities & Inclusion | Facility Management Team   | Facilities & Inclusion | LOW             | None      | MEDIUM    | False       |
| M6   | hazardous_disposal    | Environmental       | waste_contamination   | hazardous_disposal    | hazardous_disposal    | CRITICAL       | HIGH     | CRITICAL | HIGH     | CRITICAL   | Waste & Environment    | Environment & Safety Team  | Waste & Environment    | LOW             | LOW       | HIGH      | False       |
| M7   | other                 | Environmental       | other                 | other                 | other                 | LOW            | LOW      | LOW      | LOW      | LOW        | Sustainability Team    | None                       |                        | LOW             | None      | LOW       | False       |
| M8   | governance_concern    | Data Integrity      | energy_waste          | other                 | energy_waste          | HIGH           | HIGH     | LOW      | HIGH     | HIGH       | Governance & Ethics    | ESG Reporting Team         | Procurement            | HIGH            | MEDIUM    | MEDIUM    | False       |
