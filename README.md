# Reflect Array CST Simulator

This MATLAB script automates the creation and configuration of a reflectarray antenna model in CST Studio Suite. It's designed to streamline the process of setting up complex reflectarray simulations by programmatically defining geometry, materials, and simulation parameters.

## Features

- Automatic creation of a new CST Studio Suite project
- Configuration of solver settings and frequency range
- Definition of units, background, and boundary conditions
- Setup of farfield monitors
- Material definitions for copper, Rogers RT5880, and foam
- Parametric model creation including ground plane, isolation layer, substrate, and reflectarray elements
- Automated generation of circular reflectarray elements based on external data

## Prerequisites

- MATLAB
- CST Studio Suite (with COM automation support)
- Microsoft Excel (for reading element dimensions)

## Usage

1. Ensure CST Studio Suite is installed and properly configured for COM automation.
2. Prepare an Excel file named `dim_value.xlsx` containing the dimensions and positions of the reflectarray elements.
3. Run the script in MATLAB.

## Simulation Workflow

The complete simulation process involves several steps using different CST Studio Suite modules. Here's the recommended workflow:

### Step 1: Unit Cell Simulation (CST Microwave Studio)

Before simulating the entire reflectarray, start with the simulation of one unit cell using Floquet's Port technique:

1. Select "CST Microwave Studio" module in the project template.
2. Select "MW & RF & Optical" and "Antennas" application.
3. Choose "Phased Array and Unit Cell" workflow.
4. Choose "Frequency Domain for unit cell calculations" solver and set all desired units.
5. For boundary conditions:
   - Set the four side walls to "unit cell"
   - Set the top boundary to "open"
   - Set the bottom boundary to "electric"
6. To simulate various feeding angles:
   - Change theta and phi values in the phase shift/scan angles tab under boundary conditions
   - Set the wave propagation direction to "Inward"
7. For accurate results, de-embed the Zmax port to the top surface of the unit cell:
   - Set the upper Z distance to a certain value (e.g., 10) in the background properties
   - Double-click the Zmax port in the navigation tree
   - Set the "distance to reference plane" to "-10"
8. For excitation:
   - Excite the unit cell with two linearly polarized waves (TE00 and TM00)
   - Set the number of Floquet modes to "2" in the Zmax properties
   - Note: You can set Floquet mode to "1" for vertical or horizontal excitation only
9. After simulation, extract the S11 results for TE and TM modes from the ID results folder

### Step 2: Full Reflectarray Simulation (CST Design Studio)

After completing the unit cell simulation, use CST Design Studio (not Microwave Studio) to simulate the entire reflectarray and the horn antenna:

1. Import the unit cell results into CST Design Studio
2. Create a model of the full reflectarray using the unit cell results
3. Add the horn antenna to the model
4. Set up the simulation parameters for the full system
5. Run the simulation and analyze the results

## Script Overview

The MATLAB script performs the following main steps:

1. Initializes CST Studio Suite and creates a new project
2. Sets up solver parameters and frequency range
3. Configures units, background, and boundary conditions
4. Defines materials (copper, Rogers RT5880, foam)
5. Creates the ground plane, isolation layer, and substrate
6. Reads element dimensions from an Excel file
7. Generates the reflectarray elements based on the read dimensions

## Customization

You can modify the following parameters in the script to customize your reflectarray design:

- Frequency range
- Array dimensions
- Substrate properties
- Element dimensions and positions

## Note

This script is designed for a specific reflectarray configuration. You may need to modify it to suit your particular design requirements. Always review and adjust the generated model in CST Studio Suite before running simulations.
