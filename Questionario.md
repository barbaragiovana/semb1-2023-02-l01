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
       comandos

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
- Synchronous exceptions:
- Reset (0): Reset do processador.
- Undefined instruction (1): Instrução indefinida.
- Software interrupt (2): Interrupção de software.
- Prefetch abort (3): Aborto de pré-busca.
- Data abort (4): Aborto de dados.
- Reserved (5-10): Reservados.
- IRQ (11): Interrupção externa.
- FIQ (12): Interrupção rápida.
- Asynchronous exceptions:
- SError (13): Erro de sistema.
- Interrupt (14): Interrupção.
- Trap (15): Trap.

Interrupções:
- IRQ (11): Interrupção externa.
- FIQ (12): Interrupção rápida.

Group Priority (Prioridade de Grupo):

As exceções e interrupções são agrupadas em diferentes níveis de prioridade.
Um nível de prioridade mais baixo indica uma prioridade mais alta, ou seja, as exceções e interrupções com menor valor de prioridade são tratadas primeiro.

Sub-Priority (Subprioridade):

Em alguns sistemas, as exceções e interrupções dentro do mesmo grupo de prioridade podem ser priorizadas ainda mais usando subprioridades.
Isso permite que exceções e interrupções de alta prioridade dentro do mesmo grupo sejam tratadas primeiro.

### (e) Qual a diferença entre os registradores **CPSR** (***Current Program Status Register***) e **SPSR** (***Saved Program Status Register***)?

CPSR (Current Program Status Register):

O CPSR armazena o estado atual do processador enquanto o código está sendo executado no modo de usuário (User Mode) ou no modo privilegiado (Privileged Mode).Ele registra informações como o estado da condição de execução (flags), o modo de operação atual, se a interrupção está habilitada ou desabilitada, entre outras informações de status do processador, ele pode ser acessado e modificado durante a execução do código usando instruções específicas (como instruções de comparação, adição ou subtração), permitindo que o software controle o comportamento do processador, E também é usado para determinar o estado do processador durante a execução normal do código e para realizar operações condicionais com base nas flags de status.

SPSR (Saved Program Status Register):

O SPSR é usado para armazenar temporariamente o estado do processador quando uma exceção ocorre e o controle é transferido para um tratador de exceção.Ele armazena o estado do processador no momento em que a exceção ocorre, permitindo que o tratador de exceção retome a execução do código após lidar com a exceção,Quando uma exceção ocorre, o CPSR atual é copiado para o SPSR correspondente antes que o processador mude para o modo de exceção,isso permite que o tratador de exceção preserve o estado do processador e retome a execução do código original após o tratamento da exceção.Após a conclusão do tratamento de exceção, o conteúdo do SPSR é copiado de volta para o CPSR para restaurar o estado do processador anterior à exceção, isso permite que a execução do programa continue de onde parou, mantendo o estado consistente do processador.

### (f) Qual a finalidade do **LR** (***Link Register***)?

O registrador LR (Link Register) é usado para armazenar o endereço de retorno de uma sub-rotina ou chamada de função, permitindo que o programa retorne ao ponto de onde a chamada foi feita após a execução da sub-rotina.

### (g) Qual o propósito do Program Status Register (PSR) nos processadores ARM?

O PSR tem como objetivo principal armazenar informações sobre o estado atual do processador, ele é crucial para controlar o fluxo de execução do programa e para lidar com exceções de forma eficaz.

### (h) O que é a tabela de vetores de interrupção?

A tabela de vetores de interrupção é uma estrutura de dados usada em sistemas embarcados para direcionar o processador para o código apropriado quando ocorre uma interrupção. Ela mapeia cada tipo de interrupção para o endereço de memória da função que lida com essa interrupção. Quando uma interrupção ocorre, o processador usa essa tabela para encontrar a função correspondente e executá-la. Essa abordagem garante um tratamento eficiente e organizado das interrupções no sistema.
Em nosso sistema criamos um array e declaramos cada endereço de memória correspondente ao seu papel de acordo com o datasheet da placa, fazemos isso pois caso seja necessario executar a interrupção, isto funcionará de forma adquada no nosso projeto.

### (i) Qual a finalidade do NVIC (**Nested Vectored Interrupt Controller**) nos microcontroladores ARM e como ele pode ser utilizado em aplicações de tempo real?

O NVIC (Nested Vectored Interrupt Controller) é um componente essencial nos microcontroladores ARM, especialmente na linha Cortex-M, que gerencia interrupções de maneira eficiente e flexível. Sua finalidade é permitir o tratamento de múltiplas interrupções de forma organizada e escalonada, o que é fundamental em aplicações de tempo real, ele oferece recursos como priorização, encadeamento e controle de estado de interrupção, permitindo que os sistemas embarcados atendam às demandas de tempo real de forma confiável.

### (j) Em modo de execução normal, o Cortex-M pode fazer uma chamada de função usando a instrução **BL**, que muda o **PC** para o endereço de destino e salva o ponto de execução atual no registador **LR**. Ao final da função, é possível recuperar esse contexto usando uma instrução **BX LR**, por exemplo, que atualiza o **PC** para o ponto anterior. No entanto, quando acontece uma interrupção, o **LR** é preenchido com um valor completamente  diferente,  chamado  de  **EXC_RETURN**.  Explique  o  funcionamento  desse  mecanismo  e especifique como o **Cortex-M** consegue fazer o retorno da interrupção. 

