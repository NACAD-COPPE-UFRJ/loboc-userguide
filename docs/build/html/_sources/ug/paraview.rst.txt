Paraview
========

**Introdução**

Paraview_ é um programa de visualização *opensource* que está disponível no LoboC.
Para poder utilizar siga as orientações abaixo.

**Requisitos**

Para utilizar o Paraview é necessário criar um túnel SSH conforme ilustrado na figura_ abaixo 

.. figure:: ../images/Rc-tunnel.png

- 2 terminais conectados ao LoboC. Os terminais serão identificados como ``t1$`` e ``t2$``
- cliente paraview instalado na workstation de visualização (computador do usuário)

.. note::

  A versão do Paraview instalado no cliente *deve* ser a mesma do servidor.

**Etapas**

1) :guilabel:`Workstation`: Configure o client Paraview para se conectar ao LoboC.

- Selecione no menu do Paraview a opção ``File->Connect...`` e crie uma nova configuração conforme ilustrado abaixo.

.. figure:: ../images/pv-001.png

- Depois clique em ``Configure`` e ``Save``.

2) :guilabel:`Terminal 1`: Conecte-se ao LoboC do terminal 1, onde `xxx` corresponde a porta SSH de conexão com o LoboC. Carregue o module do Paraview, submeta um job iterativo e aguarde a alocação do node, conforme mostrado abaixo.

.. code-block:: bash
  
  t1$ ssh -p xxx user@loboc.nacad.ufrj.br
  user@service1:~> module load ParaView/5.8.0
  user@service1:~> qsub -I -V
  qsub: waiting for job 232826.service1 to start
  qsub: job 232826.service1 ready
  
  user@r2i2n9:~> 

.. warning::
  
  O tempo máximo de um job iterativo (*walltime*) é de no máximo de 2 horas.

3) :guilabel:`Terminal 2`: Neste exemplo o node alocado foi o ``r2i2n9``. Faça uma nova conexão do *t2* para o LoboC fazendo um túnel SSH para o node alocado.

.. code-block:: bash
  
  t2$ ssh -L 11111:r2i2n9:11111 -p xxx user@loboc.nacad.ufrj.br

4) :guilabel:`Terminal 1`: Volte ao *t1*. Carregue o module do Paraview no node e inicie o ``pvserver``

.. code-block:: bash
  
  user@r2i2n9:~> module load ParaView/5.8.0
  user@r2i2n9:~> pvserver --server-port=11111
  Waiting for client...
  Connection URL: cs://r2i2n9:11111
  Accepting connection(s): r2i2n9:11111

5) :guilabel:`Workstation`: Conecte ao LoboC selecionando a configuração feita para o LoboC e aguarde aparecer a mensagem abaixo no terminal 1 (`t1`). Pronto já pode usar o paraview.

.. code-block:: bash
  
  Waiting for client...
  Connection URL: cs://r2i2n9:11111
  Accepting connection(s): r2i2n9:11111
  Client connected.

Repare na figura abaixo que no *Pipeline Browser* mostra a conexão com o LoboC.

.. figure:: ../images/pv-003.png


6) Ao terminar o uso vá no menu do Paraview na workstation e selecione ``File->Disconnect``. Depois vá ao terminal 1 (*t1*) e digite ``exit``. Para finalizar feche todas as conexões de *t1* e *t2*.

.. _Paraview: https://www.paraview.org/
.. _figura: https://www.paraview.org/Wiki/Reverse_connection_and_port_forwarding




