
# NeuralSyncTester Suite

The NeuralSyncTester Suite is a tool that can be used to simulate the synchronization process between two Multilayer Tree Parity Machine (MTPM) neural networks, considering the option to choose the use of binary or non-binary stimuli. Its main goal is to help understand the synchronization process between two MTPM networks for research and educational purposes, through user-defined simulations.

# Quick Installation
Start by cloning this repository and its submodules:
```
git clone --recurse-submodules git@github.com:lavidaesrecorta/NeuralSyncTester.git
```

This repository contains two submodules, one for **NeuralSyncTester Simulation Engine** and another for **NeuralSyncTester Visualizer**. 

## Simulation Engine (Docker)

If you just want to get up and running, you can host all necessary services for the simulation engine in one machine using the `docker-compose.yml` file present in the `Sample Configuration` directory.

> [!WARNING]  
> ⚠️ Important: Running the example `docker-compose.yml` file will generate a `mysql` directory. You may adjust the directory path within the file if necessary.  

There is no need to clone the repository and its submodules, just make sure you have the following files like the examples in the `Sample Configuration` directory: 
 - `docker-compose.yml`: Used to setup all services.
 - `simulation_engine.env`: Used to define the environment for NeuralSyncTester Simulation **Engine**.
 - `visualizer.env`: Used to define the environment for NeuralSyncTester Simulation **Visualizer**.
 - `init.sql`: This file will define the schema used in the MySQL database.

Inside the folder containing `docker-compose.yml`, you can add configuration files in the `configFiles` directory. Additionally, ensure you update the `ENABLE_AUTOMATIC_SIM` variable in the `simulation_engine.env` file to `true`.

In the `Sample Configuration` directory, you will find a `configFiles` folder with example configurations for various MultiLayer Tree Parity Machine architectures, each with a network size of 1024 bits. 

To use the `docker-compose.yml`, use the following command:
```
docker compose --env-file ./simulation_engine.env up
```
_Using the `simulation_engine.env` file on the first run ensures that the MySQL database is using the correct username, password and table name for both setup and simulation execution._


## Visualizer

Clone the Visualizer repository, copy the `visualizer.env` file as `.env` inside the root folder of the repository and run the following commands:

```
# Install packages
yarn
# Run the code as a developer
yarn dev
```

> [!WARNING]  
> ⚠️ Important: For full functionality, the visualizer server and the web browser must run on the same machine. Running the visualizer on a separate (dedicated) server is untested and may cause real-time features to malfunction.

# Configuration files
This section describes the configuration files present in the `Sample Configuration` folder.
## Simulation Engine
The following environment variables are used to configure the simulation engine:
| Variable Name            | Description                                                                 | Example / Default        |
|--------------------------|-----------------------------------------------------------------------------|---------------------------|
| `HOSTNAME`               | Hostname identifier used for logging in the database                     | `"HOSTNAME_ERROR"`        |
| `MAX_GOROUTINES`         | Maximum number of concurrent goroutines allowed                             | `4`                       |
| `DB_HOST`                | Hostname or IP address of the database server                               | `"database"`              |
| `DB_PORT`                | Port on which the database server is listening                              | `3306`                    |
| `DB_USER`                | Username for authenticating with the database                               | `your_username`           |
| `DB_PASSWORD`            | Password for the specified database user                                    | `your_password`           |
| `DB_NAME`                | Name of the database to connect to                                          | `sessions`                |
| `ENABLE_AUTOMATIC_SIM`  | Enables automatic simulation at startup; set to `true` or `false`           | `false`                   |
| `CONFIG_DIRECTORY`       | Path to directory containing simulation configuration files                 | `"./configFiles"`         |

If `ENABLE_AUTOMATIC_SIM` is set to `true`, the Simulation Engine is going to look for configuration files inside of the `CONFIG_DIRECTORY` directory (which should be mounted as volume if using docker). 

The application supports two configuration file formats for MTPM networks: one for architectures **without overlap**, and another for architectures both **with partial or complete overlap**. Make sure to use the correct format depending on the type of MTPM you are simulating, as the structure of the configuration files differs between these two cases. Full examples for all scenarios are available in the `Sample Configuration` directory.

#### For **complete or partial overlap**:

| Field Name        | Type       | Description                                                                 |
|-------------------|------------|-----------------------------------------------------------------------------|
| `tpm_type`        | `string`   | Scenario identifier for this configuration file                             |
| `max_session_count` | `int`    | Number of repetitions for each configuration                                |
| `max_iterations`  | `int`      | Maximum number of iterations per session                                    |
| `k_configs`       | `[][]int`  | Configurations for the number of neurons per layer                          |
| `n0_configs`      | `[]int`    | Number of inputs for each neuron in the first layer                         |
| `m_configs`       | `[]int`    | Range of input stimuli for each neuron in the first layer                   |
| `l_configs`       | `[]int`    | Range of synaptic weights                                                   |
| `learn_rules`     | `[]string` | Learning rules to be used in each simulation (simulated sequentially)       |

#### For **no overlap**:

| Field Name        | Type       | Description                                                                 |
|-------------------|------------|-----------------------------------------------------------------------------|
| `tpm_type`        | `string`   | Scenario identifier for this configuration file                             |
| `max_session_count` | `int`    | Number of repetitions for each configuration                                |
| `max_iterations`  | `int`      | Maximum number of iterations per session                                    |
| `klast_configs`   | `[]int`    | Number of neurons in the last layer                                         |
| `n_configs`       | `[][]int`  | Input configurations for each layer                                         |
| `m_configs`       | `[]int`    | Range of input stimuli for each neuron in the first layer                   |
| `l_configs`       | `[]int`    | Range of synaptic weights                                                   |
| `learn_rules`     | `[]string` | Learning rules to be used in each simulation  

## Visualizer
The visualizer uses the following environment variables:

These variables configure the connection between the web app and the **Simulation Engine**:

| Variable Name     | Description                                             | Example / Default      |
|-------------------|---------------------------------------------------------|-------------------------|
| `BACKEND_URL`     | Hostname or container name of the Simulation Engine     | `simulation_engine`     |
| `BACKEND_PORT`    | Port on which the Simulation Engine is listening        | `8080`                  |
