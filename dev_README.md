# TumourVisualizer

![alt text](https://github.com/Spenca/UnityTumourSimulator/blob/development/Screenshot1.png)
![alt text](https://github.com/Spenca/UnityTumourSimulator/blob/development/Screenshot2.png)

## About
TumourVisualizer uses Unity to visualize data generated by a modified version of [TumourSimulator version 1.2.3](https://www2.ph.ed.ac.uk/~bwaclaw/cancer-code/), included in this repository. This development branch is a slight modification of the master code, created to display an interesting visualization discovered by experimentation. The green cells in the visualization all share a specific driver mutation (id 277), whereas the red cells do not.

## Using the visualizer
To make changes to the project, or build for any platforms, clone this repository and open the root directory in your Unity editor.

## Controls
While moving the mouse, click and hold the left mouse button to pan the camera, or click and hold and the right mouse button to strafe the camera. Hold the spacebar and move the mouse forwards and backwards to zoom.

## Input
The visualizer accepts the file `out.csv` as input; at the root project directory while running the Unity editor, and in the same directory as the executeable when running a Unity build. This file has been doctored by pandas, and is not outputted natively by `TumourSimulator_1.2.3`. 


Other files are generated by TumourSimulator, which can be modified by compiling and running the code found in the `TumourSimulator_1.2.3` directory. Use `g++ simulation.cpp main.cpp functions.cpp -w -O3 -I include/ -o cancer.exe` to compile the code on Linux and Mac. On Windows, please run with the "Windows Subsytem for Linux" and accompanying Linux install (tested with Ubuntu). Current installation directions for these tools can be found [here](https://docs.microsoft.com/en-us/windows/wsl/install-win10).


After compiling the code found in the `TumourSimulator_1.2.3` directory, more information about the specifiable parameters with which the simulation can be run is viewable by running `./cancer.exe -h` in a terminal. More information about these parameters is also available in [this](https://www.nature.com/articles/nature14971) paper, which describes the model of tumour growth that TumourSimulator attempts to simulate.

## Categorical information
The modified TumourSimulator included in this repository outputs 3 files containing tables of data, called `cell_table_10000.pcd`, `genotype_table_10000.pcd`, and `mutation_table_10000.pcd`. Each row in the cell and genotype tables represents a single cell in the simulation, and each group of adjacent rows in the mutation table with the same `genotype_id` also represents a single cell.

### Fields in `cell_table_10000.pcd`:
`cell_id`: integer identifier; each cell has a unique one

`x`: integer x-coordinate for the cell's position in a visual representation

`y`: integer y-coordinate for the cell's position in a visual representation

`z`: integer z-coordinate for the cell's position in a visual representation

`genotype_id`: integer identifier that categorizes cells; the colour of a cell in the visualization is determined by its genotype information

### Fields in `genotype_table_10000.pcd`:
`genotype_id`: same as in `cell_table_10000.pcd`

`mother_genotype_id`: the `genotype_id` belonging to the cell's direct ancestor; if a cell has a `mother_genotype_id` of `-1`, that means it has no ancestors

### Fields in `mutation_table_10000.pcd`:
`genotype_id`: same as in `cell_table_10000.pcd` and `genotype_table_10000.pcd`

`mutation_id`: integer identifier; each one represents a mutation belonging to a cell

`is_driver`: boolean value; states if the mutation in question is a driver mutation or not

`is_resistant`: boolean value; states if the mutation in question is a resistant mutation or not

More information about driver and resistant mutations can be found [here](https://www.nature.com/articles/nature14971).

## Future work
I'm interested in potentially modifying the visualizer to update in real time and/or have the ability to step through different states, by providing multiple outputs from TumourSimulator.