# ClaymoreUW
## Claymore for Engineering - Multi-GPU Material Point Method 

#

<div style="display: flex; justify-content: center;">
  <a href="https://github.com/NHERI-SimCenter/HydroUQ/#gh-light-mode-only"><img width=256px src="https://github.com/NHERI-SimCenter/HydroUQ/icons/HydroUQ_Icon_Black_BorderRight.svg#gh-light-mode-only" align="left" /></a>
  <a href="https://github.com/NHERI-SimCenter/HydroUQ/#gh-dark-mode-only"><img width=256px src="https://github.com/NHERI-SimCenter/HydroUQ/icons/HydroUQ_Icon_White_BorderRight.svg#gh-dark-mode-only" align="left" /></a>
  <span style="display:inline-block; width: 25px;"></span>
  <div>
    <p>
      <h3 class="subtitle"><b>ClaymoreUW - Engineering Tool</b></h3>
      <h3>Claymore for Engineering - Multi-GPU Material Point Method</h3>
      <h5><i>Justin Bonus and Pedro Arduino</i></h5>
      <h5>Arduino Geomechanics and NHERI SimCenter, 2021-2025</h5>
      <br>
    </p>
  </div>
</div>

---

[![Latest Release](https://img.shields.io/github/v/release/NHERI-SimCenter/HydroUQ?color=blue&label=Latest%20Release)](https://github.com/NHERI-SimCenter/HydroUQ/releases/latest)   <span style="display:inline-block; width: 20px;"></span> [![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.10902090.svg)](https://doi.org/10.5281/zenodo.10902090)   <span style="display:inline-block; width: 20px;"></span> [![Build status](https://ci.appveyor.com/api/projects/status/k1cfrfmjsq14akso?svg=true)](https://ci.appveyor.com/project/fmckenna/hydrouq)  <span style="display:inline-block; width: 20px;"></span> [![License](https://img.shields.io/badge/License-BSD%202--Clause-blue)](https://raw.githubusercontent.com/NHERI-SimCenter/HydroUQ/master/LICENSE)  <span style="display:inline-block; width: 20px;"></span> [![GitHub](https://img.shields.io/badge/NHERI--SimCenter-%23121011.svg?style=for-the-badge&logo=github&logoColor=white)](https://github.com/NHERI-SimCenter)  <span style="display:inline-block; width: 20px;"></span>  [![LinkedIn Follow](https://img.shields.io/badge/nheri--simcenter-%230077B5.svg?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/company/nheri-simcenter) <span style="display:inline-block; width: 20px;"></span>  [![YouTube Subscribe](https://img.shields.io/badge/DesignSafe-%23FF0000.svg?style=for-the-badge&logo=YouTube&logoColor=white)](https://www.youtube.com/@DesignSafe) <span style="display:inline-block; width: 20px;"></span>  

---

<div style="display: flex; justify-content: center;">
    <img src="https://github.com/JustinBonus/HydroUQ/images/NHERI_SimCenter_DamBreakAnimation_VelocityPressureVisualized_2.5MParticles_res0.05m_23012023.gif" alt="Dam Break Animation" width="45%" />
    <img src="https://github.com/JustinBonus/HydroUQ/images/HydroUQ_MPM_3DViewPort_OSULWF_2024.04.25.gif" alt="HydroUQ MPM 3D ViewPort OSULWF" width="53%" />
</div>

---


Authors:
[Justin Bonus](https://github.com/JustinBonus)\, 
[Pedro Arduino](https://github.com/parduino)

<div align="left">
    <a href="https://claymore.readthedocs.io/en/latest/"> Documentation </a>
</div>

## Data-Repositories

Comparison data of ClaymoreUW MPM to DualSPHysics SPH and STAR-CCM+ CFD against stochastic experiments by Goserberg et al. 2016. For comparison details, see [Bonus et al. 2025](https://doi.org/10.1016/j.coastaleng.2024.104672), "Tsunami Debris Motion and Loads in a Scaled Port Setting: Comparative Analysis of Three State-of-the-Art Numerical Methods Against Experiments", published in Coastal Engineering.

[DesignSafe DataDepot Repository](https://www.designsafe-ci.org/data/browser/public/designsafe.storage.published/PRJ-5846)

## Description

Opensource code for Multi-GPU MPM. It is a modified fork from opensource code [page](https://github.com/penn-graphics-research/claymore) for the SIGGRAPH 2020 paper:

**A Massively Parallel and Scalable Multi-GPU Material Point Method** 

[page](https://sites.google.com/view/siggraph2020-multigpu)\, [pdf](https://www.seas.upenn.edu/~cffjiang/research/wang2020multigpu/wang2020multigpu.pdf)\, [supp](https://www.seas.upenn.edu/~cffjiang/research/wang2020multigpu/supp.pdf)\, [video](https://vimeo.com/414136257)


<!--
<p float="left">
<img src="Data/Clips/faceless.gif" height="128px"/>
<img src="Data/Clips/flow.gif" height="128px"/>
<img src="Data/Clips/chains.gif" height="128px"/>
<img src="Data/Clips/cat.gif" height="128px"/>
</p>
-->

## Compilation
This is a cross-platform C++/CUDA cmake project. The minimum version requirement of cmake is 3.16, yet the latest version is generally recommended. The required CUDA version is 10.2 or 11.

Currently, *supported OS* includes Windows 10 and Ubuntu (>=18.04), and *tested compilers* includes gcc8.4, msvc v142, clang-9 (includes msvc version). 

### Build
Run the following command in the *root directory*. Note that adding "--config Release" to the last command is needed when compiling using msvc.
```mkdir build
cd build
cmake ..
cmake --build .
```

Or configure the project using the *CMake Tools* extension in *Visual Studio Code* (recommended).

### Formulation

> Time-Integration (Explicit)
> Material models (Fixed-corotated, NA Cam-Clay, Drucker-Prager, Weakly Comp. Fluid)
> Shape Function (2nd Order B-Spline)
> Transfer Scheme (Affine Particle-In-Cell)
> Kernel (Grid-to-Particle-to-Grid)

### Input

JSON input files are used to configure some simulation settings.

Currently, binary position data and the level-set (signed distance field) [data](https://github.com/littlemine/Data) are accepted as input files for particles. Uniformly sampling particles from analytic geometries is another viable way for the initialization of models.

Starting from an \*.obj or \*.stl file, SDFGen [page](https://github.com/wdas/SDFGen) can make appropiate \*.sdf files. 

### Output

Particle output includes 
> Position (x, y, z)
> Stress ($\sigma_{1}$, $\sigma_{2}$, $\sigma_{3}$)
> Deformation Gradient ($J = ||F||$)

Particle data is segmented by object and device.

Grid output includes
> Index (x, y, z)
> Mass (m)
> Momentum ($M_{x}$, $M_{y}$, $M_{z}$)

Grid data is dynamic (inactive cells not included) and down-sampled (one block output per 4x4x4 cells)

Outputs are binary geometry files (\*.bgeo). Houdini Apprentice can render these efficiently.


### Run Demos
The project provides the following GPU-based schemes for MPM:
- **GMPM**: Improved single-GPU pipeline
- **MGSP**: Static geometry (particle) partitioning multi-GPU pipeline
- **WASIRF**: Single-GPU simulation of flume experiments. 
<!--
- dynamic spatial partitioning multi-GPU pipeline
-->

Go to *Projects/\*\**, run the executable.

## Code Usage
> Use the codebase in another cmake c++ project.

Directly include the codebase as a submodule, and follow the examples in the *Projects*.

> Develop upon the codebase.

Create a sub-folder in *Projects* with a cmake file at its root.

## Bibtex

Please cite the original paper if you use this code for your research: 
```
@article{Wang2020multiGMPM,
    author = {Xinlei Wang* and Yuxing Qiu* and Stuart R. Slattery and Yu Fang and Minchen Li and Song-Chun Zhu and Yixin Zhu and Min Tang and Dinesh Manocha and Chenfanfu Jiang},
    title = {A Massively Parallel and Scalable Multi-GPU Material Point Method},
    journal = {ACM Transactions on Graphics},
    year = {2020},
    volume = {39},
    number = {4},
    articleno = {Article 30}
}
```

## Credits
This project draws inspirations from [Taichi](https://github.com/taichi-dev/taichi), [GMPM](https://github.com/kuiwuchn/GPUMPM).



### Dependencies
The following libraries are adopted in our project development:

- [cub](http://nvlabs.github.io/cub/) (now replaced by Thrust)
- [fmt](https://fmt.dev/latest/index.html)

For particle data IO and generation, we use these two libraries in addition:

- [partio](http://partio.us/)
- [SDFGen](https://github.com/christopherbatty/SDFGen)

Due to the C++ standard requirement (at most C++14) for compiling CUDA (10.2) code, we import these following libraries as well:

- [function_ref](https://github.com/TartanLlama/function_ref)
- [optional](https://github.com/TartanLlama/optional)
- [variant](https://github.com/mpark/variant)
