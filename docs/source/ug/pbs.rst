******
PBSPro
******

.. contents:: Conteúdo

Introdução
==========

O `PBS Pro <https://www.altair.com/pbs-professional/>`_ é um *job scheduler open-source* baseado no original PBS code desenvolvido pela NASA. Agora a Altair Engineering possui e mantém o PBS Pro Scheduler.

PBS Comandos
============
.. list-table:: Comandos básicos
   :align: center
   :header-rows: 1
   
   * - Comando
     - Descrição
     - Exemplo
   * - ``qsub``
     - Submite um job
     - ``qsub myjob``
   * - ``qstat``
     - Mostra o status dos jobs
     - ``qstat -u user1``
   * - ``qdel``
     - Delete um job
     - ``qdel 212345``
   * - ``qhold``
     - Suspende um job
     - ``qhold 200123``
   * - ``qrls``
     - Libera o job em hold
     - ``qrls -h u 200123``
   * - ``qrerun``
     - Termina a execução e submete novamente o job
     - ``qrerun 200012``
   * - ``tracejob``
     - Imprime informações de log do job
     - ``tracejob 201012``

.. _exemplos:

Exemplos de scripts
===================

Os exemplos dos scripts para o PBS estão disponiveis no servidor de login no diretório ``/sw/share/doc``. Conforme descrito em :doc:`/ug/introduction`, cada nó de processamento possui 24 cores/48 threads.  

Script Básico
-------------
O script abaixo pode ser usado como base para qualquer tipo de aplicação.

.. code-block:: bash
   :linenos:

   #!/bin/bash
   #PBS -l select=1:ncpus=48
   #PBS -l walltime=01:00:00
   #PBS -j oe
   #PBS -V
   #PBS -N <jobname>
   
   # load modules
   module load module1 [module2] [...]
   # change directory
   cd ${PBS_O_WORKDIR}
   
   ./prog

.. list-table:: Descrição detalhada do job
   :align: center
   :header-rows: 1

   * - Linha
     - Descrição
   * - 1
     - SHELL utilizado para os comandos do job
   * - 2
     - ``select=1`` aloca 1 node. ``ncpus=48`` aloca todos os 48 threads disponíveis no node
   * - 3
     - Total do tempo de processamento (*walltime*) do job
   * - 4
     - Os arquivos de saída e erro são direcionados para um único arquivo
   * - 5
     - (Opcional) As variáveis de ambiente do servidor de submissão são enviadas para o job
   * - 6
     - Define o nome do job
   * - 9
     - Módulos necessários para a execução do programa
   * - 11
     - O programa será executado no mesmo diretório em que o comando ``qsub`` foi executado
   * - 13
     - Execução do programa ``prog``

.. note::

   Caso seja de interesse pode-se incluir duas linhas com os parâmetros ``#PBS -m ae`` e ``#PBS -M sua_conta@seu_dominio.com.br``, logo após a linha *6*, caso queiram receber um e-mail com informações de quando o job terminar ou for abortado. Caso use esta opção, por favor, verifique se o seu e-mail foi preenchido **corretamente**.

OpenMP
------

.. code-block:: bash
   :emphasize-lines: 2,13

   #!/bin/bash
   #PBS -l select=1:ncpus=48:ompthreads=24
   #PBS -l walltime=01:00:00
   #PBS -j oe
   #PBS -V
   #PBS -N OpenMP

   # load modules
   module load intel/2019.4
   # change directory
   cd ${PBS_O_WORKDIR}
   # environment (if necessary)
   #export OMP_NUM_THREADS=24
   # run
   ./prog

.. note::

   Repare nas linhas em destaque. A quantidade de threads de um job pode ser definida pelo PBS incluindo o parâmetro ``:ompthreads=24`` ou descomentando a linha do comando ``export OMP_NUM_THREADS=24``.

MPI
---

.. code-block:: bash
   :emphasize-lines: 2, 13
   
   #!/bin/bash
   #PBS -l select=2:ncpus=48:mpiprocs=24
   #PBS -l walltime=01:00:00
   #PBS -j oe
   #PBS -V
   #PBS -N mpi-intel
   
   # load modules
   module load intel/2019.4
   # change directory
   cd ${PBS_O_WORKDIR}
   # run
   mpirun ./prog

.. note::

   Repare nas linhas em destaque. A quantidade de processos MPI por nó de processamento pode ser definida pelo PBS incluindo o parâmetro ``:mpiprocs=24``. Desta maneira o parâmetro ``-np=48`` do ``mpirun`` pode ser omitido, isto é, ``2 nodes x 24 procs = 48``. Isto é uma grande vantagem pois facilita a manutenção do job caso haja alguma modificação na quantidade de processos MPI. Bastando para isso modificar apenas a primeira linha do job.

.. note::

   As bibliotecas MPI do compilador Intel são carregadas automaticamente ao carregar o module do compilador Intel. Neste exemplo, ``module load intel/2019.4``.
 
.. hint:: 

   Se o seu programa usufrui dos threads, os parâmetros ``mpiprocs`` e ``ompthreads`` podem ser **omitidos** ou modificados para ``:mpiprocs=48`` ou  ``:ompthreads=48``, caso contrário mantenham eles como ``24`` que corresponde ao número de cores.

Submissão de job
================

Submetendo um batch job
-----------------------
Usando como base um dos jobs scripts de exemplo, mostrados anteriormente no item :ref:`exemplos`. 

.. code-block:: bash

   user1@service1:~/test> qsub mpi-intel.job
   233180.service1

Acompanhando o status do job
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: bash

   user1@service1:~/test> qstat -u user1
   service1:
                                                               Req'd  Req'd   Elap
   Job ID          Username Queue    Jobname    SessID NDS TSK Memory Time  S Time
   --------------- -------- -------- ---------- ------ --- --- ------ ----- - -----
   233181.service1 user1    workq    mpi-intel     --    2  96    --  01:00 Q   --


Neste exemplo, o status do job é ``Q``. O status de um job pode ser:

* ``R``: job sendo executado
* ``Q``: está na fila esperando recurso para ser executado
* ``H``: job em hold
* ``S``: job suspenso
* ``E``: job terminando

Submetendo um job interativo
----------------------------

Para submeter um job interativo deve usar o comando ``qsub -I``. O *job scheduler* procurará um nó de computação disponível e fornecerá um shell de logon, se houver algum disponível. Neste exemplo, o node alocado foi o ``r2i2n9``.

.. code-block:: bash

  user1@service1:~> qsub -I
  qsub: waiting for job 233174.service1 to start
  qsub: job 233174.service1 ready
  
  Directory: /home/users/user1
  Thu Aug  6 14:27:18 UTC 2020
  user1@r2i2n9:~>

.. note::
   Para executar aplicativos gráficos em uma sessão interativa, adicione no comando a opção ``-X``, que permite o encaminhamento da interface gráfica. Por exemplo, ``qsub -I -X`` ou ``qsub -IX``. Pode-se adicionar também as variáveis de ambiente do servidor incluindo a opção ``-V``, obtendo o seguinte comando ``qsub -I -X -V`` ou ``qsub -IXV``.

.. admonition:: Maiores informações

   Através do comando ``man pbs`` ou do `PBS Professional User's Guide <https://www.altair.com/pbs-works-documentation/>`_.

