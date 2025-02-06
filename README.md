
# NeuralSyncTester Suite

The NeuralSyncTester Suite is a tool that can be used to simulate the synchronization process between two Multilayer Tree Parity Machine (MTPM) neural networks, considering the option to choose the use of binary or non-binary stimuli. Its main goal is to help understand the synchronization process between two MTPM networks for research and educational purposes, through user-defined simulations.

# Installation

This repository contains two submodules, one for the Simulation Engine and another for the Visualizer.

To deploy the Simulation Engine you also need a MySQL database, the Simulation Engine repository includes both a Dockerfile inside the `/src` directory and a docker-compose file that also enables a database. Remember to change the configuration file in the root directory and create a `.env` file with the following variables:
```
DB_HOST=<Database host>
DB_PORT=<Database port>
DB_USER=<Database Username>
DB_PASSWORD=<Database Password>
DB_NAME=<Name for the table with simulation results>

MAX_SIMULATION_REPETITIONS=10
MAX_ITERATION_COUNT=7_000_000
MAX_GOROUTINES=3

#All changes below this line are optional
HOSTNAME=<Server hostname> #This is just for fallback
DEFAULT_N_0=5
DEFAULT_M=1
DEFAULT_RULE=HEBBIAN
DEFAULT_TYPE=NO_OVERLAP
```

To deploy the Visualizer, simpmly run `yarn` inside the Visualizer repository to install all dependencies and then run `yarn dev` to start the server in development mode.

You need the following variables in a `.env` file at the root of the repository:
```
BACKEND_URL=<Simulation Engine URL>
BACKEND_PORT=<Simulation Engine port>
```