O mecanismo de tratamento de interrupções no Cortex-M envolve o uso do registrador LR (Link Register) de maneira especial. Quando uma interrupção ocorre, o Cortex-M automaticamente preserva o contexto da execução atual, incluindo o valor do registrador LR, antes de transferir o controle para o tratador de interrupção. Isso é essencial para garantir que, após o tratamento da interrupção, o programa possa retomar a execução no ponto onde foi interrompido.

O valor especial preenchido no registrador LR durante uma interrupção é chamado de "EXC_RETURN". Ele contém informações específicas sobre o contexto de execução antes da interrupção. O formato do valor EXC_RETURN varia dependendo do tipo de exceção que ocorreu e do estado do processador no momento da interrupção.

Quando o tratador de interrupção está prestes a retornar ao código interrompido, ele usa o valor EXC_RETURN no registrador LR para restaurar o contexto de execução anterior à interrupção. O Cortex-M interpreta o valor EXC_RETURN para determinar como restaurar corretamente o estado do processador e retomar a execução do programa.

Por exemplo, se a interrupção foi tratada enquanto o processador estava em um modo privilegiado (como o modo Handler), o valor EXC_RETURN informará ao Cortex-M para retornar ao modo anteriormente usado antes da interrupção. Além disso, o valor EXC_RETURN pode conter informações sobre se o tratamento da interrupção foi realizado com sucesso, se houve uma troca de pilha, etc.

Em resumo, o valor EXC_RETURN preenchido no registrador LR durante uma interrupção fornece informações essenciais para que o Cortex-M possa restaurar corretamente o contexto de execução anterior à interrupção e retomar a execução do programa no ponto onde foi interrompido. Isso é uma parte crucial do mecanismo de tratamento de interrupções nos microcontroladores Cortex-M.

### (k) Qual  a  diferença  no  salvamento  de  contexto,  durante  a  chegada  de  uma  interrupção,  entre  os processadores Cortex-M3 e Cortex M4F (com ponto flutuante)? Descreva em termos de tempo e também de uso da pilha. Explique também o que é ***lazy stack*** e como ele é configurado. 

O salvamento de contexto durante a chegada de uma interrupção nos processadores Cortex-M3 e Cortex-M4F difere principalmente devido à presença de registros de ponto flutuante no Cortex-M4F. Isso afeta tanto o tempo de resposta da interrupção quanto o uso da pilha. Além disso, o conceito de "lazy stack" também é relevante para o gerenciamento eficiente da pilha durante as interrupções.

Cortex-M3:

- Tempo de Resposta: No Cortex-M3, o salvamento de contexto durante uma interrupção é realizado de maneira mais simples, pois não há registros de ponto flutuante a serem preservados.
- Uso da Pilha: Durante uma interrupção no Cortex-M3, o contexto do processador é salvo na pilha principal. Isso inclui os registradores de propósito geral (incluindo o LR) e os registradores especiais relacionados à interrupção, como o registrador de estado PRIMASK ou BASEPRI, se aplicável.
- Lazy Stack: No Cortex-M3, não há o conceito de "lazy stack". Isso significa que toda a informação do contexto é imediatamente empilhada na entrada da rotina de tratamento de interrupção.

Cortex-M4F:

- Tempo de Resposta: No Cortex-M4F, o salvamento de contexto pode ser um pouco mais lento devido à necessidade de preservar também os registros de ponto flutuante.
- Uso da Pilha: Durante uma interrupção no Cortex-M4F, além dos registradores de propósito geral, os registradores de ponto flutuante (se utilizados) também precisam ser preservados. Isso resulta em uma quantidade maior de dados a serem empilhados na pilha.
- Lazy Stack: No Cortex-M4F, o conceito de "lazy stack" pode ser usado para otimizar o gerenciamento da pilha durante interrupções. Com o lazy stack ativado, apenas os registradores de propósito geral são inicialmente empilhados quando uma interrupção ocorre. Os registradores de ponto flutuante só são salvos na pilha quando são realmente usados pelo tratador de interrupção. Isso reduz a sobrecarga de salvar e restaurar todos os registradores de ponto flutuante a cada interrupção, o que pode melhorar significativamente o tempo de resposta em aplicações que não usam rotineiramente cálculos de ponto flutuante.

Configuração do Lazy Stack:

O lazy stack é configurado através do bit de controle LazyStacking no registrador de configuração de exceções (EXC_RETURN).Quando ativado, o processador só empilhará os registradores de propósito geral automaticamente quando uma exceção ocorrer, os registradores de ponto flutuante serão salvos e restaurados conforme necessário pelo tratador de interrupção. Essa configuração pode ser útil em aplicações que visam minimizar o tempo de resposta de interrupções, especialmente em cenários onde os registros de ponto flutuante não são frequentemente utilizados.

A principal diferença no salvamento de contexto durante a chegada de uma interrupção entre os processadores Cortex-M3 e Cortex-M4F está relacionada à presença de registros de ponto flutuante no Cortex-M4F. Isso afeta tanto o tempo de resposta da interrupção quanto o uso da pilha. Além disso, o conceito de "lazy stack" pode ser utilizado no Cortex-M4F para otimizar o gerenciamento da pilha durante as interrupções, reduzindo assim a sobrecarga e melhorando o tempo de resposta.

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
