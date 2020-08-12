******
Python
******

.. contents:: Conteúdo

Introdução
==========
Ao se trabalhar com a linguagem Python pode ser necessário o uso de algumas dependências. Não é viável instalar todos os pacotes no sistema, pois alguns deles são incompatíveis com outras versões do sistema. Para isso devemos utilizar um gerenciador de pacotes Python que pode ser o Conda ou o Virtualenv. O gerenciador conda faz parte de dois modules do sistema o ``Anaconda`` e o ``Miniconda`` que serã descritos posteriormente.

Anaconda
========

.. code-block:: bash

  user1@service1:~> module load anaconda3
  user1@service1:~> module list
  Currently Loaded Modulefiles:
  1) anaconda3/2020.07
  
  user1@service1:~> conda list
  # packages in environment at /sw/apps/python/anaconda3/2020.07:
  #
  # Name                    Version                   Build  Channel
  _ipyw_jlab_nb_ext_conf    0.1.0                    py38_0
  _libgcc_mutex             0.1                        main
  alabaster                 0.7.12                     py_0
  anaconda                  2020.07                  py38_0
  ...
  python                    3.8.3                hcff3b4d_2
  ...

.. code-block:: bash

  user1@service1:~> conda env list
  # conda environments:
  #
  base                  *  /sw/apps/python/anaconda3/2020.07
  
  user1@service1:~> python
  Python 3.8.3 (default, Jul  2 2020, 16:21:59)
  [GCC 7.3.0] :: Anaconda, Inc. on linux
  Type "help", "copyright", "credits" or "license" for more information.
  >>>


Miniconda
=========

.. code-block:: bash

  user1@service1:~> module load miniconda3
  user1@service1:~> conda create -n pytorch
  Collecting package metadata (current_repodata.json): done
  Solving environment: done
  
  ## Package Plan ##
  
    environment location: /home/users/user1/.conda/envs/pytorch
  
  Proceed ([y]/n)? y
  
  Preparing transaction: done
  Verifying transaction: done
  Executing transaction: done 
  #
  # To activate this environment, use
  #
  #     $ conda activate pytorch
  #
  # To deactivate an active environment, use
  #
  #     $ conda deactivate

.. code-block:: bash

  user1@service1:~> conda activate pytorch
  
  CommandNotFoundError: Your shell has not been properly configured to use 'conda activate'.
  To initialize your shell, run
  
    $ conda init <SHELL_NAME>
  
  Currently supported shells are:
    - bash
    - fish
    - tcsh
    - xonsh
    - zsh
    - powershell
  
  See 'conda init --help' for more information and options.
  
  IMPORTANT: You may need to close and restart your shell after running 'conda init'.

.. code-block:: bash

  user1@service1:~> conda init bash
  ...
  modified      /home/users/user1/.bashrc
  
  ==> For changes to take effect, close and re-open your current shell. <==

.. code-block:: bash

  user1@service1:~> bash
  (base) user1@service1:~> conda activate pytorch
  (pytorch) user1@service1:~> conda deactivate 
  (base) user1@service1:~>

Se preferir não ativar o conda por padrão basta mudar o parâmetro ``auto_activate_base`` para ``false``, digitando o comando abaixo.

.. code-block:: bash

  (base) user1@service1:~> conda config --set auto_activate_base false

.. code-block:: bash

  user1@service1:~> module load miniconda3
  
  user1@service1:~> conda env list
  # conda environments:  
  #
  pytorch                  /home/users/user1/.conda/envs/pytorch
  base                  *  /sw/apps/python/miniconda3/4.8.2
  
  user1@service1:~> conda activate pytorch
  (pytorch) user1@service1:~>



