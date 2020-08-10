.. modules

******************
Module Environment
******************

.. contents:: Conteúdo

Introdução
==========

O module é usado para facilitar o chaveamento de ambientes de programação. Esta ferramenta permite que o usuário escolha qual(is) ferramenta(s) deseja usar, como por exemplo, versão do compilador, biblioteca matemática, MPI, etc.

Utilização do Module
====================

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

Exemplos de Uso do Module
=========================

Segue abaixo alguns exemplos de como utilizar o comando module.
Nenhum módulo é carregado por padrão.

.. code-block:: bash

   user@service1:~> module list
   No Modulefiles Currently Loaded.

O comando abaixo lista os módulos disponiveis. É importante observar que os módulos são separados por grupos. Deve-se ter o cuidado de utiliza-lo de forma correta. Por exemplo, os modulos abaixo do ``/sw/apps/pgi16/modulefiles`` devem ser utilizado junto com o compilador PGI. Outro exemplo, uma das implementações do padrão MPI é feita através do ``mvapich`` e este por sua vez tem 3 versões diferentes, uma para cada compilador (PGI, Intel e GNU).

.. code-block:: bash

  user@service1:~> module avail
  
  ------------------------------- /usr/share/modules/modulefiles -----------------------------------
  mpt/2.13    perfboost   perfcatcher
  
  -------------------------------- /sw/apps/pgi16/modulefiles --------------------------------------
  hdf5/1.8.10p1/2016      pgi/16.7(default)                 pnetcdf/1.6.1/mpich-3.2/2016
  mvapich/2.1/2016        pgi/2016                          pnetcdf/1.6.1/mvapich2-2.1/2016
  netcdf/4.3.3.1/2016     pgi64/16.5                        pnetcdf/1.6.1/openmpi-1.10.2/2016
  openmpi/1.10.2/2016     pgi64/16.7(default)               PrgEnv-pgi/16.5
  pgi/16.5                pgi64/2016                        PrgEnv-pgi/16.7(default)
  
  ------------------------------- /sw/apps/suse/intel17/modulefiles --------------------------------
  hdf5/1.10.5-i17    nco/4.7.5          phdf5/1.10.5-i17   pio/2.3.0          R/3.5.3
  hdf5/1.8.18        ncview/2.1.7       phdf5/1.8.18       pnetcdf/1.8.1      szip/2.1.1
  hdf5/1.8.19        netcdf-intel/4.5.0 phdf5/1.8.19       R/3.5.1            udunits/2.2.26
  
  ------------------------------- /sw/apps/suse/intel19/modulefiles --------------------------------
  cdo/1.9.7.1           netcdf-parallel/4.7.2 phdf5/1.10.5          R/3.6.0
  hdf5/1.10.5           netcdf-serial/4.7.0   pnetcdf/1.11.2        szip-i19/2.1.1
  netcdf-parallel/4.7.0 netcdf-serial/4.7.2   pnetcdf/1.12.0        wgrib2/2.0.8

  --------------------------------- /sw/apps/suse/modulefiles --------------------------------------
  mvapich-gnu/2.2      openblas/multi-threaded/0.2.18  openblas/single-threaded/0.2.18 singularity
  mvapich-intel/2.2    openblas/multi-threaded/0.2.19  openblas/single-threaded/0.2.19
  
  -------------------------------------- /sw/modulefiles -------------------------------------------
  intel/2016.3.210     intel/2016.4.072(default) java/jdk/1.8.0_102        java/jre/1.8.0_102


.. note::
  
  Repare os diretórios dos modulefiles. Eles mostram a dependência entre os pacotes. Por exemplo, os modules abaixo do diretório ``/sw/apps/suse/intel17/modulefiles`` são os pacotes que foram compilados usando o compilador intel17. O mesmo acontece em outros diretórios. Outro exemplo, o diretório ``/sw/apps/suse/intel19/modulefiles`` contém os pacotes compilados com o intel19. Recomenda-se que utilize o mesmo compilador, no caso de dependência de pacotes, para evitar problemas de incompatibilidade.

.. warning::

  Os modules (incluindo as versões) utilizados para compilar **devem ser os mesmos** a serem incluidos no script de submissão do job.

Obtendo informações sobre os módulos
------------------------------------

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

Obtendo informações dos modules para compilação
-----------------------------------------------

Suponha que necessite do module ``netcdf-parallel/4.7.2`` para compilar o seu programa. Primeiro consulte qual compilador foi usado para compilar a biblioteca em questão.

.. code-block:: bash
   :emphasize-lines: 9
   
   user1@service1:~> module help netcdf-intel/4.5.0
    
   ----------- Module Specific Help for 'netcdf-intel/4.5.0' ---------
   
   Sets up the paths you need to use NetCDF.
   NetCDF-C      : 4.5.0
   NetCDF-CXX    : 4.3.0
   NetCDF-Fortran: 4.4.4
   Compiled with Intel 2017.4.196

A linha em detaque mostra que a versão usada foi o ``Intel 2017.4.196``. Recomenda-se então o uso da mesma versão do compilador ou da mesma familia ``Intel 2017.x``, isto é não deve se deve usar o compilador ``Intel 2019.x``. O comando abaixo deve ser utilizado para compilar e incluido no job para a sua execução.

.. code-block:: bash
 
   module load intel/2017.4.196

Ou da mesma familia, por exemplo.

.. code-block:: bash
 
   module load intel/2017.8

.. note::

   Quando o compilador GNU do sistema operacional é usado para compilar um ``module`` é **omitida** a informação sobre a versão utilizada para compilar.

Dependências
------------

Ao carregar um module todas as dependências, **excluindo** o compilador são carregadas.

.. code-block:: bash

 user1@service1:~> module list
 No Modulefiles Currently Loaded.
 user1@service1:~> module load netcdf-intel/4.5.0
 user1@service1:~> module list
 Currently Loaded Modulefiles:
   1) szip/2.1.1           2) hdf5/1.8.19          3) netcdf-intel/4.5.0


