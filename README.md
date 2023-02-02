# Minesweeper Solver 💣

This is a minesweeper solver written in [Otter](https://www.mcs.anl.gov/research/projects/AR/otter/). Otter is an automated deduction system I learned about in class. This solver is the product of a class project.

This project consists of two solvers, that solve two different minesweeper games.

## Run it

If you don't care about the details, you can just run the solver executing the ```run_solver.sh``` script. You have to pass either 1 or 2 as an argument to the script, depending on which solver you want to run. But first, you'll have to adapt the ```run_solver.sh``` script to your system. Either change the absolute path to the location on your system where you have otter installed, or if you have otter installed in your PATH, just replace the complete path ```.../.../foo/bar/otter``` with ```otter```. When everything is set up, you can run it like this:

```bash
./run_solver.sh 1 # Runs solver 1
```

## Solver 1

Solver one (```minesweeper_solver_1.in```) works with the classic minesweeper game. The initial game setup is given inside of ```formula_list(sos).```. There, you have to specify the number of rows and columns and the (X,Y,Z) values of the sensors. The sensors have the structure ```sensor(x,y,z)```, where ```x``` and ```y``` denote the coordinates of the sensor in the gameboard and ```z``` the number of bombs that sensor detects. For instance, if the gameboard were to look like this:

| | 1 | 2 | 3 |
| --- | --- | --- | --- |
| 1 | 💣 | 👀 | |
| 2 | 👀 | 💣 | 👀 |
| 3 | 💣 | | 💣 |

Then the setup would be:

```prolog
formula_list(sos).
    columns(3).
    rows(3).
    sensor(1,2,2).
    sensor(2,1,3).
    sensor(2,2,2).
end_of_list.
```

Just hit

```bash
./run_solver.sh 1
```

and watch it solve the game!

## Solver 2

Solver 2 (```minesweeper_solver_2.in```) works with a different version of the minesweeper game. Now, there is two different types of sensors: vertical and horizontal ones. A vertical sensor (```sensorV```) tells you the number of bombs there is in the sensor's column (his spot not counted, so if you have a 3x3 board, the maximal number of possible bombs in a column whith a sensor would be 2, as one cell is already occupied by the sensor). The same goas for the horizontal sensors analogously.

For instance, if the gameboard were to look like this:

| | 1 | 2 | 3 |
| --- | --- | --- | --- |
| 1 | 💣 | ↕️ | |
| 2 | ↕️ | 💣 | ↔️ |
| 3 | 💣 | | |

Then the setup would be:

```prolog
formula_list(sos).
    columns(3).
    rows(3).
    sensorV(1,2,1).
    sensorV(2,1,2).
    sensorH(2,3,1).
end_of_list.
```

Just hit

```bash
./run_solver.sh 2
```

and watch it solve the game!
