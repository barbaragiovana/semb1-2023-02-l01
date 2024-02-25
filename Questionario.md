# Questionário Sistemas Embarcados I

## 1. Explique brevemente o que é compilação cruzada (***cross-compiling***) e para que ela serve.
 Cross-compiling é um processo no qual você compila um programa em um sistema diferente daquele em que será executado. Como estamos realizando nessa matéria utilizando o linux para poder efetuar a compilação da Arquiterura ARM.

## 2. O que é um código de inicialização ou ***startup*** e qual sua finalidade?
 Um código de inicialização (Startup) é um código que é executado antes do inicio da execução do progama principal (main), sua finalidade é preparar o ambiente de execução do programa principal, no nosso caso o codigo startup serve para:
•	declaração e inicialização do Stack;
•	declaração e inicialização da Tabela de Vetores de Interrupção;
•	código do Reset Handler;
•	outros códigos Exception Handlers.
 O codigo de inicialização é crucial em sistemas embarcados onde é necessário um controle preciso sobre o ambiente de execução desde o início.

## 3. Sobre o utilitário **make** e o arquivo **Makefile responda**:

#### (a) Explique com suas palavras o que é e para que serve o **Makefile**.
 O arquivo Makefile é um arquivo de texto, composto por instruções criadas pelo programador sobre como compilar cada parte do codigo-fonte, quais arquivos dependem de outros arquivos e como produzir os executaveis finais. A sua principal finalidade é automatizar o processo de compilação.

#### (b) Descreva brevemente o processo realizado pelo utilitário **make** para compilar um programa.
 O processo realizado pelo make para compilar um programa segue mais ou menos os seguintes passos:
- Análise do Makefile
- Determinação das dependências
- Execução das regras
- Verificação das datas de modificação
- Execução dos comandos de compilação
- Geração dos arquivos alvo
- Finalização
Esses passos garantem que apenas os arquivos necessários sejam compilados e que o processo de compilação seja executado de forma eficiente e automatizada.
#### (c) Qual é a sintaxe utilizada para criar um novo **target**?
alvo: dependências
(tab) comandos
 - alvo: é o nome do alvo que você deseja criar
 - dependências: são os arquivos que o alvo depende
 - comandos: são os comandos que o make deve executar para construir o alvo.

#### (d) Como são definidas as dependências de um **target**, para que elas são utilizadas?
As dependencias são definidas logo após o nome do target, separadas por espaços. Essas dependências indicam os arquivos ou outros targets que devem ser construídos antes que o target em questão possa ser construído. As dependências são usadas pelo make para determinar se o target precisa ser reconstruído e, em caso afirmativo, em qual ordem.

    programa: arquivo1.c arquivo2.c
         gcc -o programa arquivo1.c arquivo2.c
  
