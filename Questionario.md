# Questionário Sistemas Embarcados I

## 1. Explique brevemente o que é compilação cruzada (***cross-compiling***) e para que ela serve.
Cross-compilation é o processo onde utilizamos um computador com determinado sistema operacional para desenvolver softwares para sistemas embarcados. A máquina em que fazemos o desenvolvimento é o HOST e o dispositivo que irá executar o binário é o target. Exemplificando: Desenvolvemos a aplicação em um computador com Sistema Operacional Linux e o dispositivo que executa o binário será o STM32, é usamos o stlink para fazer a comunicação entre os dois.
## 2. O que é um código de inicialização ou ***startup*** e qual sua finalidade?
Quando um arquivo executável é carregado na memória, existe uma rotina intermediária que executa algumas tarefas antes de chegarem na função principal main(), isso acontece no arquivo de inicialização ou startup. Alguns exemplos de tarefas executadas são: configuração do hardware ( periféricos, registradores, e outros), configuração do ambiente de execução ( inicializando pilhas, definindo vetores de interrupção, e outros), inicialização do sistema operacional, carregamento do software de aplicação, diagnósticos iniciais e manuseios de erros.

## 3. Sobre o utilitário **make** e o arquivo **Makefile responda**:

#### (a) Explique com suas palavras o que é e para que serve o **Makefile**.
O Makefile é um arquivo que contém instruções para utilização de programas e bibliotecas que serão necessárias para execução de um programa em C com os parâmetros que desejamos.
#### (b) Descreva brevemente o processo realizado pelo utilitário **make** para compilar um programa.
O utilitário make usa o arquivo (Makefile) para determinar quais arquivos precisam ser compilados e como compilá-los. Ele verifica quais arquivos precisam ser compilados, verifica a data de modificação dos arquivos e determina os arquivos que precisam ser compilados novamente, executa os comandos de compilação especificados no Makefile e exibe mensagens de erro caso ocorrer algum problema de compilação.
#### (c) Qual é a sintaxe utilizada para criar um novo **target**?
targets: prerequisites
	
 recipe

Na prática, o target é o arquivo objeto que desejamos criar, e o prerequisites é o arquivo que dependemos para criar nosso arquivo objeto. Já o recipe é exatamente a linha de comando que deve ser utilizado para gerar o arquivo.

#### (d) Como são definidas as dependências de um **target**, para que elas são utilizadas?
all: startup.o main.o

Utilizamos o “all” como um target e colocamos como dependências todos os arquivos objetos que desejamos gerar, que no caso do exemplo acima é o startup.o e main.o. Elas são utilizadas quando queremos executar todos os targets presentes no nosso Makefile.

#### (e) O que são as regras do **Makefile**, qual a diferença entre regras implícitas e explícitas?

Uma regra informa ao make duas coisas: quando um target está desatualizado e como fazer para atualizá-lo.
Regra implícita: diz quando e como refazer uma classe de arquivos com base em seus nomes. Ele descreve como um alvo pode depender de um arquivo com um nome semelhante ao alvo e fornece uma receita para criar ou atualizar este alvo.
Regra explícita: diz quando e como refazer um ou mais aquivos, chamados de alvos da regra (rules's targets). Ela lista os arquivos dos quais os alvos (targets) dependem, chamados de pré-requisitos do alvo. Também pode fornecer instruções ou uma receita para criar ou atualizar os alvos.

## 4. Sobre a arquitetura **ARM Cortex-M** responda:

### (a) Explique o conjunto de instruções ***Thumb*** e suas principais vantagens na arquitetura ARM. Como o conjunto de instruções ***Thumb*** opera em conjunto com o conjunto de instruções ARM?
Thumb é uma extensão do conjunto de instruções do processador ARM. Ele foi originalmente desenvolvido para proporcionar um melhor desempenho em termos de consumo de energia e tamanho do código em sistemas embarcados, principalmente em sistemas com restrição de memória.
O processador pode executar tanto as instruções Thumb quanto às instruções ARM, pois eles operam em conjunto. Quando o processador está em modo Thumb, ele executa apenas instruções de 16 bits de tamanho fixo, já as instruções do modo ARM são de 32 bits. Isso permite que o processador economize espaço de memória e melhore o seu desempenho em algumas situações, já que para instruções mais complexas ou específicas, é necessário usar as do ARM.
Eles trabalham em “modo misto”, isto significa que os processadores ARM podem executar tanto instruções ARM quanto Thumb.

### (b) Explique as diferenças entre as arquiteturas ***ARM Load/Store*** e ***Register/Register***.
Arquitetura Load/Store - Operações de carga e armazenamento são realizadas, movendo dados entre a memória e os registradores do processador. Requer instruções separadas para acessar a memória e manipular os dados.
Arquitetura Register/Register - Todas as operações são realizadas diretamente entre registradores do processador, sem necessidade de acessar  memória diretamente. A memória é acessada  apenas quando é necessário carregar ou armazenar dados. Permite operações diretas entre registradores, reduzindo a necessidade de acesso à memória e potencialmente melhorando o desempenho do código.

### (c) Os processadores **ARM Cortex-M** oferecem diversos recursos que podem ser explorados por sistemas baseados em **RTOS** (***Real Time Operating Systems***). Por exemplo, a separação da execução do código em níveis de acesso e diferentes modos de operação. Explique detalhadamente como funciona os níveis de acesso de execução de código e os modos de operação nos processadores **ARM Cortex-M**.

### (d) Explique como os processadores ARM tratam as exceções e as interrupções. Quais são os diferentes tipos de exceção e como elas são priorizadas? Descreva a estratégia de **group priority** e **sub-priority** presente nesse processo.

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
