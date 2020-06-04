# Atena

## Data and File System
The 6.9T disk is mounted on `/mnt/data`.

Use this to:
* store your files/data
* docker images
* backups
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

You can then use `conda create -n myenv`. For further details check [conda documentation](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html). Virtual environments will be setup within your user. When activated, `python` and `python3` will point to the Anaconda's version of Python. To deactivate conda or a specific conda environment use `source deactivate`.

### NodeJS
Not yet installed.

### Docker
Not yet installed.

## Custom services running on Atena

Here are listed all the services running on Atena (including URL/port).

| Service Name | Description | Virtual host | Port | Caretaker |
| ------------ |:----------- | ------------ | ----:| --------- |
| iot-rapids   | IoT platform for multiple EU projects (NAIADES, Water4Cities) | atena.?.? | 80 | Klemen |
| GPS tracking | Tracking of GPS devices | atena.?.? | 8888 | Klemen |
