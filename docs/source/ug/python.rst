******
Python
******

.. contents:: Conteúdo

Introdução
==========
Normalmente ao se trabalhar com a linguagem Python é necessário instalar algumas dependências. Como não é viável instalar todos os pacotes no sistema operacional, pois, dependendo da versão, algumas dependências são incompatíveis entre si. Entretanto, pode-se contornar o problema utilizando um gerenciador de pacotes **Python** que pode ser o ``Conda`` ou o ``Virtualenv``. O gerenciador **Conda** faz parte de dois *modules* do LoboC, o ``Anaconda`` e o ``Miniconda``.

.. note::

  O LoboC tem instalado apenas o gerenciador ``Conda``. 


Anaconda
========

O **Anaconda** é uma das distribuições mais utilizadas para *Data Science* e *Machine Learning*. Ele inclui mais de 300 pacotes. A utilização no LoboC é muito simples basta carregar o module e usar.

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

Pode-se perceber facilmente a mudança da versão do **Python** logo após o carregamento do module do **Anaconda**.

.. code-block:: bash

  user1@service1:~> python
  Python 3.8.3 (default, Jul  2 2020, 16:21:59)
  [GCC 7.3.0] :: Anaconda, Inc. on linux
  Type "help", "copyright", "credits" or "license" for more information.
  >>>

.. note::

   O **Anaconda** também permite a criação de novos ambientes como mostrado no item **Miniconda**.


Miniconda
=========

Nem sempre os pacotes do **Anaconda** são o suficiente para atender todas as necessidades. Então neste caso, recomenda-se o uso do **Miniconda**, pois ele carrega o mínimo de pacotes para fazer o gerenciamento e permite que o usuário crie um novo ambiente de forma otimizada. 

Por exemplo, suponha que seja necessário a instalação do *pytorch*. Nos itens a seguir serão mostrados os procedimentos para a criação de um novo ambiente chamado ``pytorch``.

Criar um novo ambiente
----------------------

Para criar o ambiente chamado ``pytorch`` basta seguir o procedimento abaixo.

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


Ajustar o ambiente
------------------

.. error::

  Na primeira vez que ativar o primeiro ambiente com o comando ``conda activate`` ele dará um erro durante a inicialização.

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

Para corrigir basta digitar o comando abaixo e depois reabra o shell corrente ou um novo shell.

.. code-block:: bash

  user1@service1:~> conda init bash
  ...
  modified      /home/users/user1/.bashrc
  
  ==> For changes to take effect, close and re-open your current shell. <==

Repare que agora no ``prompt`` aparece o ambiente **conda**. O ambiente padrão é o ``(base)``. Ao ativar um novo ambiente, por exemplo o ``pytorch`` ele mudará o ambiente e o ``prompt``. Para desativar o ambiente basta digitar ``conda deactivate``.

.. code-block:: bash

  (base) user1@service1:~> conda activate pytorch
  (pytorch) user1@service1:~> conda deactivate 
  (base) user1@service1:~>

Pode-se optar por não ativar automaticamente o conda durante o ``login``. Basta mudar o parâmetro ``auto_activate_base`` para ``false``, digitando o comando a seguir.

.. code-block:: bash

  (base) user1@service1:~> conda config --set auto_activate_base false

No novo ``login`` não aparece mais o ambiente ``(base)`` do **conda** no prompt. Para ativar o ambiente ``pytorch`` carregue o *module* e ative o novo ambiente.

Listar os ambientes
-------------------

Para listar os ambientes disponiveis use o comando ``conda env list``.

.. code-block:: bash

  user1@service1:~> module load miniconda3
  
  user1@service1:~> conda env list
  # conda environments:  
  #
  pytorch                  /home/users/user1/.conda/envs/pytorch
  base                  *  /sw/apps/python/miniconda3/4.8.3
  
Instalar pacotes no ambiente
----------------------------

Para instalar os pacotes selecione o ambiente desejado e instale os pacotes. Por exemplo, instalar o **pytorch** para **CPU**.

.. code-block:: bash

  user1@service1:~> conda activate pytorch
  (pytorch) user1@service1:~>

  user1@service1:~> conda install pytorch-cpu
  Collecting package metadata (current_repodata.json): done
  Solving environment: done
  
  ## Package Plan ##
  
    environment location: /sw/apps/python/miniconda3/4.8.3
  
    added / updated specs:
      - pytorch-cpu
  ...
   Proceed ([y]/n)? y


.. note::

  Também é possível usar o comando ``pip`` para fazer a instalação de pacotes dentro do ambiente virtual, mas para isso é necessário que o ``python`` e ``pip`` já estejam previamente instalados.



Remover um ambiente
-------------------

Removendo um ambiente com todos os pacotes.

.. code-block:: bash

  (pytorch) user1@service1:~> conda deactivate
  user1@service1:~> conda remove -n pytorch --all

