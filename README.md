# Venturi-meter-multiphase-simulation

In this simulation I applied the simplest multiphase solver available in OpenFOAM to simulate a flow through a classical Venturi meter. In this project I created my on CAD geometry of a standardized venturi meter and compared the simulation results with calculations based on the well known equations regarding the Venturi meter.

## Pre-analysis

The geometry I used for the Venturi flow meter comes from [this papar](https://www.researchgate.net/publication/264440733_A_CFD_study_of_the_effect_of_venturi_geometry_on_high_pressure_wet_gas_metering). You can see a drawing of the part I used in the Geometry and Mesh part.

Note: The throat pressure tappings are larger than prescribed in the [ISO 5167-4:2003](https://azaransanjesh.com/wp-content/uploads/2021/07/ISO_5167_4_2003-Venturi-tubes.pdf) standard. Despite this, the results are fairly accurate, but the geometry should be changed in order to make the simulations more akin to real-world use.

Using the Bernulli equation, the continuity equation, and the hydrostatic pressure equation, it is trivial to arrive at the following equation for the mercury level height diference h:

<p align="center">
$h = \frac{15\rho U_1^2}{2g(\rho_{Hg}-\rho)}$
</p>

The expected value of h is 1.5 cm.

## Geometry and Mesh

I made the geometry and a drawing with SolidWorks (the files are available in the geometry folder), then saved them in the STL format and imported it into Blender where I extracted and named the patches in order to prepare them for meshing with snappyHexMesh.

<p align="center">
    <img src="https://user-images.githubusercontent.com/84512701/218510208-38b4f9c0-c99a-45e7-81ba-7ecbb2c52584.png")>
</p>

After that I made a relatively simple mesh with snappyHexMesh (all parameters can be seen in the snappyHexMeshDict located in the system folder).

## Numerical Model

For this simulation I used interFoam, which is a transient, incompressible, turbulent, immisible, isothermal, VOF solver.

For the turbulence model I used the K Omega SST model and initialized the their values using these [recommendations](https://turbmodels.larc.nasa.gov/sst.html).

## Results and postprocessing

After reaching a steady level, the observed height difference is around 1.46 cm. 

<p align="center">
<img src="https://user-images.githubusercontent.com/84512701/218527376-60f0c4d5-88b7-43f4-ac81-c16d4c9c2b11.png")>
</p>

This is very close to the expected value, but still, simulations with different parameters should be added in the future for more validation.
