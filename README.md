# Apache Superset Docker Image (Version 2.1.0)

This repository provides instructions to build a Docker image for Apache Superset version 2.1.0, an open-source business intelligence web application. With this Docker image, you can easily deploy and run Superset in a containerized environment.

## Prerequisites

- Docker installed on your system.

## Getting Started

### Step 1: Build the Docker Image

Run the following command to build the Docker image for Apache Superset version 2.1.0:

```bash
$ docker build -t superset:2.1.0 https://github.com/apache/superset.git@2.1.0
```

### Step 2: Run Apache Superset Container

To start a Superset instance on port 8080, use the following command:

```bash
$ docker run -d -p 8080:8088 -e "SUPERSET_SECRET_KEY=<your_secret_key_here>" --name superset superset:2.1.0
```

Note: Replace `<your_secret_key_here>` with a randomly generated secret key to ensure the security of your Superset instance. You can use Python to generate a random key:

```bash
$ python -c 'import os; print(os.urandom(16).hex())'
```

### Step 3: Initialize Superset

Once the container is running, you need to initialize the Superset instance by following these steps:

#### Step 3.1: Create a Local Admin Account

Run the following command to set up a local admin account:

```bash
$ docker exec -it superset superset fab create-admin \
    --username admin \
    --firstname Superset \
    --lastname Admin \
    --email admin@superset.com \
    --password admin
```

Replace `admin` with your desired username and `admin@superset.com` with your email address. Choose a strong password for better security.

#### Step 3.2: Migrate the Local Database

Next, migrate the local database to the latest version:

```bash
$ docker exec -it superset superset db upgrade
```

#### Step 3.3: Load Example Data

Load example data to have some sample visualizations and dashboards:

```bash
$ docker exec -it superset superset load_examples
```

#### Step 3.4: Setup Roles

Set up the roles required for Superset:

```bash
$ docker exec -it superset superset init
```

### Accessing Superset

After completing the initialization steps, you can access the Superset web interface by navigating to http://localhost:8080/login/. Use the admin credentials (username: admin, password: admin) or the credentials you set during the admin account creation to log in.

## Welcome Image

![image](https://github.com/ikhsannur1996/docker-superset-2.1.0/assets/32507742/041e1d1b-597a-4aa3-b09a-778511b91dd7)


## Sample Dashboard

Here is a sample dashboard showcasing various data visualizations created using Apache Superset.

![world-banks-data-2023-08-04T01-59-06 597Z](https://github.com/ikhsannur1996/docker-superset-2.1.0/assets/32507742/831849d6-b4ac-4895-a757-b94651b29bb4)

## My Dashboard

Create your own interactive dashboards using Apache Superset! Use the intuitive interface to explore and visualize your data.

![global-superstore-2023-08-06T12-18-59 801Z](https://github.com/ikhsannur1996/docker-superset-2.1.0/assets/32507742/a95e3eb7-1392-4385-84bf-f8d521347595)


## Optional Auto-Restart

To enable auto-restart for the Superset container in case it crashes or is stopped, use the `--restart` flag with the `unless-stopped` option in the `docker run` command. This ensures that the container will automatically restart unless it is explicitly stopped.

```bash
$ docker run -d -p 8080:8088 -e "SUPERSET_SECRET_KEY=<your_secret_key_here>" --name superset --restart unless-stopped superset:2.1.0
```


## References

For more information and documentation on Apache Superset, visit the official website: https://superset.apache.org

Happy data exploration with Apache Superset in your Docker container! 🚀 
