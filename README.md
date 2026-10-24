# docker-status-page

Per-host Docker container status dashboard, installable as a PWA. Shows at a
glance what's running on a given Docker host — no monitoring, no alerting,
no history, just a live container grid. Not to be confused with
[clbsoldev/statuspage](https://github.com/clbsoldev/statuspage), which feeds
the public aggregated status page at status.clb-sol.dev.

## Image

```
ghcr.io/clbsoldev/status-page:latest
```

Built and pushed automatically via [docker-image-template](https://github.com/clbsoldev/docker-image-template).
No digest pinning — the image always tracks the latest `python:3.14-slim`
base.

## Environment variables

| Variable           | Description                              |
|--------------------|-------------------------------------------|
| `HOST_NAME`        | Name of the Docker host this runs on       |
| `HOST_INITIALS`    | Short label shown on the dashboard         |
| `REFRESH_INTERVAL` | Poll interval in seconds                   |

## Requirements

- `/var/run/docker.sock` mounted into the container (currently `:ro`; will
  become `:rw` once start/stop/restart controls are added)

## Deployment

One instance per Docker host, deployed via the `docker_stack` Ansible role.
Each instance is modeled as its own NetBox VM object (type: Container), with
`config_context` holding the host-specific environment variables above —
not static group_vars on the `docker-hosts` group.

No authentication. Don't expose this beyond the host's own trusted network.

## Roadmap

- Per-container uptime display
- Start/stop/restart controls

## License

MIT
