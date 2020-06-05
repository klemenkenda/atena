# Atena
Atena server is primarily intended to support environmental projects (NAIADES, Water4Cities, PerceptiveSentinel and enviroLENS) and any other projects that develop solutions related to processing sensor and other time-series data, data fusion, time-series prediction and stream mining.

## Data and File System
The 6.9T disk is mounted on `/mnt/data`.

Use this to:
* store your files/data
* docker images
* backups
* project-dedicated repos
* running web services

To store personal data, use `/mnt/data/users/username`.
To store project-related stuff, use `/mnt/data/projects/projectname`.
To store data for running services, use `/mnt/data/services/servicename`.


### File transfer
For file transfer use scp (e. g. WinSCP).
For development environment use VS Code with MS extension [Remote Development](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.vscode-remote-extensionpack). 


## Software
Any intended new installation of a software should be reported to Slack. 
Some utilities are already installed (`tmux`, `git`).

### Web server
Installed is Apache2 web server.
Config location: `/etc/apache2`.
Use `sudo apache2ctl` for controlling the component (i.e. restarting).
Use Apache2 to create proxies and similar.

### Python

| Version | Python Shell | Pip command |
| ------- | ------------ | ----------- |
| 3.8.2   | `python3`    | `pip3`      |

Virtual environment is installed. Use it! Documentation is [here](https://virtualenv.pypa.io/en/latest/index.html).

### Anaconda3
Anaconda3 is installed in `/opt/anaconda3`. 

To use it, you have to change your `.bashrc`, so that you add the following lines to the end:
```sh
# >>> conda initialize >>>
# !! Contents within this block are managed by 'conda init' !!
__conda_setup="$('/opt/anaconda3/bin/conda' 'shell.bash' 'hook' 2> /dev/null)"
if [ $? -eq 0 ]; then
    eval "$__conda_setup"
else
    if [ -f "/opt/anaconda3/etc/profile.d/conda.sh" ]; then
        . "/opt/anaconda3/etc/profile.d/conda.sh"
    else
        export PATH="/opt/anaconda3/bin:$PATH"
    fi
fi
unset __conda_setup
# <<< conda initialize <<<
```

After this you either re-login into your account or source the .bashrc with `source .bashrc`. Example of this file is also available on `/mnt/data/sw/anaconda.rc`, which you can also source with `source /mnt/data/sw/anaconda.rc`.

You can then use `conda create -n myenv`. For further details check [conda documentation](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html). Virtual environments will be setup within your user. When activated, `python` and `python3` will point to the Anaconda's version of Python. To deactivate conda or a specific conda environment use `conda deactivate`.

### NodeJS
We are using [NodeJS Version Manager (nvm)](https://github.com/nvm-sh/nvm/) for managing node. Each user has his NodeJS distributions installed on a local account. `nvm` itself is installed globally and you can invoke it by running `source /mnt/data/sw/nvm.rc`. Alternatively you can copy the content of `/mnt/data/sw/nvm.rc` at the end your `~/.bashrc` file.

Table of frequently used `nvm` commands.
| Command | Description |
|:------- |:----------- |
| `nvm ls` | Lists all currently installed NodeJS versions. |
| `nvm install 12` | Installs the latest version of 12.x.y of NodeJS. |
| `nvm install 8.0` | Installs the latest version of 8.0.x of NodeJS. |
| `nvm use v12.18.0` | Uses the selected version of NodeJS (as listed in `nvm ls`). |
| `nvm uninstall v12.18.0` | Uninstalls the selected version of NodeJS. |
| `nvm deactivate` | Deactivates the current version of NodeJS. |
| `nvm install --lts` | Install the latest long-term-support (LTS) version of NodeJS. |

**Be aware to only install as little NodeJS versions on the system as needed!**

### PostgreSQL

Additional documentation is available [here](https://www.digitalocean.com/community/tutorials/how-to-install-postgresql-on-ubuntu-20-04-quickstart). PostgreSQL is installed on a default port. Ask for a username/password or to install additional modules on Slack.

* Data directory: `/mnt/data/postgresql/12/main`
* Start command: `sudo systemctl start postgresql`
* Status command: `sudo systemctl status postgresql`
* Stop command: `sudo systemctl stop postgresql`
* Running psql as default user: `sudo -u postgres psql`

### Docker
Not yet installed.

## Custom services running on Atena

Here are listed all the services running on Atena (including URL/port).

| Service Name | Description | Virtual host | Port | Caretaker |
| ------------ |:----------- | ------------ | ----:| --------- |
| iot-rapids   | IoT platform for multiple EU projects (NAIADES, Water4Cities) | atena.?.? | 80 | Klemen |
| GPS tracking | Tracking of GPS devices | atena.?.? | 8888 | Klemen |
