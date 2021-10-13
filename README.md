# Odoo Development Environment

This repository is a template to develop odoo addons with VS Code.

It's awesome, try it! 🎉

## Requirements

- [Git](https://git-scm.com/) version control system
- [Docker](https://www.docker.com/products/docker-desktop) container runtime
- [VS Code](https://code.visualstudio.com/) code editor
- [Fira Code](https://github.com/tonsky/FiraCode#download--install) font

## Setup

> If you're using Windows:
>
> Make sure that the **OpenSSH Authentication Agent** is activated and running.  
> [Here's a stackoverflow answer](https://stackoverflow.com/questions/18683092/how-to-run-ssh-add-on-windows/40720527#:~:text=Update%202019%20-%20A%20better%20solution%20if%20you%27re%20using%20Windows%2010) that explains how to enable and start it.

1. Make sure docker is up and running

2. Open a terminal and navigate to your development projects folder, e.g.

   ```bash
   cd ~/dev
   ```

3. Clone this repository (adjust `my-odoo-project` to a directory name into which you want to download this repository)

   ```bash
   git clone https://github.com/humiu/odoo-dev-env.git my-odoo-project
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

   Click the "**Reopen in Container**" button.

   > If you don't see that notification click on the small bell icon at the very right of the bottom status bar in VS Code. This will open a list of all VS Code notifications.
   >
   > If you still can't see the "Reopen in Container" button open the **Command Palette** (either via **View** → **Command Palette** or with the shortcut <kbd>CTRL</kbd>+<kbd>SHIFT</kbd>+<kbd>P</kbd> on Windows and Linux or <kbd>⌘</kbd>+<kbd>SHIFT</kbd>+<kbd>P</kbd> on Mac) and type "**Reopen in Container**". Choose "**Remote-Containers: Reopen in Container**" with the arrow keys (if it's not already selected) and then hit the enter key (<kbd>⏎</kbd>).

7. Wait until the new Odoo development environment is built (check progress bar of "_Starting Dev Container (show log): Installing server_" notification)

8. If you don't already have the [Python](https://marketplace.visualstudio.com/items?itemName=ms-python.python) VS Code extension installed in VS Code, it'll be installed automatically in the development container. After it got installed you have to enable it by going to the **Extensions** panel in the sidebar, scroll down inside the **INSTALLED** section until you see the Python extension and click the "**Reload Required**" button. If it still says "Installing" wait until the installation is finished and then click the "**Reload Required**" button.

9. Open a new terminal in VS Code (the [integrated terminal](https://code.visualstudio.com/docs/editor/integrated-terminal) of VS Code)

10. Generate a new addon / module from a template with the `odoo-bin` [scaffold subcommand](https://www.odoo.com/documentation/15.0/developer/misc/other/cmdline.html#scaffolding)

    ```bash
    odoo-bin scaffold my_module addons
    ```

11. To debug your code go to **Run** → **Start Debugging** or go to the debugging panel in the sidebar and start the **attach to odoo process** task.

12. To use your own git repository:

    12.1. Create a git repository on any git hosting service like [GitHub](https://github.com/) or [GitLab](https://gitlab.com/) or on you own server

    12.2. Remove the current `origin` from this repository

    ```bash
    git remote remove origin
    ```

    12.3. Add your own git repository URL to this repository. E.g.

    ```bash
    git remote add origin git@github.com:yourusername/my-odoo-project.git
    ```

    12.4. The first time you want to push your odoo project to your own repository you have to specify the upstream and branch name

    ```bash
    git push --set-upstream origin main
    ```

## Usage

### Odoo

- **URL**: http://localhost:8069/
- **Master Password**: `MasterPassword`

### Odoo application logs

1. Go to the **Remote Explorer** extension in the VS Code sidebar

2. Right click the odoo container (the container under **CONTAINERS** → **Dev Containers** with the green checkmark)

   > If you can't see any containers make sure that you are in the containers view. There might be a dropdown next to the **REMOTE EXPLORER** label at the top of the sidebar where you can select **Containers**.

3. Select **Show Container Log**

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

1.  Download the Odoo Enterprise repository

2.  Build your own Odoo Enterprise docker image.  
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

3.  Then build the image. E.g.

    ```bash
    docker build -t odoo-enterprise:latest .
    ```

4.  Update the `ODOO_BASE_IMAGE` variable in the [docker-compose.yaml](./.devcontainer/docker-compose.yaml) file to your new Odoo Enterprise docker image name (e.g. `odoo-enterprise:latest`)

5.  If you have already built a Odoo development environment before:

    5.1. Make sure that you're not connected to it (e.g. by closing VS Code or by calling the "**Remote-Containers: Reopen Folder Locally**" command in the Command Palette)

    5.2. Delete the development environment (append a `-v` at the following command if you also want to delete all your data in your local Odoo dev env)

    ```bash
    docker compose --project-name odoo_dev_env down
    ```

    5.3. Delete the docker image

    ```bash
    docker image rm odoo-local:dev
    ```

6.  (Re)start VS Code, open your Odoo dev env folder and click the "**Reopen in Container**" button in the notification.
