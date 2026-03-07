# Docker services

This repository is just my take on how to structure a Docker Compose project using only built-in
tools. The aim is to share single containers of common services like database or reverse-proxy,
while keeping subprojects easily manageable separately. Suited for developer environments or
single-Compose-project-per-host situations (tag: homelab homeserver).

## Requirements

[Docker Engine and CLI with Docker Compose](https://docs.docker.com/engine/install)  
Normal "rootful" installation is required.

Several service images referenced here require root at startup; however, most drop privileges during
their initialization sequence. Refer to the individual subproject READMEs for details.

**NOTE**: User namespace isolation - when only `dockerd` daemon runs as `root` -, can be enabled
with careful planning of user groups and file permissions, along with some minor subproject
customizations.  
Be aware, that enabling it retroactively requires tedious file permission migrations.

## Usage

After cloning the repository, copy these example files with new name, then customize them:
- Docker Compose _dotenv_ file containing `COMPOSE_*` and host-specific `HOST_*` environment
  variables:  
  `cp ./example.env ./.env`
- Service container default environment variables:  
  `cp ./container.default-example.env ./container.default.env`
- List of included Compose subprojects:  
  `cp ./compose.override-example.yaml ./compose.override.yaml`

**For every included Compose subproject, navigate to it's directory**, then copy the example file
containing subproject-specific overrides with new name, then customize it:  
`cp ./compose.override-example.yaml ./compose.override.yaml`  
Also, make sure that a symbolic link named `.env` exists there, and that it points to `.env` file in
the repository's root directory.

## Service catalog

- [Jellyfin](jellyfin/README.md)
- [PostgreSQL](postgres/README.md)
- [Prowlarr](prowlarr/README.md)
- [qBittorrent](qbittorrent/README.md)
- [Recyclarr](recyclarr/README.md)
- [Sonarr](sonarr/README.md)
- [Traefik](traefik/README.md)
