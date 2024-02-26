CC = arm-none-eabi-gcc                                          #ferramenta do toolchain
RM = rm -rf                                                     #ferramenta do toolchain
OBJDIR = build                                                  # Diretorios arquivos objeto serao salvos
SRCS = main.c startup.c                                         #Arquivos a serem compilados 
CFLAGS = -g -mcpu=cortex-m4 -mthumb -Wall -O0                   #Flags do compilador 

 #Gera uma lista de arquivos objeto utilizando os arquivos fonte
OBJS = $(patsubst %, %.o, $(basename $(SRCS)))

# Cria diretorios onde serao armazenados arquivos objeto
$(shell mkdir -p $(dir $(OBJS)) > /dev/null)

all: $(OBJS)

$(OBJDIR)/%.o: %.c
	$(CC) -c $(CFLAGS) $< -o $@

clean:
	$(RM) $(OBJDIR)

