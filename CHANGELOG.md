# Changelog

## 2026-10-23 — implemented admin/audit ownership

- Replaced the implied empty admin deployment with explicit ownership of the real Go `cmd/admin` runtime built from `user-notification-service` using TARGET=admin.
- Added protected user search/ban/unban, durable sanitized audit, delivery history/replay and owner-isolated quarantine/corrected replay. All commands require authoritative live sessions, MFA and permissions; no cross-service SQL or fake cloud controls.
- Documented independent audit database migrations, generated internal contracts, bounded TLS/token clients, durable command outcomes and explicit external gates.

The integration controller exercised actual HTTPS/MFA administrative paths with real identity, PostgreSQL, Kafka and Mailpit, including ban/unban/audit and replay. Owning Go verification passed on Go 1.26.10 with real PostgreSQL/Kafka race tests and all command builds; actual scratch-image Go executable scanning reported zero HIGH/CRITICAL findings. SMTP outage recovery, duplicate/poison/corrected replay, actual worker invalid-recipient failure/Prometheus alert and a trace across all five services were observed locally.

These results do not establish exactly-once SMTP or production readiness. Genuine Telegram credentials/test chat and externally reachable authenticated webhook remain external prerequisites. Remote CI was not run and requires an explicit immutable contracts revision matching the pinned tree digest. No cloud or remote publication operations were performed.
