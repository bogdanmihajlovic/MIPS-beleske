PROGRAM = program
BUILD_DIR = build

SRC = source
INCLUDE = include

SOURCE_S_LIST = \
$(SRC)/startup_code.s

SOURCE_C_LIST = \
$(SRC)/main.c \
$(SRC)/systick.c

OBJECT_LIST =
OBJECT_LIST += $(addprefix $(BUILD_DIR)/, $(notdir $(SOURCE_S_LIST:.s=.o)))
OBJECT_LIST += $(addprefix $(BUILD_DIR)/, $(notdir $(SOURCE_C_LIST:.c=.o)))

HX = arm-none-eabi-objcopy.exe -O ihex
CC = arm-none-eabi-gcc.exe -c
AS = arm-none-eabi-gcc.exe -c -x assembler
LD = arm-none-eabi-ld.exe

LINKER_SCRIPT = linker_script.ld 

FLAGS_C = 
FLAGS_C += -mcpu=cortex-m3 -mthumb
FLAGS_C += -MMD -MP 
FLAGS_C += -I$(INCLUDE)

FLAGS_S = 
FLAGS_S += -mcpu=cortex-m3 -mthumb

vpath %.s $(sort $(dir $(SOURCE_S_LIST)))
vpath %.c $(sort $(dir $(SOURCE_C_LIST)))

all : $(BUILD_DIR)/$(PROGRAM).elf $(BUILD_DIR)/$(PROGRAM).hex

$(BUILD_DIR)/$(PROGRAM).hex : $(BUILD_DIR)/$(PROGRAM).elf
	$(HX) $(<) $(@)

$(BUILD_DIR)/$(PROGRAM).elf : $(OBJECT_LIST) makefile
	$(LD) -T $(LINKER_SCRIPT) -o $(@) $(OBJECT_LIST)

$(BUILD_DIR)/%.o : %.s makefile | $(BUILD_DIR)
	$(AS) $(FLAGS_S) -o $(@) $(<)
	
$(BUILD_DIR)/%.o : %.c makefile | $(BUILD_DIR)
	$(CC) $(FLAGS_C) -o $(@) $(<)

$(BUILD_DIR) :
	mkdir $(@)

clean:
	rm -rf $(BUILD_DIR)

-include $(wildcard $(BUILD_DIR)/*.d)
