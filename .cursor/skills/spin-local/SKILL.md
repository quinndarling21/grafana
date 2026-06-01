---
name: spin-local
description: Spin up the local Grafana demo app with backend and frontend hot reloading. Use when the user says "spin local", "spin the app", "start the demo app", or asks to run Grafana locally.
---

# Spin Local

## Instructions

When the user asks to spin the local demo app, start Grafana from the repo root using the Shell tool. Do not ask the user to run commands manually.

## Preflight

1. Inspect the terminals folder first to see whether these processes are already running:
   - `make run`
   - `yarn start:liveReload`
2. If both are already running, do not start duplicates. Check recent output for readiness and report the app URL.
3. If frontend startup fails because dependencies are missing, run:

```sh
corepack enable
corepack install
yarn install --immutable
```

## Start Commands

Run each command from the repo root in its own long-running shell session:

```sh
make run
```

```sh
yarn start:liveReload
```

## Readiness Checks

Wait for these signals:

- Backend: `HTTP Server Listen` on port `3000`
- Frontend: `Compiled successfully`

After both are ready, verify the app responds:

```sh
curl -I http://localhost:3000/
```

Expected behavior: `http://localhost:3000/` redirects to `/login`. Share `http://localhost:3000/login` with the user when ready.

## Notes

- These processes run indefinitely until stopped.
- If port `3000` is already in use, identify the existing process before starting anything new.
- Default login is `admin` / `admin`.
