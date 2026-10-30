# checks

Part of statuspage, an uptime monitor. This repo runs the checks:

- `check-scheduler` gets the monitor list from status-api and queues one probe per monitor every 30 seconds on the Redis stream `probes`.
- `probe-worker` takes probes off that stream, checks each endpoint, and writes results to the stream `results`. KEDA scales it on stream lag.
- Redis holds both streams. This team owns it.

The services in [toil-lab/status](https://github.com/toil-lab/status) serve the monitor list, read the results, and show them.

The developer agent writes the code and each service's `service.yaml`. The
DevOps agent owns `.github/`, `CODEOWNERS`, and `toil.json`. A human approves
every merge. The services arrive in phase 4.
