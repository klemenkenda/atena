# Atena
Atena server is primarily intended to support environmental projects (NAIADES, Water4Cities, PerceptiveSentinel and enviroLENS) and any other projects that develop solutions related to processing sensor and other time-series data, data fusion, time-series prediction and stream mining.

## Terminal Environment
It might be that the default terminal shell of a new user is set to `sh`. This shell works different that for instance `bash` (the `source` command does not work, etc). To change the default terminal shell of the user to `bash` run the following command and restart the terminal:
```bash
chsh -s /usr/bin/bash
```

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

### Zip and Unzip
For compressing and decompressing files use `gzip`. 

To compress the file or folders: 
```bash
# -k: keep the uncompressed files (optional)
# -l: get stats how much space was saved (optional)
gzip -k -l file
```

To decompress the zip file:
```bash
# -k: keep the compressed files (optional)
# -l: get stats of decompression (optional)
gunzip -k -l file.gz
```

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

### Elasticsearch

Elasticsearch is a search engine service. Additional documentation is available [here](https://www.elastic.co/guide/en/elasticsearch/reference/current/index.html). Elasticsearch is installed on a default port (`9200`). No username and password is required.

Before using elasticsearch, check which indexes are already in use via the following command:
```bash
curl http://localhost:9200/_aliases?pretty=true
```

* Data directory: `/mnt/data/elasticsearch/data`
* Logs directory: `/mnt/data/elasticsearch/logs`
* Configuration directory: `/etc/elasticsearch`
* Start command: `sudo systemctl start elasticsearch.service`
* Status command: `sudo systemctl status elasticsearch.service`
* Stop command: `sudo systemctl stop elasticsearch.service`

### Kafka
Kafka is a distributed streaming platform, mainly used as a high-performance messaging system. Kafka was installed using [this guide](https://www.digitalocean.com/community/tutorials/how-to-install-apache-kafka-on-ubuntu-20-04). It uses default ports: `9092` for Kafka and `2181` for Zookeeper.

* Logs (data) directory: `/mnt/data/kafka/logs`
* Installation directory: `/home/kafka/kafka/`
* Start command: `sudo systemctl start kafka`
* Status command: `sudo systemctl status kafka`
* Stop command: `sudo systemctl stop kafka`

Logging in as `kafka` user to use command-line utilities: `sudo su - kafka`.
Try running command `~/kafka/bin/kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic TutorialTopic --from-beginning`

### Supervisor
[Supervisor](http://supervisord.org/) is a client/server system that allows its users to monitor and control a number of processes. It use used
to run the services in production mode and restarts the service if it crashes. It provides various features and can be used through the linux terminal.

Each process requires its own config file in `/etc/supervisor/conf.d/` folder (examples of existing services are already available in the folder).
The config files documentation is available [here](http://supervisord.org/configuration.html).

Once the config file is setup, one can start the process with the following terminal commands (lets say the servies name is `service`):

* Reread processes: `sudo supervisorctl reread` - reads which processes have its own config files
* Update processes: `sudo supervisorctl update` - updates the supervisor to take into account new and changed config files
* Start process: `sudo supervisorctl start service`
* End process: `sudo supervisorctl stop service`
* Log process: `sudo supervisorctl tail -{number} service` where `{number}` is the number of bytes one would like to output, e.g. 5000. Example: `sudo supervisorctl tail -5000 service`
* Start all processes: `sudo supervisorctl start all`
* End all processes: `sudo supervisorctl stop all`


## Custom services running on Atena

Here are listed all the services running on Atena (including URL/port).

| Service Name | Description | Virtual host | Port | Caretaker |
| ------------ |:----------- | ------------ | ----:| --------- |
| iot-rapids   | IoT platform for multiple EU projects (NAIADES, Water4Cities) | atena.?.? | 80 | Klemen |
| GPS tracking | Tracking of GPS devices | atena.?.? | 8888 | Klemen |
| Zookeeper | Kafka Zookeeper | localhost | 2181 | Klemen |
| Kafka | Kafka | localhost | 9092 | Klemen |
| eLENS miner system | Connecting eLENS services | atena.?.? | 4300 | Erik |
| eLENS text embeddings | Creates Text Embeddings Interface | atena.?.? | 4000 | Erik |
| eLENS text embeddings | Creates English Text Embeddings | atena.?.? | 4001 | Erik |
| eLENS text embeddings | Creates Slovene Text Embeddings | atena.?.? | 4002 | Erik |
| eLENS text embeddings | Creates German Text Embeddings | atena.?.? | 4003 | Erik |
| eLENS text embeddings | Creates Greek Text Embeddings | atena.?.? | 4004 | Erik |
| eLENS document search | Searches through legal documents | atena.?.? | 4100 | Erik |
| eLENS document similarity | Calculates document similarity | atena.?.? | 4200 | Erik |
| NAIADES FIWARE adapter | End-point for FIWARE for NAIADES | atena.?.? | 5003 | Gal |
| NAIADES WatchDog API | End-point for NAIADES WatchDog | atena.?.? | 5004 | Mark |
| NAIADES WatchDog GUI | GUI for NAIADES WatchDog | atena.?.? | 5005 | Mark |


