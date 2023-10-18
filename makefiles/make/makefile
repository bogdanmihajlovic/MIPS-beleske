PROGRAM = program
BUILD_DIR = build
DEBUG_ENABLED = 1

INCLUDE = include
SRC = source

LD = arm-none-eabi-ld.exe
HX = arm-none-eabi-objcopy.exe -O ihex
CC = arm-none-eabi-gcc.exe -c -mcpu=cortex-m3 -mthumb -mlong-calls -MMD -MP -I$(INCLUDE)
AS = arm-none-eabi-gcc.exe -c -mcpu=cortex-m3 -mthumb -x assembler

FLAGS_DEBUG = -g -gdwarf-2 -fdebug-prefix-map==../

ifeq ($(DEBUG_ENABLED), 1)
CC += $(FLAGS_DEBUG)
endif

ifeq ($(DEBUG_ENABLED), 1)
AS += $(FLAGS_DEBUG)
endif

LD_SCRIPT = linker_script.ld

SRC_LIST_S = $(SRC)/startup_code.s

SRC_LIST_C = $(SRC)/main.c \
$(SRC)/systick.c

OBJECT_LIST = 
OBJECT_LIST += $(addprefix $(BUILD_DIR)/, $(notdir $(SRC_LIST_S:.s=.o)))
OBJECT_LIST += $(addprefix $(BUILD_DIR)/, $(notdir $(SRC_LIST_C:.c=.o)))

vpath %.c $(SRC)
vpath %.s $(SRC)

all : $(BUILD_DIR)/$(PROGRAM).elf $(BUILD_DIR)/$(PROGRAM).hex

$(BUILD_DIR)/$(PROGRAM).hex : $(BUILD_DIR)/$(PROGRAM).elf
	$(HX) $(<) $(@)

$(BUILD_DIR)/$(PROGRAM).elf: $(OBJECT_LIST) makefile
	$(LD) -T $(LD_SCRIPT) -o $(@) $(OBJECT_LIST)

$(BUILD_DIR)/%.o : %.s makefile | $(BUILD_DIR)
	$(AS) -o $(@) $(<)
	
$(BUILD_DIR)/%.o : %.c makefile | $(BUILD_DIR)
	$(CC) -o $(@) $(<)
	

$(BUILD_DIR):
	mkdir $(@)

clean :
	rm -rf $(BUILD_DIR)

-include $(wildcard $(BUILD_DIR)/*.d)