#### (e) O que são as regras do **Makefile**, qual a diferença entre regras implícitas e explícitas?
As regras em um arquivo Makefile são instruções que o make segue para construir um alvo específico. Cada regra consiste em um alvo, suas dependências e os comandos necessários para construir o alvo a partir das dependências.
- regra explícita: diz quando e como refazer um ou mais aquivos, chamados de alvos da regra (rules's targets). Ela lista os arquivos dos quais os alvos (targets) dependem, chamados de pré-requisitos do alvo. Também pode fornecer instruções ou uma receita para criar ou atualizar os alvos.
- regra implícita: diz quando e como refazer uma classe de arquivos com base em seus nomes. Ele descreve como um alvo pode depender de um arquivo com um nome semelhante ao alvo e fornece uma receita para criar ou atualizar este alvo.

## 4. Sobre a arquitetura **ARM Cortex-M** responda:

### (a) Explique o conjunto de instruções ***Thumb*** e suas principais vantagens na arquitetura ARM. Como o conjunto de instruções ***Thumb*** opera em conjunto com o conjunto de instruções ARM?
O conjunto de instruções Thumb é um conjunto de instruções de 16 bits usado em processadores ARM. Foi introduzido em 1994 com o objetivo de reduzir o tamanho do código e melhorar o desempenho em dispositivos embarcados com memória limitada.
Vantagens de usar o conjunto de instruções Thumb:
- Código menor: O código Thumb ocupa menos espaço na memória, o que pode ser importante para dispositivos embarcados com memória limitada.
- Maior desempenho: O código Thumb pode ser executado mais rapidamente do que o código ARM de 32 bits em alguns casos.
- Flexibilidade: Os programadores podem usar os dois conjuntos de instruções no mesmo código, o que oferece flexibilidade e otimização.
o conjunto de instruções Thumb opera em conjunto com o conjunto de instruções ARM, permitindo que os processadores ARM alternem dinamicamente entre os modos Thumb (para eficiência de código e economia de energia) e ARM (para alto desempenho) conforme necessário para diferentes aplicativos e cenários de uso.

### (b) Explique as diferenças entre as arquiteturas ***ARM Load/Store*** e ***Register/Register***.

Arquitetura Load/Store:
- Na arquitetura Load/Store, apenas instruções de carga (load) e armazenamento (store) podem acessar a memória.
- As instruções de manipulação de dados, como adição e subtração, operam apenas em registradores.
- Para acessar dados da memória, primeiro é necessário carregar os dados para um registrador usando uma instrução de carga (load).
- Depois de manipular os dados nos registradores, eles podem ser armazenados de volta na memória usando uma instrução de armazenamento (store).

Arquitetura Register/Register:
- Na arquitetura Register/Register, as operações de manipulação de dados podem ser realizadas diretamente entre registradores, sem a necessidade de acessar a memória.
- Registradores são usados tanto para operandos de entrada quanto de saída em operações aritméticas e lógicas.
- As operações de carga/armazenamento da memória são menos comuns e geralmente são usadas apenas para entrada e saída de dados do programa.
  
### (c) Os processadores **ARM Cortex-M** oferecem diversos recursos que podem ser explorados por sistemas baseados em **RTOS** (***Real Time Operating Systems***). Por exemplo, a separação da execução do código em níveis de acesso e diferentes modos de operação. Explique detalhadamente como funciona os níveis de acesso de execução de código e os modos de operação nos processadores **ARM Cortex-M**.

Os níveis de acesso de execução de código em processadores ARM Cortex-M referem-se à permissão de acesso para diferentes regiões de memória onde o código pode ser executado. Esses níveis são essenciais para garantir a segurança, a integridade e a eficiência do sistema. Existem principalmente dois tipos de níveis de acesso de execução de código em sistemas Cortex-M:

Execute-in-Place (XiP):

No modo Execute-in-Place (XiP), o código é executado diretamente da memória onde está armazenado, geralmente a memória de programa (flash).
Isso significa que o processador executa instruções diretamente da memória sem precisar carregá-las em outra área da memória.
A memória de programa geralmente é apenas leitura (ROM), garantindo que o código não seja modificado durante a execução.
Esse modo é comumente usado em sistemas embarcados, onde a memória flash é utilizada para armazenar o código do programa.

Execute-in-Place (DiP):

No modo Execute-in-Place (DiP), o código é copiado da memória de programa para a memória de dados (RAM) antes da execução.
Isso pode ser necessário em casos onde a memória de programa é mais lenta para execução direta ou quando há restrições de segurança que exigem a separação entre memória de programa e memória de dados.
O código é carregado na memória de dados temporariamente apenas para execução e pode ser descartado após o término da execução.

Funcionamento:

O processador Cortex-M é configurado para acessar as instruções de acordo com o tipo de acesso de execução de código definido para a região de memória onde o código está armazenado. No modo XiP, o processador busca as instruções diretamente da memória de programa.
No modo DiP, o processador copia as instruções da memória de programa para a memória de dados antes de executá-las.
A escolha entre XiP e DiP depende das necessidades do sistema, incluindo velocidade de execução, consumo de energia e requisitos de segurança.

### (d) Explique como os processadores ARM tratam as exceções e as interrupções. Quais são os diferentes tipos de exceção e como elas são priorizadas? Descreva a estratégia de **group priority** e **sub-priority** presente nesse processo.

Os processadores ARM têm um mecanismo dedicado para tratar exceções e interrupções. Quando uma exceção ou interrupção ocorre, o processador suspende a execução do código atual e transfere o controle para um tratador de exceção específico. Esse tratador de exceção é uma rotina de software que lida com o evento específico que ocorreu.
As exceções e interrupções são priorizadas de acordo com sua importância e urgência. Os processadores ARM geralmente implementam uma estratégia de priorização baseada em níveis de prioridade, que podem incluir "group priority" (prioridade de grupo) e "sub-priority" (subprioridade).

Exceções:
Synchronous exceptions:
Reset (0): Reset do processador.
Undefined instruction (1): Instrução indefinida.
Software interrupt (2): Interrupção de software.
Prefetch abort (3): Aborto de pré-busca.
Data abort (4): Aborto de dados.
Reserved (5-10): Reservados.
IRQ (11): Interrupção externa.
FIQ (12): Interrupção rápida.
Asynchronous exceptions:
SError (13): Erro de sistema.
Interrupt (14): Interrupção.
Trap (15): Trap.

Interrupções:
IRQ (11): Interrupção externa.
FIQ (12): Interrupção rápida.

Group Priority (Prioridade de Grupo):

As exceções e interrupções são agrupadas em diferentes níveis de prioridade.
Um nível de prioridade mais baixo indica uma prioridade mais alta, ou seja, as exceções e interrupções com menor valor de prioridade são tratadas primeiro.

Sub-Priority (Subprioridade):

Em alguns sistemas, as exceções e interrupções dentro do mesmo grupo de prioridade podem ser priorizadas ainda mais usando subprioridades.
Isso permite que exceções e interrupções de alta prioridade dentro do mesmo grupo sejam tratadas primeiro.

### (e) Qual a diferença entre os registradores **CPSR** (***Current Program Status Register***) e **SPSR** (***Saved Program Status Register***)?

### (f) Qual a finalidade do **LR** (***Link Register***)?

### (g) Qual o propósito do Program Status Register (PSR) nos processadores ARM?

### (h) O que é a tabela de vetores de interrupção?

### (i) Qual a finalidade do NVIC (**Nested Vectored Interrupt Controller**) nos microcontroladores ARM e como ele pode ser utilizado em aplicações de tempo real?

### (j) Em modo de execução normal, o Cortex-M pode fazer uma chamada de função usando a instrução **BL**, que muda o **PC** para o endereço de destino e salva o ponto de execução atual no registador **LR**. Ao final da função, é possível recuperar esse contexto usando uma instrução **BX LR**, por exemplo, que atualiza o **PC** para o ponto anterior. No entanto, quando acontece uma interrupção, o **LR** é preenchido com um valor completamente  diferente,  chamado  de  **EXC_RETURN**.  Explique  o  funcionamento  desse  mecanismo  e especifique como o **Cortex-M** consegue fazer o retorno da interrupção. 

### (k) Qual  a  diferença  no  salvamento  de  contexto,  durante  a  chegada  de  uma  interrupção,  entre  os processadores Cortex-M3 e Cortex M4F (com ponto flutuante)? Descreva em termos de tempo e também de uso da pilha. Explique também o que é ***lazy stack*** e como ele é configurado. 


## Referências

### Básicas

[1] [STM32F411xC Datasheet](https://www.st.com/resource/en/datasheet/stm32f411ce.pdf)

[2] [RM0383 Reference Manual](https://www.st.com/resource/en/reference_manual/rm0383-stm32f411xce-advanced-armbased-32bit-mcus-stmicroelectronics.pdf)

[3] [Using the GNU Compiler Collection (GCC)](https://gcc.gnu.org/onlinedocs/gcc/index.html)

[4] [GNU Make](https://www.gnu.org/software/make/manual/html_node/index.html)

### Vídeos Microsoft Teams

[5] [05 - Introdução à arquitetura de computadores](https://web.microsoftstream.com/embed/channel/f6b3a0de-e6f3-4652-b2d5-f1164032498a?app=microsoftteams&sort=undefined&l=pt-br#)

[6] [06 - Arquitetura Cortex-M Parte 1/2](https://web.microsoftstream.com/embed/channel/f6b3a0de-e6f3-4652-b2d5-f1164032498a?app=microsoftteams&sort=undefined&l=pt-br#)

[7] [07 - Arquitetura Cortex-M Parte 2/2](https://web.microsoftstream.com/embed/channel/f6b3a0de-e6f3-4652-b2d5-f1164032498a?app=microsoftteams&sort=undefined&l=pt-br#)

[8] [08 - Microcontroladores STM32](https://web.microsoftstream.com/embed/channel/f6b3a0de-e6f3-4652-b2d5-f1164032498a?app=microsoftteams&sort=undefined&l=pt-br#)

[9] [10 - Introdução à arquitetura de computadores](https://web.microsoftstream.com/embed/channel/f6b3a0de-e6f3-4652-b2d5-f1164032498a?app=microsoftteams&sort=undefined&l=pt-br#)

### Material Suplementar

[5] [A General Overview of What Happens Before main()](https://embeddedartistry.com/blog/2019/04/08/a-general-overview-of-what-happens-before-main/)
 
[6] [Bare metal embedded lecture-1: Build process](https://youtu.be/qWqlkCLmZoE?si=mn5yDnJYudQ1PpZH)
 
[7] [Bare metal embedded lecture-2: Makefile and analyzing relocatable obj file](https://youtu.be/Bsq6P1B8JqI?si=yuNLPj3JQ-2IT1yo)
 
[8] [Bare metal embedded lecture-3: Writing MCU startup file from scratch](https://youtu.be/2Hm8eEHsgls?si=c27MpZ47ApiMSwHR)
 
[9] [Lecture 15: Booting Process](https://youtu.be/3brOzLJmeek?si=MsHRUEJP8zofjwJQ)
