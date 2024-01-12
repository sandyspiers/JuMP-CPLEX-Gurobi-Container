# JuMIP: Docker Container for JuMP, CPLEX and Gurobi

Creates a docker container with `Julia`, [`JuMP`](https://github.com/jump-dev/JuMP.jl), `CPLEX` & `Gurobi` installed, all with correct environment variables so [`CPLEX.jl`](https://github.com/jump-dev/CPLEX.jl) and [`Gurobi.jl`](https://github.com/jump-dev/Gurobi.jl) install without fuss.

## Preparation

### CPLEX

Obtain a licence and download the linux installer.
The file should be something like `cplex_studioXXXX.linux_x68_64.bin`.
Place this file in `bin/`.
`bin` should then contain the following 2 files,

```txt
bin
 - cplex_studioXXX.linux_x68_64.bin
 - cplex_installer.properties
```

### Gurobi

Obtain [web service licence](https://www.gurobi.com/features/web-license-service/) (client-only licences don't work for containers).
Generate a `gurobi.lic` licence file and place it in `C:/gurobi/` (as recommended (for Windows) [here](https://support.gurobi.com/hc/en-us/articles/360013417211)).

### JuMIP Dockerimage

The Dockerfile starts by creating a 'mipopt' image with both Cplex and Gurobi installed into the `/opt/` directory.
We then copy this over to a fresh [julia image](https://hub.docker.com/_/julia).
The correct environment variables are then set so that `CPLEX.jl` and `Gurobi.jl` install correctly (when you eventually want them).

## Usage

We can start a REPL session container by using the `docker-compose.yml`.
Note that a volume must be added to transfer across the `Gurobi.lic`.
To keep have code between your local environment, and the REPL container, we add a volume in the docker compose file.
Then, to start your REPL in a container, run

```shell
docker compose run jumip
```
