# SQL Errors

## EX 2: Incident Count IP vs. CLosed

Catalog Error: Scalar Function with name to_char does not exist! Did you mean "chr"? LINE 15: to_char(month, 'YYYY-MM') AS month_label, month, status, incident_count FROM incident_status ORDER BY month, status... ^

Catalog Error: Scalar Function with name format_timestamp does not exist! Did you mean "make_timestamp"? LINE 18: FORMAT_TIMESTAMP('%Y-%m', month) AS month_label, in_progress_count, closed_count FROM monthly_counts ORDER BY month;... ^

# WBG Errors

## EX 2: Incident Count IP vs. CLosed

Error: Parser Error: SELECT clause without selection list

Error: Binder Error: Referenced column "created_date" not found in FROM clause! Candidate bindings: "incident_monthly_status.status" LINE 1: ...us FROM (SELECT \*, date_trunc('month', created_date) AS incident_monthly_statu... ^

Error: Binder Error: column "incident_count" must appear in the GROUP BY clause or must be part of an aggregate function. Either add it to the GROUP BY list, or use "ANY_VALUE(incident_count)" if the exact value of "incident_count" is not important. LINE 1: SELECT incident_count AS incident_monthly_stat... ^

Error: Binder Error: Referenced column "created_date" not found in FROM clause! Candidate bindings: "incident_monthly_status.status" LINE 1: ...us FROM (SELECT \*, date_trunc('month', created_date) AS incident_monthly_statu... ^

## Ex 4 Reader Engagement Score

Failed to create widget - Invalid field: series

Widget did not display.
