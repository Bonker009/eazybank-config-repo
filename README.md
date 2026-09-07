# eazybank-config-repo

Git-backed configuration for the **cards** microservice.

Served by the EazyBank Spring Cloud Config Server (port 8071), which runs a
**composite** backend:

| Order | Backend | Serves                                  |
|-------|---------|-----------------------------------------|
| 1     | git     | this repo -> `cards` (highest priority) |
| 2     | native  | `classpath:/config` -> `accounts`, `loans` |

First backend in a composite wins, so `cards*.yml` here overrides the
`cards*.yml` still present in the config server's classpath. Those classpath
files remain as an offline fallback and as a visible contrast during the demo.

## Files

| File             | Profile   |
|------------------|-----------|
| `cards.yml`      | default   |
| `cards-qa.yml`   | qa        |
| `cards-prod.yml` | prod      |

## Demo

Change a value here, commit, push, then:

    curl -X POST http://localhost:9000/actuator/busrefresh

...and re-read `GET http://localhost:9000/api/contact-info`.
No restart, no redeploy.
