## SIEM

| Action                           | Sentinel                                   | Splunk                         |
| -------------------------------- | ------------------------------------------ | ------------------------------ |
| Select Data Source               | AuditLog                                   | index=AuditLog                 |
| Filter Results (Equal)           | \| where ActionType == "User Add"          | ActionType="User Add"          |
| Filter Results (Starts With)     | \| where ActionType startswith "User Add"  | ActionType="User Add*"         |
| Filter Results (Not Starts With) | \| where ActionType !startswith "User Add" | ActionType!="User Add*"        |
| Return Subset of Results         | \| take 100                                | \| head 100                    |
| Time Now                         | now()                                      | now                            |
| Add fields/columns               | \| extend NewRole = OldRow                 | \| eval NewRole = OldRow       |
| Rename fields/columns            | \| project-rename NewRole = OldRow         | \| rename NewRole = OldRow     |
| Keep certain fields              | \| project Id, User, Description           | \| table Id, User, Description |
| Count by value                   | \| summarize count() by EventID            | \| stats count by EventID      |
| Sort (Ascending)                 | \| sort by count asc                       | \| sort by -count              |
| Sort (Descending)                | \| sort by count desc                      | \| sort by count               |
| Filter field for multiple values | \| where EventCode in (4624, 4625)         | EventCode IN (4624, 4625)      |

*** 
[Return to home page](../README.md)