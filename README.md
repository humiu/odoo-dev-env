# Odoo Development Environment

This repository is a template to develop Odoo addons with VS Code.

It's awesome, try it! 🎉

## Requirements

- **Windows only**: [Windows Subsystem for Linux (WSL)](https://docs.microsoft.com/en-us/windows/wsl/) Linux environment on Windows
- [Git](https://git-scm.com/) version control system
- [Docker](https://www.docker.com/products/docker-desktop) container runtime
- [VS Code](https://code.visualstudio.com/) code editor
- [Fira Code](https://github.com/tonsky/FiraCode#download--install) font

## Setup

1. Make sure all requirements are met

   1.1. Docker is up and running

   1.2. **If you haven't setup an SSH keypair yet**: To be able to forward your git authentication into the [development container](https://code.visualstudio.com/docs/remote/containers) you need to have **SSH keys** configured. This is as simple as calling the `ssh-keygen` command in your terminal and then accepting the default configurations by pressing enter multiple times. If you want to read more about it, you'll find detailed information in the main [Git documentation](https://git-scm.com/book/en/v2/Git-on-the-Server-Generating-Your-SSH-Public-Key), in the [GitHub Docs](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent), [GitLab Docs](https://docs.gitlab.com/ee/ssh/) and lots of other websites online.

   1.3. **Windows only**: Make sure that the **OpenSSH Authentication Agent** is activated and running. [Here's a stackoverflow answer](https://stackoverflow.com/questions/18683092/how-to-run-ssh-add-on-windows/40720527#40720527:~:text=Update%202019%20%2D%20A%20better%20solution%20if%20you%27re%20using%20Windows%2010) that explains how to enable and start it.

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

5. Change git remote origin

   5.1. Create a git repository on any git hosting service like [GitHub](https://github.com/) or [GitLab](https://gitlab.com/) or on you own server

   5.2. Remove the current `origin` from this repository

   ```bash
   git remote remove origin
   ```

   5.3. Add your own git repository URL to this repository. E.g.

   ```bash
   git remote add origin git@github.com:yourusername/my-odoo-project.git
   ```

   5.4. The first time you want to push your Odoo project to your own repository you have to specify the upstream and branch name

   ```bash
   git push --set-upstream origin main
   ```

6. Open it in VS Code

   ```bash
   code .
   ```

   > If you have multiple Odoo development environments (e.g. for different projects), open the [.env](./.env) file in the root directory of this repository and change the `COMPOSE_PROJECT_NAME` variable to something else than `odoo_dev_env` to prevent conflicts with your other Odoo dev envs. Also adjust the commands where `odoo_dev_env` is used in this README file accordingly.

7. A notification will popup saying something like

   > Folder contains a Dev Container configuration file. Reopen folder to develop in a container.

   Click the "**Reopen in Container**" button.

   > If you don't see that notification click on the small bell icon at the very right of the bottom status bar in VS Code. This will open a list of all VS Code notifications.
   >
   > If you still can't see the "Reopen in Container" button open the **Command Palette** (either via **View** → **Command Palette** or with the shortcut <kbd>CTRL</kbd>+<kbd>SHIFT</kbd>+<kbd>P</kbd> on Windows and Linux or <kbd>⌘</kbd>+<kbd>SHIFT</kbd>+<kbd>P</kbd> on Mac) and type "**Reopen in Container**". Choose "**Remote-Containers: Reopen in Container**" with the arrow keys (if it's not already selected) and then hit the enter key (<kbd>⏎</kbd>).

8. Wait until the new Odoo development environment is built (check progress bar of "_Starting Dev Container (show log): Installing server_" notification)

9. If you don't already have the [Python](https://marketplace.visualstudio.com/items?itemName=ms-python.python) VS Code extension installed in VS Code, it'll be installed automatically in the development container. After it got installed you have to enable it by going to the **Extensions** panel in the sidebar, scroll down inside the **INSTALLED** section until you see the Python extension and click the "**Reload Required**" button. If it still says "Installing" wait until the installation is finished and then click the "**Reload Required**" button.

10. Open a new terminal in VS Code (the [integrated terminal](https://code.visualstudio.com/docs/editor/integrated-terminal) of VS Code)

11. Generate a new addon from a template with the `odoo-bin` [scaffold subcommand](https://www.odoo.com/documentation/15.0/developer/misc/other/cmdline.html#scaffolding) and replace `<MY_ODOO_ADDON>` with the name of your new Odoo addon

    ```bash
    odoo-bin scaffold <MY_ODOO_ADDON> addons
    ```

    This command will create a new Odoo addon in the `addons` folder with the most basic files every Odoo addon needs.

12. To debug your code go to **Run** → **Start Debugging** or go to the debugging panel in the sidebar and start the **attach to Odoo process** task.

13. If you want to add more folders to the current workspace (e.g. in case you want to debug another Odoo addon contained in the Docker image), you can do that with VS Codes [multi-root Workspaces](https://code.visualstudio.com/docs/editor/multi-root-workspaces) feature. There are two ways how you can do that in a VS Code [development container](https://code.visualstudio.com/docs/remote/containers) environment:

    13.1. [From the UI](https://code.visualstudio.com/docs/editor/multi-root-workspaces#_add-folder-to-workspace): **File** > **Add Folder to Workspace**

    13.2. [From the terminal](https://code.visualstudio.com/docs/editor/multi-root-workspaces#_command-line-add): `code --add <FOLDER_NAME>` (You can multiple folders at once)

14. Adjust code formatting to your needs

    14.1. Source code is formatted automatically on every save. If you don't like that, you can turn it off in the **VS Code Settings**. Make sure the **Workspace** tab is selected in the settings. Then search for **Format On Save** and untick the checkbox. Alternatively you can go to the `.vscode/settings.json` file and change the `"editor.formatOnSave"` property to `false`.

    14.2. This project uses [Black](https://black.readthedocs.io/en/stable/index.html) for Python code formatting. If you want to change the formatting rules go to the `pyproject.toml` file in the addons folder and add or adjust rules [according to Blacks documentation](https://black.readthedocs.io/en/stable/usage_and_configuration/the_basics.html#configuration-via-a-file).

## Usage

### Odoo

- **URL**: [http://localhost:8069](http://localhost:8069)
- **Master Password**: `MasterPassword`

### Odoo application logs

1. Go to the **Remote Explorer** extension in the VS Code sidebar

2. Right click the Odoo (`odoo_dev_env_odoo_1`) container (the container with the green checkmark in the **CONTAINERS** list)

   > If you can't see any containers make sure that you are in the containers view. There might be a dropdown next to the **REMOTE EXPLORER** label at the top of the sidebar where you can select **Containers**.

3. Select **Show Container Log**

### pgAdmin

This Odoo development environment repository will setup a preconfigured pgAdmin instance for you as well.  
Just login to pgAdmin and connect to the databases you want to inspect.

- **URL**: [http://localhost:8080](http://localhost:8080)
- **Username**: `admin@pgadmin.org`
- **Password**: `PgAdminPW!`

> If the login fails with the error message "_The CSRF tokens do not match._" clear the page cache and reload the page.
>
> If your database doesn't show up, right click **Databases** (in the left sidebar of pgAdmin expand **Servers** → **Odoo Database** → **Databases**) and then **Refresh**

## Odoo Enterprise / Custom Odoo Image

If you want to use this Odoo development repository with Odoo Enterprise you have to create your own Odoo enterprise docker image.

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

4. Update the `ODOO_BASE_IMAGE` variable in the [.env](./.devcontainer/.env) file (the one in the `.devcontainer` folder) to your new Odoo Enterprise docker image name (e.g. `odoo-enterprise:latest`).

5. If you have already built a Odoo development environment before, follow the steps described in the [Troubleshooting](#troubleshooting) section.

6. (Re)start VS Code, open your Odoo dev env folder and click the "**Reopen in Container**" button in the notification.

## Shutdown Odoo Development Environment

To see the status of your Docker containers execute the following command in a terminal (doesn't have to be inside your development environment):

```bash
docker compose --project-name odoo_dev_env ps -a
```

If you close the VS Code window with your Odoo development environment the Docker containers will be stopped. The next time you open this project in VS Code everything will be back to where it was and you can continue exactly where you left off.

But you can also stop / start / restart your containers manually by appending `stop`, `start` or `restart` to the following command:

```bash
docker compose --project-name odoo_dev_env
```

To delete all containers of your Odoo development environment run:

```bash
docker compose --project-name odoo_dev_env down
```

(If you want to delete all the volumes as well, which contain all data of the Odoo development environment, append a `-v` to the command above.)

## Troubleshooting

> ⚠️ **CAUTION** ⚠️ The following steps will delete all the data of your Odoo development environment (apart from the code in the repository).
>
> If you still need the Odoo database go to the [Odoo Database Manager](http://localhost:8069/web/database/manager) and create a backup first.

1. Make sure that you're not connected to the Odoo development environment (e.g. by closing VS Code or by calling the **Remote-Containers: Reopen Folder Locally** command from the Command Palette)

2. Delete the development environment with all the data in it:

   ```bash
   docker compose --project-name odoo_dev_env down -v
   ```

3. Delete the docker image

   ```bash
   docker image rm odoo-dev:local
   ```

4. Now open the Odoo development environment again in VS Code and click the "**Reopen in Container**" button (if you're not already in the Dev Container mode). This will rebuild your Odoo Docker container and everything will be back to the default setup.

If this still doesn't fix your problem, create an issue in the [official GitHub repository](https://github.com/humiu/odoo-dev-env).
