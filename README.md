# OpenCloud (Heinlein) Unraid Template

This is a modular Unraid CA template for [OpenCloud](https://opencloud.eu/en) by Heinlein Gruppe. It is designed for users who, like Unraid users, prefer to manage services in separate, external containers.

This template **does not** include a database, Redis, or OnlyOffice. It is designed to **connect** to your existing external Docker containers for these services.

## ⚠️ Mandatory First-Time Setup

OpenCloud requires a manual setup **BEFORE** you start the container for the first time. If you skip this, the container will fail to start due to `permission denied` errors.

---

### Step 1: Create Directories & Set Permissions

You must manually create your configuration and data folders and give them open permissions *before* running the init command. This prevents Docker from creating them as `root` and causing permission errors.

Open the Unraid Terminal and run the following commands. **Remember to edit the paths** to match your Unraid setup.

First, create your config and data folders:

```bash
mkdir -p [YOUR_CONFIG_PATH]
mkdir -p [YOUR_DATA_PATH]
```

Next, set permissions to avoid errors (this allows the container's internal user to write to the folders):

Bash

chmod -R 777 [YOUR_CONFIG_PATH]
chmod -R 777 [YOUR_DATA_PATH]
Step 2: Run the Init Command
Now, run the init command. This will populate your config folder.

Note: If your password contains special characters like !, wrap it in single quotes (' ') to prevent a terminal error.

Bash

docker run --rm -it \
 -v [YOUR_CONFIG_PATH]:/etc/opencloud \
 -v [YOUR_DATA_PATH]:/var/lib/opencloud \
 -e IDM_ADMIN_PASSWORD='[YOUR_SECURE_PASSWORD]' \
 opencloudeu/opencloud-rolling:latest init
When asked ...certificate checking disabled?, type yes and press Enter.

Full Example:
Here is a full example if your paths are:

Config Path: /mnt/user/appdata/opencloud-config

Data Share: /mnt/user/OpenCloud

Password: Super!Secure123

Your commands in the terminal would be:

Step 1: Create folders and set permissions

Bash

mkdir -p /mnt/user/appdata/opencloud-config
mkdir -p /mnt/user/OpenCloud/
chmod -R 777 /mnt/user/appdata/opencloud-config
chmod -R 777 /mnt/user/OpenCloud/
Step 2: Run init command

Bash

docker run --rm -it \
 -v /mnt/user/appdata/opencloud-config:/etc/opencloud \
 -v /mnt/user/OpenCloud/:/var/lib/opencloud \
 -e IDM_ADMIN_PASSWORD='Super!Secure123' \
 opencloudeu/opencloud-rolling:latest init
Only after this command runs successfully can you proceed to install and start the container via the CA template.

Template Configuration Notes
When you install this template from the Unraid Apps tab, make sure your paths and settings match:

Appdata-Pfad (Config): Must be identical to [YOUR_CONFIG_PATH] from the init command.

Daten-Pfad (Data): Must be identical to [YOUR_DATA_PATH] from the init command.

Redis Server Host:Port: Enter the LAN IP and port of your existing Redis container (e.g., 192.168.1.10:6379). Use this value for both Redis fields.

OnlyOffice Server URL: Enter the full LAN URL of your existing OnlyOffice container (e.g., http://192.168.1.11:80).

Externe URL (Reverse Proxy): The full public URL your Nginx/Traefik proxy uses (e.g., https://cloud.your-domain.com).
