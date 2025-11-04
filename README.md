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
 -e IDM_ADMIN_PASSWORD='[YOUR_SECURE_PASSWORD]' \
 opencloudeu/opencloud-rolling:latest init
````

### Example:

  * If you want your config files in `/mnt/user/appdata/opencloud-config`
  * And your cloud data (files, etc.) in your share `/mnt/user/OpenCloud`
  * And your password to be `SuperSecure123`

...your command would be:

```bash
docker run --rm -it \
 -v /mnt/user/appdata/opencloud-config:/etc/opencloud \
 -v /mnt/user/OpenCloud/:/var/lib/opencloud \
 -e IDM_ADMIN_PASSWORD=SuperSecure123 \
 opencloudeu/opencloud-rolling:latest init
```

**Only after this command runs successfully** can you proceed to install and start the container via the CA template.

## Template Configuration Notes

When you install this template from the Unraid Apps tab, make sure your paths and settings match:

  * **Appdata-Pfad (Config):** Must be **identical** to `[YOUR_CONFIG_PATH]` from the init command.
  * **Daten-Pfad (Data):** Must be **identical** to `[YOUR_DATA_PATH]` from the init command.
  * **Redis Server Host:Port:** Enter the LAN IP and port of your existing Redis container (e.g., `192.168.1.10:6379`). Use this value for both Redis fields.
  * **OnlyOffice Server URL:** Enter the full LAN URL of your existing OnlyOffice container (e.g., `http://192.168.1.11:80`).
  * **Externe URL (Reverse Proxy):** The full public URL your Nginx/Traefik proxy uses (e.g., `https://cloud.your-domain.com`).

<!-- end list -->
