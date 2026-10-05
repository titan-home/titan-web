# titan-web

The TITAN web UI: sign-in, chat, node management and every domain in a browser. It is published as an image that contains the built files only; the node's nginx serves them.

Part of TITAN, a self-hosted personal AI assistant, planner and tracker. The
product, architecture and rules shared by every TITAN repository are in the
`shared/` submodule ([titan-shared](shared/README.md)).

## Contents

- **Screens**: sign-in, chat with approvals, node management (health, updates, backups), then tasks, reminders, calendar, trackers, notes and memory.
- **API client** generated from `shared/contracts/`.
- **Image**: `FROM scratch` with the built files, mounted read-only by nginx.

## Status

Not started. Build-plan stages 5–6. See the [build plan](shared/docs/roadmap/plan.md).

## Getting the code

```sh
git clone --recurse-submodules https://github.com/titan-home/titan-web.git
# after a pull:
git submodule update --init
```

## Licence

Released into the public domain under [the Unlicense](LICENSE).
