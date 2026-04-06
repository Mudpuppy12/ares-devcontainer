# AresMUSH dev container (Cursor)

This repository provides a **Dev Container** configuration for developing **[AresMUSH](https://www.aresmush.com/)** locally inside Docker, using **Cursor** (or VS Code) with the Dev Containers extension.

The container image is based on Ubuntu (Jammy), adds an `ares` user with passwordless `sudo`, and installs the runtimes and services typically needed for the game engine, API, and web portal.

## What you get

- **Ruby** (3.3.x), **Node.js** (18.x), **Python**, **Git**, and **Azure CLI** (via Dev Container features)
- **nginx** and **redis-server** installed after the container is created
- **Port 80** forwarded for the web stack (nginx config proxies `/api/` and `/websocket` to the game’s usual local ports)
- Workspace-friendly symlinks from `/home/ares/` into your checked-out `aresmush` and `ares-webportal` trees (see below)

## Prerequisites

- [Docker](https://docs.docker.com/get-docker/) running on your machine
- [Cursor](https://cursor.com/) with the **Dev Containers** support (same idea as the [VS Code Dev Containers extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers))

## Repository layout

Keep the AresMUSH game and web portal as subfolders of this repo (as in this template):

- `aresmush/` — clone or place the AresMUSH game code here
- `ares-webportal/` — clone or place the Ares web portal here

The placeholder READMEs under those directories remind you to clone the upstream repos after the container is available.

## Opening in Cursor

1. Clone this repository and ensure `aresmush` and `ares-webportal` are populated (or clone them after the container starts into those paths).
2. In Cursor, **File → Open Folder** and select this repository’s root (the folder that contains `.devcontainer/`).
3. Run **Dev Containers: Reopen in Container** (command palette). Wait for the image build and `postCreate` / `postStart` steps to finish.
4. Inside the container, follow normal AresMUSH setup for running the game and portal; nginx on port **80** is intended to sit in front of the portal and proxy API/WebSocket traffic.

## Workspace path note

`postStartCommand` in `.devcontainer/devcontainer.json` creates symlinks under `/home/ares` into `aresmush/` and `ares-webportal/` using **`${containerWorkspaceFolder}`**, which Dev Containers expands to the workspace root inside the container (for example `/workspaces/ares-devcontainer` when you open this repo by that folder name). You do not need to edit paths for a different local folder name.

## Files of interest

| Path | Purpose |
|------|--------|
| `.devcontainer/devcontainer.json` | Dev Container definition, features, lifecycle commands, port **80** forwarding |
| `.devcontainer/Dockerfile` | Base image, `ares` user, `/var/www/html` ownership |
| `nginx.default` | Reference nginx site (API/WebSocket upstreams, static portal) |

For upstream AresMUSH documentation, installation, and game-specific steps, see the official AresMUSH site and the READMEs in your `aresmush` and `ares-webportal` clones once added.
