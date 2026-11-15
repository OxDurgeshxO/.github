# Incident Postmortem: [Incident Title / Identifier]

- **Date of Incident**: [YYYY-MM-DD]
- **Authors**: [Incident Commander / Responders]
- **Status**: [Complete | Action Items in Progress]
- **Severity**: [Sev-1 Critical Outage | Sev-2 Partial Degradation | Sev-3 Minor Glitch]

---

## 1. Executive Summary
Brief summary of the incident: what broke, what was the user impact, how long it lasted, and what resolved it.

## 2. Impact Analysis
- **User Impact**: Number of affected sessions, failed requests, or dropped transactions.
- **Duration**:
  - Time to Detect (TTD): [X minutes]
  - Time to Acknowledge (TTA): [X minutes]
  - Time to Resolve (TTR): [X minutes]
- **Data Loss / Privacy Exposure**: [Confirmed 0 / Details if any].

## 3. Timeline (UTC)
| Timestamp (UTC) | Event Description |
|---|---|
| `14:02` | PR #123 merged containing unindexed query migration. |
| `14:05` | Elevated CPU saturation alert triggered on database primary. |
| `14:08` | On-call engineer paged and incident room opened. |
| `14:15` | Rollback initiated to container `:v1.2.3`. |
| `14:20` | Traffic stabilized, health checks returned green. |

## 4. Root Cause Analysis (5 Whys)
1. **Why did the outage occur?** The database connection pool became completely exhausted.
2. **Why was the connection pool exhausted?** A new query lacked an index on foreign key `session_id`.
3. **Why did the query lack an index?** The migration was not run against production-scale data in staging.
4. **Why was staging data insufficient?** Staging database lacked automated synthetic load fixtures.
5. **Why was synthetic load fixture missing?** Pre-merge performance benchmark gate was not mandatory in CI.

## 5. What Went Well / What Went Poorly
### What Went Well
- Automated health check alert fired within 3 minutes of saturation.
- Container rollback took under 5 minutes with zero data corruption.

### What Went Poorly
- Missing query plan validation gate in pull request CI.
- Alerting lacked explicit diagnostic pointer to the problematic SQL statement.

## 6. Action Items & Prevention
| Action Item | Type | Owner | Target Date | Tracking Issue |
|---|---|---|---|---|
| Add automated EXPLAIN query plan check to PR CI | Prevent | @engineer | YYYY-MM-DD | #456 |
| Tune database connection pool timeouts & circuit breaker | Mitigate | @devops | YYYY-MM-DD | #457 |
| Update runbook for rapid index creation under load | Detect | @sre | YYYY-MM-DD | #458 |
