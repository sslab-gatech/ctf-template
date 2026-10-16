CC ?= gcc
CFLAGS ?= -std=gnu99 -O0 -g
LDFLAGS ?=
LIBS ?=

# 32b or 64b
CFLAGS += -m32
# CFLAGS += -m64

# supress warning
CFLAGS += -Wno-format-security

# enable executable stack
# CFLAGS += -z execstack

# enable SSP
CFLAGS += -fstack-protector

# disable SSP
# CFLAGS += -fno-stack-protector

# enable PIE
# CFLAGS += -pie -fPIE

# disable PIE
CFLAGS += -no-pie

# disable CET
CFLAGS += -fcf-protection=none

ALL := target

.PHONY: all
all: $(ALL)

target: fmtstr.c
	$(CC) $(CFLAGS) -o $@ $< $(LDFLAGS) $(LIBS)
	pwn checksec $@

.PHONY: clean
clean:
	$(RM) -f $(ALL)
