# osd-PANACEA

**osd-PANACEA** integrates the [PANACEA](https://github.com/Marini97/PANACEA) project into an [OpenSearch Dashboards plugin](https://github.com/Francsco99/adt_viewer). This repository contains the necessary files to set up containers running:

1. A Flask application exposing APIs to interact with PANACEA.
2. A Flask application exposing APIs for database operations to store and manage data for the plugin.

## Setup Instructions

### 1. Clone the Repository

First, clone this repository and navigate to its directory:

```bash
git clone https://github.com/Francsco99/osd-PANACEA.git
```

### 2. Start the Containers

Run the following command
```bash
docker compose up -d --build
```

### 4. Installing the adt-viewer plugin

- Under the `Docker` tab in VS Code, verify that there are five containers running: opensearchproject/opensearch:latest and abbyhu/opensearch-dashboards-dev:latest.
- Right-click `abbyhu/opensearch-dashboards-dev:latest`, and select Attach Visual Studio Code.
	- This will ssh into the container and you will be able to view and edit the files using VS Code as the code editor.
    - If you do not wish to use VS Code as the code editor, the alternative way of ssh into the container is by using the command:
```
docker exec -it dev-env /bin/bash
```
- Clone the adtViewer repository into the `plugins` folder: 
```
cd plugins
git clone https://github.com/Francsco99/adt_viewer
```

### 5. Starting OpenSearch Dashboards

- In the terminal, start the OpenSearch Dashboards application by typing:
```
yarn start:docker
```

- Now that OpenSearch Dashboards is running, you should be able to see a log line similar to: 
`[info][server][OpenSearchDashboards][http] http server running at http://0.0.0.0:5603/dog`.

	- The last three letters dog are randomly generated every time we start dashboards.

- Wait for the optimizer to run, which takes about 100s - 200s. Once the optimizer is finished running, it will show a line such as `[success][@osd/optimizer] 48 bundles compiled successfully after 204.9 sec, watching for changes`.

- Then paste the link into a chrome browser and view dashboard running in browser, but change ‘0.0.0.0’ to ‘localhost’. So here the link should be `http://localhost:5603/dog`.

### 6. Other

For any doubt you can check the [OpenSearch Dashboards Docker Development Setup Manual](https://github.com/opensearch-project/OpenSearch-Dashboards/blob/main/docs/docker-dev/docker-dev-setup-manual.md) to start the containers required for the project.

## Repository Structure

- `database-server/`: Contains the Flask app for the database APIs
- `panacea-server/`: Contains a minimal version of PANACEA, its dependencies and the Flask app for the PANACEA APIs
- `docker-compose.yml`: Docker configuration for the project.
- `entrypoint.sh`: Entry point script for initializing Opensearch Dashboard dev-env.

## Contributing

Contributions are welcome! To contribute:

1. Fork the repository.
2. Create a new branch (`git checkout -b feature/your-feature`).
3. Make your changes and commit them (`git commit -m 'Add new feature'`).
4. Push to your branch (`git push origin feature/your-feature`).
5. Open a Pull Request.
