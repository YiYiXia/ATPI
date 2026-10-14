# ATPI

Code for "Interaction Potential between Anisotropic Particles: from Measurements to Tailored Design"

- GitHub: https://github.com/YiYiXia/ATPI

## Parameters in `config.ini`

| Parameter  | Description                                       | Example Value                  |
| ---------- | ------------------------------------------------- | ------------------------------ |
| `GPU_N`    | The number of GPUs used in parallel               | `4`                            |
| `THREADS`  | The number of threads per GPU                     | `32`                           |
| `BLOCKS`   | The number of blocks per GPU                      | `32`                           |
| `DATANAME` | Snapshot file of particles; supports `.txt`       | `output49152`                  |
| `TIMENAME` | Time index of snapshots; supports `.txt`          | `times49152`                   |
| `GRNAME`   | `$g(r, \theta, \phi)$` file name; supports `.txt` | `grTH49152_r400_theta40_phi40` |
| `xlen`     | The X size of the particle region, rectangle      | `30.0`                         |
| `ylen`     | The Y size of the particle region, rectangle      | `30.0`                         |
| `maxr`     | Maximum radius range of `g(r, \theta, \phi)`      | `6.81`                         |
| `minr`     | Minimum radius range of `g(r, \theta, \phi)`      | `0.81`                         |
| `rNum`     | Bin numbers of radius                             | `400`                          |
| `thetaNum` | Bin numbers of `\theta`                           | `40`                           |
| `phiNum`   | Bin numbers of `\phi`                             | `40`                           |
| `gridx`    | The X size of the insertion grid                  | `40`                           |
| `gridy`    | The Y size of the insertion grid                  | `40`                           |
| `ntheta`   | Orientation number of trial particle              | `10`                           |

## Data Format

### Input

#### 1. `g(r, \theta, \phi)`

Example: `grTH49152_r400_theta40_phi40.txt`

```text
Rows Columns
g(r_0, \theta_0, \phi_0)
g(r_1, \theta_0, \phi_0)
g(r_2, \theta_0, \phi_0)
...
```

The sequence of `g(r_i, \theta_j, \phi_k)` in the file is:

```text
i + j * rNum + k * rNum * thetaNum
```

#### 2. Time index

Example: `times49152.txt`

```text
Rows Columns
0
sum of particles number in 1st frame
sum of particles number in 1st and 2nd frame
...
sum of particles number in N frame
```

#### 3. Particle configuration

Example: `output49152.txt`

```text
Rows Columns
x  y  cos(\theta)  sin(\theta)  time  ID
...
```

### Output

#### Potential file

Example: `U_N49152.000_r400.000_theta40.000_phi40.000_iter1.000.txt`

```text
Rows Columns
u(r_0, \theta_0, \phi_0)
u(r_0, \theta_0, \phi_1)
u(r_0, \theta_0, \phi_2)
...
```

The sequence of `u(r_i, \theta_j, \phi_k)` in the file is:

```text
(i - 1) * thetaNum * phiNum + (j - 1) * phiNum + k
```

## Usage

The executable file is named `ATPI`.

Run `ATPI` to perform the potential measurement:

```bash
./ATPI
```

Make sure `config.ini` is properly configured and all required input files are placed in the working directory before running.
