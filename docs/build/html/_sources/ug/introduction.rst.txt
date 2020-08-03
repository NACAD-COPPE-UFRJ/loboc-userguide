Introdução
==========

O Supercomputador Lobo Carneiro possui capacidade de 226 teraflops, isto é, pode executar 226 trilhões de operações matemáticas por segundo.

O sistema de engenharia montado para o Lobo Carneiro permite que ele prescinda do acompanhamento presencial, como é a regra para os demais computadores de alto desempenho em atividade no Brasil. Sua instalação foi inédita do ponto de vista do controle e da automação, mas para isso foi necessário um alto nível de automação. Refrigeração e no-breaks precisam dialogar com o computador. O desligamento é preparado para ocorrer em temperaturas confortáveis, de forma que o equipamento não seja exposto a situações críticas. Há múltiplas camadas de proteção. Também há checkpoints para a recuperação dos trabalhos, quando ocorrer esse desligamento.

**HPE-SGI ICE-X**

+----------------------------------+---------------------------------------+
| 504 CPUs Intel Xeon (Haswell)    | 6048 cores                            |
+----------------------------------+---------------------------------------+
| Total de Nós de processamento    | 252                                   |
+----------------------------------+---------------------------------------+
| Total de Memória RAM             | 16 TBytes (distribuída)               |
+----------------------------------+---------------------------------------+
| Sistema de arquivo paralelo      | Intel Lustre (500 TBytes)             |
+----------------------------------+---------------------------------------+
| Armazenamento em disco           | 60 TBytes                             |
+----------------------------------+---------------------------------------+
| Rede                             | Infiniband FDR - 56 Gbs (Hypercube)   |
+----------------------------------+---------------------------------------+
| Sistemas operacional             | Suse Linux Enterprise Server (SLES)   |
+----------------------------------+---------------------------------------+
| Compiladores                     | Intel, PGI e GNU (Fortran-90 e C/C++) |
+----------------------------------+---------------------------------------+
| Bibliotecas MPI                  | MPT, Intel MPI, MVAPICH e OpenMPI     |
+----------------------------------+---------------------------------------+

**Especificação do nó de processamento**

+---------------------------+-------------------------------------------------------+
| Modelo                    | Intel(R) Xeon(R) CPU E5-2670 v3 @ 2.30GHz ("Haswell") |
+---------------------------+-------------------------------------------------------+
| Total cores por node      | 24 cores on two sockets (12 cores/socket)             |
+---------------------------+-------------------------------------------------------+
| Hardware threads per core | 2                                                     |
+---------------------------+-------------------------------------------------------+
| Hardware threads per node | 24 x 2 = 48                                           |
+---------------------------+-------------------------------------------------------+
| Clock rate                | 2.3 GHz nominal                                       |
+---------------------------+-------------------------------------------------------+
| RAM                       | 64 GB  DDR4                                           |
+---------------------------+-------------------------------------------------------+
| Local storage             | 0 GB - diskless                                       |
+---------------------------+-------------------------------------------------------+

