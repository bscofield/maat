## SSH
SSH is allowed to staging instances.

Ideally, SSH would not be allowed to production instances. It is difficult to guarantee upfront that it won't be necessary, however, so: SSH allowed to production instances. Any SSH session to a production instance generates an alert / incident / exception / what-have-you, however, and the full session is recorded so that the infrastructure can be updated to render that need inert in the future.

## Logging
Comprehensive, centralized logging is critical to Maat. All servers forward their logs to a central location where they are aggregated, archived, and made searchable.

## Monitoring
All servers share a base level of monitoring -- filesystem, CPU, etc. These metrics flow to a centralized, modern monitoring system along with utility (e.g., nginx) and application metrics.
