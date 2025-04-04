# Summary
This repo provides documentation, guides, and code examples for various healthcare quality measures and groupers.

While there are other sources that provide measure specs, this repo is designed to provide concrete implementation details.

**Disclaimer**
The code in this repository is provided "as is," without any express or implied warranties. The examples are intended for educational and informational purposes only and are not officially endorsed by, or affiliated with, any healthcare quality measurement organization. Use this code at your own risk. It is recommended that you perform your own testing and validation before using it in any production environment.

For an authoritative source, see the [Partnership for Quality Measurement](https://p4qm.org/measures).

# Code Sets
Many measures and groupers require code sets. We link to these where appropriate, but you may contact tbabineau@newvoltsolutions.com if you would like these in a more friendly format.

Unless otherwise specified, we will use:
- ICD-10-CM for diagnosis codes and external causes of morbidity
- ICD-10-PCS for inpatient procedure codes
- CPT (HCPCS Level I) for outpatient procedure codes

# Data Formats
Unless otherwise specified, calculations assume source data is using a patient encounter/discharge data format (but this input can also be derived from Claims Data in most cases).

The general format is described by HCUP:
* [State Inpatient Databases (SID)](https://hcup-us.ahrq.gov/db/state/siddbdocumentation.jsp)
* [State Ambulatory Surgery and Services Databases (SASD)](https://hcup-us.ahrq.gov/db/state/sasddbdocumentation.jsp)
* [State Emergency Department Databases (SEDD)](https://hcup-us.ahrq.gov/db/state/sedddbdocumentation.jsp)

Note that these can vary slightly from state to state.

For concrete examples and documentation, we will use the [California Department of Health Care Access and Information (HCAI) fields](https://hcai.ca.gov/data/submit-data/patient-data/) with some minor edits to make more general (e.g. using `facility_id` instead of `hcai_id`).
- [Inpatient HCAI Submission Format](https://hcai.ca.gov/data/submit-data/patient-data/inpatient-reporting/)
- [Outpatient HCAI Submission Format](https://hcai.ca.gov/data/submit-data/patient-data/edas-reporting/)

See [data-formats/patient-encounter/README.md](./data-formats/patient-encounter/README.md) for more details.

# Example Code/SQL Dialect
For concrete examples, we will use the [ClickHouse SQL dialect](https://clickhouse.com/docs/sql-reference) unless otherwise specified, but note that the code will have strong interoperability with other SQL dialects like Postgres, MySQL, or MS SQL Server.

We choose ClickHouse for a couple reasons
- This is what we use at NewVolt
- Descriptive built-in functions and strong user-defined function capabilities that make code more readable
- Alias and materialized columns that make code more readable

# Groupers vs Measures
In general, groupers will refer to categorizations—such as DRGs or CCSRs—and measures will refer to quality measures—like readmission rates.

In some cases, we'll use "measure" more loosely. For example, we have Sepsis under measures, but technically the final measure would be something like "mortality rate for patients with sepsis."