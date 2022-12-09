**A sample VPIC particle dataset for local C2 development and testing**

[![License](https://licensebuttons.net/l/by/4.0/88x31.png)](https://creativecommons.org/licenses/by/4.0/)

C2 vpic sample dataset
================

```
XX              XXXXX XXX         XX XX           XX       XX XX XXX         XXX
XX             XXX XX XXXX        XX XX           XX       XX XX    XX     XX   XX
XX            XX   XX XX XX       XX XX           XX       XX XX      XX XX       XX
XX           XX    XX XX  XX      XX XX           XX       XX XX      XX XX       XX
XX          XX     XX XX   XX     XX XX           XX XXXXX XX XX      XX XX       XX
XX         XX      XX XX    XX    XX XX           XX       XX XX     XX  XX
XX        XX       XX XX     XX   XX XX           XX       XX XX    XX   XX
XX       XX XX XX XXX XX      XX  XX XX           XX XXXXX XX XX XXX     XX       XX
XX      XX         XX XX       XX XX XX           XX       XX XX         XX       XX
XX     XX          XX XX        X XX XX           XX       XX XX         XX       XX
XX    XX           XX XX          XX XX           XX       XX XX          XX     XX
XXXX XX            XX XX          XX XXXXXXXXXX   XX       XX XX            XXXXXX
```

This sample dataset is generated by running open source VPIC particle simulation code using a single process on a single node with result post-processed to transform local particle locations in a cell to global coordinates (X, Y, Z) while pre-calculating particle energies and storing them with the dataset. A total of 131,072 ions and 131,072 electrons were simulated and recorded.

A modified https://github.com/lanl/vpic/blob/master/sample/harris input deck was run. The resulting simulation had 480 timesteps. Simulation state was saved every 24 timesteps. The initial state (timestep 0) was recorded in `iparticle.0.0.bin` and `eparticle.0.0.bin`. The final state (timestep 480) was recorded in `iparticle.480.0.bin` and `eparticle.480.0.bin`. There are a total of 21 such file pairs. Each stores the state of 131,072 ions and the state of 131,072 electrons at a specific simulation timestep ranging from 0 to 480. Ions are stored in `iparticle` files. Electrons are stored in `eparticle` files. There are 42 files in total. Each file is 6MB in size.

Particles are 48 bytes each. Each particle has 9 fields. Both particle types share the same schema shown below. Particles are written to files one by one (48 bytes by 48 bytes) in a binary form with no encoding or compression. There is no headers or footers in a particle file.

# Particle Schema (48 bytes per particle)

```
8 bytes uint64_t ID             unique ID of a particle
8 bytes uint64_t padding
4 bytes float    x              location of particle in X direction
4 bytes float    y              location of particle in Y direction
4 bytes float    z              location of particle in Z direction
4 bytes float    i              index of the cell that had the particle
4 bytes float    ux             momentum of particle in X direction
4 bytes float    uy             momentum of particle in Y direction
4 bytes float    uz             momentum of particle in Z direction
4 bytes float    ke             kinetic energy of particle
```

**Acknowledgement**: C2 is developed under U.S. Government contract 89233218CNA000001 for Los Alamos National Laboratory (LANL), which is operated by Triad National Security, LLC for the U.S. Department of Energy/National Nuclear Security Administration. VPIC is a general purpose particle-in-cell simulation code developed by LANL. See https://github.com/lanl/vpic for more information.

**A much larger version of this dataset (15,728,640 particles per file, 256 files, 180GB total data) is also available at ftp://hpc-ftp.lanl.gov/data/operational/vpic/LA-UR-22-31691.tar**.
