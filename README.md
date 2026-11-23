# Maze Generator and Solver

A maze generator and solver, animated step by step.

The program builds a maze with the generation algorithm of your choice, then solves it with a search algorithm, drawing every step in a window. It is meant for anyone who wants to compare how these algorithms behave.

## Table of contents

- [Maze Generator and Solver](#maze-generator-and-solver)
	- [Table of contents](#table-of-contents)
	- [How it works](#how-it-works)
	- [Tech stack](#tech-stack)
	- [Repository structure](#repository-structure)
	- [Prerequisites](#prerequisites)
	- [Installation](#installation)
	- [Running locally](#running-locally)
		- [Command-line options](#command-line-options)
	- [Useful scripts](#useful-scripts)
	- [License](#license)

## How it works

1. **Setup**: the window size is 1600x900 pixels, or the desktop size in fullscreen mode. The grid has one cell per `--cell-size` pixels, all starting as walls.
2. **Generation**: the selected algorithm carves the maze. Each frame runs `--speed` update steps. Available algorithms: `prim`, `kruskal`, `hunt-and-kill`, `depth-first` and `aldous-broder`.
3. **Solving**: once the maze is complete, the solver runs with the same step rate. The only available solver is `breadth-first`; `none` skips this step.
4. **Restart**: a left click starts a new generation. `Escape` or closing the window quits.

## Tech stack

| Layer | Technologies |
| --- | --- |
| Language | C++17 |
| Graphics | SFML |
| Command line | cxxopts |
| Build | xmake |

## Repository structure

```
.
├── assets/             Window icon
├── src/
│   ├── display/        Grid rendering and simulation loop
│   ├── generation/     Maze generation algorithms
│   ├── solve/          Maze solving algorithms
│   ├── vector/         2D vector type
│   ├── config.cpp      Window size, title and colors
│   └── main.cpp        Argument parsing and window loop
└── xmake.lua           Build configuration
```

Each algorithm has its own `.cpp` and `.hpp` pair, built on the `Generation` and `Solve` base classes. Adding an algorithm means adding a pair of files and registering the name in `src/main.cpp`.

## Prerequisites

- [Git](https://git-scm.com/downloads)
- [xmake](https://xmake.io/#/getting_started?id=installation), which downloads SFML and cxxopts on the first build
- A C++17 compiler

## Installation

```bash
git clone git@github.com:maxencebonamy/Maze-Generator-Solver.git
cd Maze-Generator-Solver
xmake
```

## Running locally

```bash
xmake run main --generation kruskal
```

The program loads `assets/icon.png` from the working directory, so run it from the repository root.

Example with a fullscreen window, the `hunt-and-kill` generator, no solving, a speed of 10, 120 frames per second and 10 pixel cells:

```bash
xmake run main -g hunt-and-kill -s none --speed 10 -f 120 --fullscreen -c 10
```

### Command-line options

| Option | Description | Default |
| --- | --- | --- |
| `-g`, `--generation` | Generation algorithm: `prim`, `kruskal`, `hunt-and-kill`, `depth-first` or `aldous-broder` | `kruskal` |
| `-s`, `--solve` | Solve algorithm: `breadth-first` or `none` | `breadth-first` |
| `--speed` | Algorithm steps per frame | `1` |
| `-c`, `--cell-size` | Cell size, in pixels | `25` |
| `-f`, `--fps` | Frames per second, `0` for no limit | `60` |
| `--fullscreen` | Run in fullscreen | disabled |

## Useful scripts

| Command | Effect |
| --- | --- |
| `xmake` | Build the project |
| `xmake run main` | Run the program with default options |
| `xmake f -m release` | Switch the build to release mode |
| `xmake f -m debug` | Switch the build to debug mode |
| `xmake clean` | Remove build outputs |

## License

This project is licensed under the [MIT License](LICENSE).
