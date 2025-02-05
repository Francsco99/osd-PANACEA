# osd-PANACEA

**osd-PANACEA** integrates the [PANACEA](https://github.com/Marini97/PANACEA) project into an [OpenSearch Dashboards plugin](https://github.com/Francsco99/adt_viewer). This repository contains the Docker compose file to set up containers running:
1. The developer environment for Opensearch Dashboards.
2. A Flask application exposing APIs to interact with PANACEA.
3. A Flask application exposing APIs for database operations to store and manage data for the plugin.
4. The PostgreSQL database

## Table of Contents

1. [Setup for Linux and MacOS](#setup-for-linux)
   - [Clone the Repository](#clone-the-repository)
   - [Set the Environment Variable](#set-the-environment-variable)
   - [Start the Containers](#start-the-containers)
   - [Install the `adt-viewer` Plugin](#install-the-adt-viewer-plugin)
   - [Start OpenSearch Dashboards](#start-opensearch-dashboards)
   - [Other Resources](#other-resources)
2. [Setup for Windows](#setup-for-windows)
   - [Modify the `docker-compose.yml` file](#modify-the-docker-composeyml-file)
   - [Modify the `entrypoint.sh` file](#modify-the-entrypointsh-file)
   - [Installation Process](#installation-process)

---

## Setup for Linux

### Clone the Repository

First, clone this repository and navigate to its directory:

```bash
git clone https://github.com/Francsco99/osd-PANACEA.git
```

### Set the Environment Variable

Set the environment variable for the fork repository URL by running the following command:
```bash
export REPO_URL=[insert your fork repo URL here]
```
If a forked repository has not been created:
	1. Go to the Opensearch Dashboards Github page
	2. Create a new fork
	3. Copy the HTTPS link of the forked repository URL and use it in the above command

**_NOTE_** This command needs to be re-run every time you restart the Docker compose file in a new terminal.

### Start the Containers

Run the following command:
```bash
docker compose up -d --build
```

### Installing the adt-viewer plugin

- Under the `Docker` right-click `abbyhu/opensearch-dashboards-dev:latest`, and select Attach Visual Studio Code.
	- This will ssh into the container and you will be able to view and edit the files using VS Code as the code editor.

    **_NOTE_** If you do not wish to use VS Code as the code editor, the alternative way of ssh into the container is by using the command:
```
docker exec -it dev-env /bin/bash
```

- Clone the adtViewer repository into the `plugins` folder: 
```
cd plugins
git clone https://github.com/Francsco99/adt_viewer
```

### Starting OpenSearch Dashboards (instructions from Opensearch Dashboards)

- In the terminal, start the OpenSearch Dashboards application by typing:
```
yarn start:docker
```

- Now that OpenSearch Dashboards is running, you should be able to see a log line similar to: 
`[info][server][OpenSearchDashboards][http] http server running at http://0.0.0.0:5603/dog`.

	- The last three letters dog are randomly generated every time we start dashboards.

- Wait for the optimizer to run, which takes about 100s - 200s. Once the optimizer is finished running, it will show a line such as `[success][@osd/optimizer] 48 bundles compiled successfully after 204.9 sec, watching for changes`.

- Then paste the link into a browser and view dashboard running in browser, but change ‘0.0.0.0’ to ‘localhost’. So here the link should be `http://localhost:5603/dog`.

### Other Resources

For any doubt you can check the [OpenSearch Dashboards Docker Development Setup Manual](https://github.com/opensearch-project/OpenSearch-Dashboards/blob/main/docs/docker-dev/docker-dev-setup-manual.md).

## Setup for Windows

### Modify the docker-compose.yml file

- Open `docker-compose.yml`
- Replace the variable `${REPO_URL}` with the forked reposiotory URL

### Modify the entrypoint.sh file

- Open `entrypoint.sh`
- Change the **End of line** format to make it Windows-compatible

### Installation Process

Once the above modifications are done, follow the same installation steps at the Linux setup
