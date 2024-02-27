CC = arm-none-eabi-gcc
RM = rm -rf 

OBJDIR = build

CFLAGS = -g -mcpu=cortex-m4 -mthumb -Wall -O0
SRCS = src/main.o scr/startup.o
DEPDIR = .deps

OBJS = $(pastsubst %, $(OBJDIR), $(basename $(SRCS)))

all: $(OBJS)

$(OBJDIR): %.c
	$(CC) -c $(CFLAGS) $< -o $@

clean:
	$(RM) $(OBJS) $(DEPDIR)