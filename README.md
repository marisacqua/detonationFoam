#Note: We fixed the bug of the mixture-averaged transport model for detonationNSFoam_mixtureAverage solver. New codes about the mixture-averaged transport model refer to https://github.com/ZSHtju/reactingDNS_OpenFOAM. detonationNSFoam_Sutherland and detonationEulerFoam solvers are not changed.


# detonationFoam: An open-source solver for simulation of gaseous detonation based on OpenFOAM

## Motivation
Gas-phase detonation simulation considering detailed chemical reactions is usually troubled by the following problems: 
1. As the widely-used CFD toolbox, OpenFOAM does not provide a solver for compressible reactive flow in detonation simulation. 
2. More detailed multicomponent transport model is required for partial detonation simulations (e.g., the deflagration to detonation process) while OpenFOAM just provides the simple Sutherland model. 
3. The characteristic scale of detonation wave structure is small so that fine grid resolution is required but the adaptive mesh refinement library provided by OpenFOAM only works in 3D. 
4. The severe load imbalance caused by the chemical source term evaluation may greatly reduce the computation efficiency in parallel computing.

## Features
1. The species equations and detailed finite-rate chemistry are considered and thereby the compressible, multi-component, reactive flow can be simulated. 
2. The mixture-averaged transport model is used and it can accurately evaluate the detailed transport coefficients. 
3. The improved HLLC-P approximate Riemann solver is used and it has advantages in accurately capturing the propagation of shock wave and contact discontinuity. 
4. The two-dimensional adaptive mesh refinement (AMR) technique is incorporated into the solver so that the detonation front can be resolved by the finest meshes. 
5. The dynamic load balancing (DLB) algorithm is used to further improve the computational efficiency.

## Directory structure
Applications: 
1. applications/solvers/detonationFoam/detonationEulerFoam 
2. applications/solvers/detonationFoam/detonationNSFoam_Sutherland 
3. applications/solvers/detonationFoam/detonationNSFoam_mixtureAverage 

Libraries: 
1. applications/solvers/detonationFoam/DLB 
2. applications/solvers/detonationFoam/dynamicMesh2D 
3. applications/solvers/detonationFoam/fluxSchemes 

Documents:
doc/Manual_detonationFoam.pdf

Tutorials:
1. tutorials/1D_flame 
2. tutorials/1D_detonation 
3. tutorials/2D_detonation 

## Compiling 
1. The solver, detonationFoam, is developed based on OpenFOAM V6. Before installing the solver, please ensure you have installed OpenFOAM V6. Please refer to https://openfoam.org/download/6-ubuntu.

2. Compiling detonationFoam:

   ```bash
   cd applications/solvers/detonationFoam
   ./Allwmake
   ```

Note: If you want to use the detonationNSFoam_mixtureAverage solver, please use ANSYS CHEMKIN to fit the transport data of Chemkin format. The tran.out can be outputted when you select to process Transport properties with Fit with Verbose Output. Mode detailed steps can be found in https://github.com/ZSHtju/reactingDNS_OpenFOAM.

## Getting help and reporting bugs
Please submit a GitHub issue if you found a bug in the program. If you need help with the software or have further questions, contact sunjie_coe@pku.edu.cn and cz@pku.edu.cn.

##  Citation
If you use the code for your works and researches, please cite: 

   ```
   J. Sun, Y. Wang, B. Tian, Z. Chen, detonationFoam: An open-source solver for simulation of gaseous detonation based on OpenFOAM, Computer Physics Communications 292 (2023) 108859.
   ```
