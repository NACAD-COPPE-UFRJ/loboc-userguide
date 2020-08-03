Module Environment
==================

Introdução:
O module é usado para facilitar o chaveamento de ambientes de programação. Esta ferramenta permite que o usuário escolha qual(is) ferramenta(s) deseja usar, como por exemplo, versão do compilador, biblioteca matemática, MPI, etc.

**Utilização do Module**

Comandos basicos do module.

+-------------------------------------------+---------------------------------------------+
| Comando                                   | Descrição                                   |
+===========================================+=============================================+
| module list                               | lista os módulos carregados                 |
+-------------------------------------------+---------------------------------------------+
| module avail                              | lista os módulos disponiveis                |
+-------------------------------------------+---------------------------------------------+
| module help [modulefile]                  | mostra a sintaxe do comando module          |
+-------------------------------------------+---------------------------------------------+
| module load modulefile [modulefile ...]   | carrega o(s) módulo(s) correspondente(s)    |
+-------------------------------------------+---------------------------------------------+
| module unload modulefile [modulefile ...] | descarrega o(s) módulo(s) correspondente(s) |
+-------------------------------------------+---------------------------------------------+

**Exemplos de Uso do Module**

Segue abaixo alguns exemplos de como utilizar o comando module.
Nenhum módulo é carregado por padrão.

.. code-block:: bash

   user@service1:~> module list
   No Modulefiles Currently Loaded.

O comando abaixo lista os módulos disponiveis. É importante observar que os módulos são separados por grupos. Deve-se ter o cuidado de utiliza-lo de forma correta. Por exemplo, os modulos abaixo do /sw/apps/pgi16/modulefiles devem ser utilizado junto com o compilador PGI. Outro exemplo, uma das implementações do padrão MPI é feita através do mvapich e este por sua vez tem 3 versões diferentes, uma para cada compilador (PGI, Intel e GNU).

.. code-block:: bash

  user@service1:~> module avail
  
  --------------------------------------- /usr/share/modules/modulefiles   ---------------------------------------
  mpt/2.13    perfboost   perfcatcher
  
  ----------------------------------------- /sw/apps/pgi16/modulefiles -----------------------------------------
  hdf5/1.8.10p1/2016                pgi/16.7(default)                 pnetcdf/1.6.1/mpich-3.2/2016
  mvapich/2.1/2016                  pgi/2016                          pnetcdf/1.6.1/mvapich2-2.1/2016
  netcdf/4.3.3.1/2016               pgi64/16.5                        pnetcdf/1.6.1/openmpi-1.10.2/2016
  openmpi/1.10.2/2016               pgi64/16.7(default)               PrgEnv-pgi/16.5
  pgi/16.5                          pgi64/2016                        PrgEnv-pgi/16.7(default)
  
  ----------------------------------------- /sw/apps/suse/modulefiles - -----------------------------------------
  mvapich-gnu/2.2                 openblas/multi-threaded/0.2.18  openblas/single-threaded/0.2.18 singularity
  mvapich-intel/2.2               openblas/multi-threaded/0.2.19  openblas/single-threaded/0.2.19
  
  ---------------------------------------------- /sw/modulefiles -----------------------------------------------
  intel/2016.3.210          intel/2016.4.072(default) java/jdk/1.8.0_102        java/jre/1.8.0_102

Obtendo informações sobre os módulos.

.. code-block:: bash

  user@service1:~> module help intel
  
  ----------- Module Specific Help for 'intel/2016.4.072' -----------
  
  The Intel module enables the Intel family of compilers (C/C++,
  Fortran and MPI) and updates the $PATH, $LD_LIBRARY_PATH,
  $INCLUDE, and $MANPATH environment variables to access the
  compiler binaries, libraries, include files, and available man
  pages, respectively.
  
  See the man pages for icc, icpc, and ifort for detailed information
  on available compiler options and command-line syntax.
  
  See the man pages for idb or idbc for more information on using the
  Intel debugger.
  
  Version 2016 SP4

.. code-block:: bash

  user@service1:~> module whatis intel
  intel                : Name: Intel Compiler
  intel                : Version: 2016 SP4
  intel                : Category: compiler, runtime support
  intel                : Description: Intel Compiler Family (C/C++/Fortran for x86_64)
  intel                : URL: http://software.intel.com/en-us/articles/intel-compilers/

Carregando, listando e descarregando um módulo.

.. code-block:: bash

  user@service1:~> module load intel
  
  user@service1:~> module list
  Currently Loaded Modulefiles:
    1) intel/2016.4.072
  
  user@service1:~> module unload intel
  
  user@service1:~> module list
  No Modulefiles Currently Loaded.


