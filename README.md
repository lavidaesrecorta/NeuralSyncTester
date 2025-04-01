
# NeuralSyncTester Suite

The NeuralSyncTester Suite is a tool that can be used to simulate the synchronization process between two Multilayer Tree Parity Machine (MTPM) neural networks, considering the option to choose the use of binary or non-binary stimuli. Its main goal is to help understand the synchronization process between two MTPM networks for research and educational purposes, through user-defined simulations.

# Quick Installation

This repository contains two submodules, one for **NeuralSyncTester Simulation Engine** and another for **NeuralSyncTester Visualizer**.

## Simulation Engine (Docker)

If you just want to get up and running, you can host all necessary services for the simulation engine in one machine using the `docker-compose.yml` file present in the `Sample Configuration` directory.

> [!WARNING]  
> Running the example `docker-compose.yml` file will generate a `mysql` directory. You may adjust the directory path within the file if necessary.  

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
