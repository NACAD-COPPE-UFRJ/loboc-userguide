******
PBSPro
******

.. contents:: Conteúdo

OpenMP
======

.. code-block:: bash
   :linenos:
   :emphasize-lines: 2,13

   #!/bin/bash
   #PBS -l select=1:ncpus=48:ompthreads=24
   #PBS -l walltime=01:00:00
   #PBS -j oe
   #PBS -V
   #PBS -N OpenMP

   # load modules
   module load intel
   # change directory
   cd ${PBS_O_WORKDIR}
   # environment (if necessary)
   #export OMP_NUM_THREADS=24
   # run
   ./prog

MPI
===

.. code-block:: bash
   :linenos:
   :emphasize-lines: 2, 13
   
   #!/bin/bash
   #PBS -l select=2:ncpus=48:mpiprocs=24
   #PBS -l walltime=01:00:00
   #PBS -j oe
   #PBS -V
   #PBS -N mpi-intel
   
   # load modules
   module load intel
   # change directory
   cd ${PBS_O_WORKDIR}
   # run
   mpirun ./prog





