#Workshop 21 July 2023

## MPI with Python
[200~Parallel Computing in Python using mpi4py](https://research.computing.yale.edu/sites/default/files/files/mpi4py.pdf)

mpi == srun

### How:
$  module load anaconda3

$ conda create -n mpi mpi4py numpy scipy

$ conda init bash

Logout and login again

## Introduction to Conda for (Data) Scientists
[Link](https://carpentries-incubator.github.io/introduction-to-conda-for-data-scientists/)

----
# Command from workshop
### Conda
```
conda activate mpi
conda list
salloc -w zeta -t 1:0:0 -n 4
```
create basic_mpi.py
```
from mpi4py import MPI
comm = MPI.COMM_WORLD
print("%d of %d" % (comm.Get_rank(), comm.Get_size()))
```
run by mpi
```
mpirun -n 4 python basic_mpi.py
conda deactivate
```
### Jupyter (run on zeta)
```
module load anaconda3
salloc -w zeta -t 1:0:0 -n 4
ssh -X zeta
jupyter notebook --port=8041 --ip=0.0.0.0
```
### Singularity (run on zeta)
```
:~$ singularity run /shared/software/singularity/images/cistem_latest.sif 
Singularity> cistem
bash: cistem: command not found
Singularity> cisTEM
14:03:27: Error: Unable to initialize GTK+, is DISPLAY set properly?
Singularity> exit
exit
:~$ env | grep DIS
DISPLAY=:3.0
:~$ singularity run --nv --env DISPLAY=:3.0 /shared/software/singularity/images/cistem_latest.sif 
Singularity> cisTEM
```
** --nv = nvidia
Show nvidia detail
```
nvidia-smi
```

Pull and run image
```
singularity pull library://library/default/busybox
singularity run library://library/default/busybox
