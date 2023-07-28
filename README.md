# EurOPDX-Galaxy
This repository contains recipe for docker version of [Galaxy platform](www.galaxyproject.org), expanded with tools and workflows for PDX(Patient Derived Xenograft) model molecular data analysis.

To use this docker image, you need to have [Docker](https://docs.docker.com/get-docker/) and [Docker Compose](https://docs.docker.com/compose/install/) installed.

# Quick start

This is a tutorial for UNIX-like environment (Lunix, MacOS)

### Setup a work-dir
```bash
mkdir ~/docker-galaxy
cd ~/docker-galaxy
mkdir reference-data
```

### Download the docker-compose.yml

In the `~/docker-galaxy` directory 

```bash
wget https://raw.githubusercontent.com/BorisYourich/EurOPDX-Galaxy/main/docker-compose.yml
```

### Configure

Set the `import` volume as the path to the directory where you store the data you want to process, to avoid copying the files into the container.

Set the `reference-data` volume to match the new, empty directory that you created in the first step. This directory is where the container will store all the reference data for mapping software. (To avoid re-creating the data ech time the container is run)

```yaml
version: '3.5'

services:
  galaxy:
    container_name: galaxy
    restart: always
    image: registry.gitlab.ics.muni.cz:443/europdx/pdx-pipelines/galaxy-docker
    ports:
      - 8080:8080

    volumes:
      - /your/import/dir:/import
      - ~/docker-galaxy/reference-data:/galaxy/reference-data/
```

### Run the container

In the `~/docker-galaxy` directory 

```bash
docker-compose up
```

After execution, a log from the container will show up in the terminal. If you run this for the first time, it will take a few minutes (depending on you internet connection) to pull the image.

When the download is finnished, the container will start and you can see the EurOPDX Galaxy instance on `localhost:8080` on your machine.

Log into the admin profile with name `admin` and password `password`
