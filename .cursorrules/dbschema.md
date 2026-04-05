# Database Schema: policies.db

This database manages medical insurance policies, drug coverage criteria, and clinical requirements.

## Table: policies
The central master table containing metadata for each insurance policy.

| Column | Data Type | Description |
| :--- | :--- | :--- |
| `id` | INTEGER | Primary Key (Autoincrement). |
| `source_filename` | TEXT | Unique name of the source document. |
| `payer` | TEXT | Insurance entity (e.g., Blue Cross NC). |
| `policy_id` | TEXT | Unique identifier for the policy. |
| `policy_title` | TEXT | Full title of the medical policy. |
| `document_type` | TEXT | Category (e.g., "single_drug_policy"). |
| `effective_date` | TEXT | Effective date of the policy. |
| `revision_date` | TEXT | Last revision date. |
| `prior_auth_required` | INTEGER | Boolean (0/1) for prior authorization status. |
| `approval_duration_initial` | TEXT | Initial timeframe for drug approval. |
| `approval_duration_renewal` | TEXT | Renewal timeframe for drug approval. |
| `site_of_care_restrictions` | TEXT | Requirements for where the drug is administered. |
| `general_requirements` | TEXT | **JSON array** of high-level clinical criteria. |
| `preferred_products` | TEXT | **JSON array** of preferred medication alternatives. |
| `policy_changes` | TEXT | **JSON array** tracking historical policy updates. |
| `raw_text` | TEXT | Unprocessed text extracted from the source. |

---

## Table: drugs
Stores drug-specific data associated with a policy, supporting individual drugs and drug lists.

| Column | Data Type | Description |
| :--- | :--- | :--- |
| `id` | INTEGER | Primary Key (Autoincrement). |
| `policy_id` | INTEGER | Foreign Key referencing `policies(id)`. |
| `generic_name` | TEXT | Generic name of the medication. |
| `brand_names` | TEXT | **JSON array** of associated brand names. |
| `hcpcs_codes` | TEXT | **JSON array** of billing codes. |
| `is_biosimilar` | INTEGER | Boolean (0/1) indicating biosimilar status. |
| `reference_product` | TEXT | The original product for a biosimilar. |
| `hcpcs_code` | TEXT | Single billing code (used for master list entries). |
| `drug_name` | TEXT | Formal name of the drug. |
| `description` | TEXT | Clinical or technical description. |
| `coverage_level` | TEXT | Tier or coverage status (e.g., "Preferred"). |
| `notes` | TEXT | Miscellaneous clinical or billing notes. |
| `covered_alternatives` | TEXT | **JSON array** of covered substitutes. |

---

## Table: covered_indications
Defines the medical conditions and requirements for coverage.

| Column | Data Type | Description |
| :--- | :--- | :--- |
| `id` | INTEGER | Primary Key (Autoincrement). |
| `policy_id` | INTEGER | Foreign Key referencing `policies(id)`. |
| `indication_name` | TEXT | Name of the medical condition. |
| `clinical_criteria` | TEXT | **JSON array** of specific diagnostic requirements. |
| `required_combination_regimens` | TEXT | **JSON array** of other drugs needed for therapy. |
| `icd10_codes` | TEXT | **JSON array** of relevant diagnosis codes. |
| `applies_to_products` | TEXT | **JSON array** of drugs affected by this indication. |

---

## Table: excluded_indications
Lists scenarios or conditions specifically denied for coverage.

| Column | Data Type | Description |
| :--- | :--- | :--- |
| `id` | INTEGER | Primary Key (Autoincrement). |
| `policy_id` | INTEGER | Foreign Key referencing `policies(id)`. |
| `description` | TEXT | Description of the excluded medical scenario. |

---

## Table: step_therapy
Outlines "fail-first" protocols required before drug approval.

| Column | Data Type | Description |
| :--- | :--- | :--- |
| `id` | INTEGER | Primary Key (Autoincrement). |
| `policy_id` | INTEGER | Foreign Key referencing `policies(id)`. |
| `required_prior_drugs` | TEXT | **JSON array** of drugs to be tried first. |
| `condition_description` | TEXT | Narrative of the step therapy protocol. |
| `applies_to_products` | TEXT | **JSON array** of drugs subject to these rules. |

---

## Table: dosing_limits
Defines the maximum quantity and frequency allowed for medications.

| Column | Data Type | Description |
| :--- | :--- | :--- |
| `id` | INTEGER | Primary Key (Autoincrement). |
| `policy_id` | INTEGER | Foreign Key referencing `policies(id)`. |
| `description` | TEXT | Context for the dose (e.g., "Maintenance"). |
| `max_dose` | TEXT | Maximum amount per administration. |
| `frequency` | TEXT | How often the drug can be administered. |
| `max_units_per_period` | TEXT | Total units allowed in a specific timeframe. |