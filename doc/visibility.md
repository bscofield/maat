## SSH
SSH is allowed to staging instances.

Ideally, SSH would not be allowed to production instances. It is difficult to guarantee upfront that it won't be necessary, however, so: SSH allowed to production instances. Any SSH session to a production instance generates an alert / incident / exception / what-have-you, however, and the full session is recorded so that the infrastructure can be updated to render that need inert in the future.

On exiting a SSH session, any files that have been changed in the app directory are cat'd and logged (since it's hard to capture editor changes in most SSH recording schemes).

## Logging
Comprehensive, centralized logging is critical to Maat. All servers forward their logs to a central location where they are aggregated, archived, and made searchable.

## Monitoring
All servers share a base level of monitoring -- filesystem, CPU, etc. These metrics flow to a centralized, modern monitoring system along with utility (e.g., nginx) and application metrics.

## Auditing
All Maat commands are logged with time, source, and user.

## Web UI
Maat includes a web interface that provides a great deal of insight into the overall system.

* It links out to the logging and monitoring interfaces (or integrates them, where that's feasible)
* It shows the deploy history for each application
* It shows the service and dependency graph for the entire system and for each component
* It shows the SSH logs (mentioned above)
* It provides management functionality -- launch new instances, deploy to production, etc.
* It shows Maat's audit trail -- overall, per application, and per user

## Command line
Maat's CLI provides visibility into some aspects of the system -- how many instances of a given application are running, etc.

## ChatOps
Maat exposes the same functionality through ChatOps that it does through the command line.
