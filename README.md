# unraid-opencloud
Unraid Community Applications (CA) template for OpenCloud (opencloud.eu).
# OpenCloud (Heinlein) Unraid Template

This is a modular Unraid CA template for [OpenCloud](https://opencloud.eu/en) by Heinlein Gruppe. It is designed for users who, like Unraid users, prefer to manage services in separate, external containers.

This template **does not** include a database, Redis, or OnlyOffice. It is designed to **connect** to your existing external Docker containers for these services.

## ⚠️ Mandatory First-Time Setup (INIT Command)

OpenCloud requires a manual `init` command to be run **BEFORE** you start the container for the first time. If you skip this, the container will fail to start.

1.  Open the Unraid Terminal.
2.  Copy and paste the following command, but **edit the paths** to match your Unraid setup.
3.  Choose a strong admin password.

```bash
docker run --rm -it \
 -v [YOUR_CONFIG_PATH]:/etc/opencloud \
 -v [YOUR_DATA_PATH]:/var/lib/opencloud \
 -e IDM_ADMIN_PASSWORD=[YOUR_SECURE_PASSWORD] \
 opencloudeu/opencloud-rolling:latest init
