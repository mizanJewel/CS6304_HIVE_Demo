# CS6304 Hive Demo

This repository contains a hands-on Apache Hive exercise using the `Twitter.txt` dataset. The instructions below use **Docker Desktop on macOS**, so you do not need to install Hadoop or Hive directly on your Mac. If you have docker installed in windows or linux, the instruction is similar.

## Contents

- `Commands.txt` — Hive SQL commands for databases, tables, queries, partitioning, and bucketing.
- `Twitter.txt` — tab-delimited Twitter dataset used by the exercises.
- `Hive_Config.txt` — legacy instructions for installing Hive in a virtual machine. Use this README instead if you are running Hive with Docker on macOS.


The commands below use the Apache Hive Docker image `apache/hive:4.0.0`.

## 1. Install Docker Desktop

If Homebrew is installed, install Docker Desktop:

```bash
brew install --cask docker
```

If Homebrew reports that Docker is already installed but the application is missing, reinstall it:

```bash
brew reinstall --cask docker
```

Launch Docker Desktop:

```bash
open -a Docker
```

Complete the first-launch setup and wait until Docker Desktop reports that the engine is running.

Verify the installation:

```bash
docker --version
docker compose version
docker run hello-world
```

The `hello-world` command should print `Hello from Docker!`.

> **Apple Silicon:** Docker automatically selects a compatible image architecture when one is available. The `apache/hive:4.0.0` image is used in the commands below.

## 2. Get this repository

Clone the repository:

```bash
git clone https://github.com/mizanJewel/CS6304_HIVE_Demo.git
cd CS6304_HIVE_Demo
```

If you already cloned it, update your local copy:

```bash
git pull
```

Confirm that the dataset is present:

```bash
ls
```

You should see `Commands.txt` and `Twitter.txt`. After here follow the `Commands.txt` instructions.



## Useful Docker commands

```bash
# List locally available images
docker images

# List running containers
docker ps

# List all containers, including stopped ones
docker ps -a

# Follow Hive container logs
docker logs -f myhive

# Open a shell inside the Hive container
docker exec -it myhive /bin/bash

# Stop the Hive container
docker stop myhive

# Start the existing Hive container
docker start myhive
```

To remove the container (this deletes its writable container filesystem, including data not stored elsewhere):

```bash
docker rm -f myhive
```

Only remove it if you intentionally want to recreate the environment. The downloaded image can remain locally and be reused.

## Troubleshooting

### `docker: command not found`

Make sure Docker Desktop is installed and launch it with:

```bash
open -a Docker
```

Then open a new terminal and check:

```bash
docker --version
```

### Container name is already in use

A container named `myhive` already exists. Start it instead of creating another:

```bash
docker start myhive
```

### Beeline cannot connect

Check that the container is running:

```bash
docker ps
```

Check HiveServer2 logs:

```bash
docker logs myhive
```

Give Hive a little more time to initialize, then retry the Beeline command.

### `Twitter.txt` cannot be found

Run `docker cp` from the local repository directory and confirm the file exists:

```bash
ls -lh Twitter.txt
docker cp Twitter.txt myhive:/tmp/Twitter.txt
```

## References

- [Apache Hive Docker image](https://hub.docker.com/r/apache/hive)
- [Docker Desktop for Mac](https://docs.docker.com/desktop/setup/install/mac-install/)
- [Docker documentation](https://docs.docker.com/)
