# Odoo Development Environment

This repository is a template to develop odoo addons with VS Code.

It's awesome, try it! 🎉

## Requirements

- [Git](https://git-scm.com/) version control system
- [Docker](https://www.docker.com/products/docker-desktop) container runtime
- [VS Code](https://code.visualstudio.com/) code editor
- [Fira Code](https://github.com/tonsky/FiraCode#download--install) font

## Setup

1. Make sure docker is up and running

2. Open a terminal and navigate to your development projects folder, e.g.

   ```bash
   cd ~/dev
   ```

3. Clone this repository

   ```bash
   git clone git@github.com:humiu/odoo-dev-env.git
   ```

4. Change into it

   ```bash
   cd odoo-dev-env
   ```

5. Open it in VS Code

   ```bash
   code .
   ```

6. A notification will popup saying something like

   > Folder contains a Dev Container configuration file. Reopen folder to develop in a container.

   Click the **"Reopen in Container"** button.

7. Wait until the new Odoo development environment is built (check progress bar of "_Starting Dev Container (show log): Installing server_" notification)

8. Open a new terminal in VS Code (the [integrated terminal](https://code.visualstudio.com/docs/editor/integrated-terminal) of VS Code)

9. Generate a new addon / module from a template with the `odoo-bin` [scaffold subcommand](https://www.odoo.com/documentation/15.0/developer/misc/other/cmdline.html#scaffolding)

   ```bash
   odoo-bin scaffold my_module
   ```

10. To debug your code go to **Run** → **Start Debugging** or go to the debugging panel in the sidebar and start the **attach to odoo process** task

## Usage

### Odoo

- **URL**: http://localhost:8069/
- **Master Password**: `MasterPassword`

### Odoo application logs

1. Go to the **Remote Explorer** extension in the VS Code sidebar
2. Make sure **Containers** is selected in the **REMOTE EXPLORER** dropdown
3. Right click the odoo container (the container under **CONTAINERS** → **Dev Containers** with the green checkmark)
4. Select **Show Container Log**

### pgAdmin

This odoo development environment repository will setup a preconfigured pgAdmin instance for you as well.  
Just login to pgAdmin and connect to the databases you want to inspect.

- **URL**: http://localhost:8080/
- **Username**: `admin@pgadmin.org`
- **Password**: `PgAdminPW!`

> If the login fails with the error message "_The CSRF tokens do not match._" clear the page cache and reload the page.

> If your database doesn't show up, right click **Databases** (in the left sidebar of pgAdmin expand **Servers** → **Odoo Database** → **Databases**) and then **Refresh**

## Odoo Enterprise / Custom Odoo Image

If you want to use this Odoo development repository with Odoo Enterprise you have to create your own odoo enterprise docker image.

The only thing you need for that is access to the Odoo Enterprise repository.

1. Download the Odoo Enterprise repository

2. Build your own Odoo Enterprise docker image.  
   If your enterprise addons are located in the `odoo-enterprise` folder the `Dockerfile` could be as simple as that:

   ```Dockerfile
   FROM odoo:latest

   COPY --chown=odoo:odoo odoo-enterprise/ /mnt/odoo-addons/
   ```

   Or if you want the Odoo Enterprise addons as well as the Odoo Themes in your custom image your `Dockerfile` could look like that:

   ```Dockerfile
   FROM odoo:latest

   COPY --chown=odoo:odoo odoo-enterprise/ odoo-themes/ /mnt/odoo-addons/
   ```

3. Then build the image. E.g.

   ```bash
   docker build -t odoo-enterprise:latest .
   ```

4. Update the `ODOO_BASE_IMAGE` variable in the [docker-compose.yaml](./.devcontainer/docker-compose.yaml) file to your new Odoo Enterprise docker image name (e.g. `odoo-enterprise:latest`)
