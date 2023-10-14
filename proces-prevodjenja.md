>1. Korak
   + Od **main.c** treba napraviti **main.o**
   + Od **main.o** => **main.elf**
   + Od **main.elf** => **main.hex**

>2. Kako se dolazi od **main.c** do **main.o**
+ main.c =(pretprocesiranje)=> main.i
+ main.i =(prevodenje)=> main.s
+ main.s =(asembliranje)=> main.o

>3. Kako se dolazi od **main.o** do **main.elf**

+ main.o =(linkovanje)=> main.elf

>4. Kako se dolazi od main.elf do main.hex
+ main.elf =(objcopy)=> main.hex

>5. Komande:
+ main.c => main.i
  + `arm-none-eabi-gcc.exe -E -o main.i main.c`
+ main.i => main.s
  + `arm-none-eabi-gcc.exe -S -mcpu=cortex-m3 -mthumb -o main.s main.i`
+ main.s => main.o
  + `arm-none-eabi-gcc.exe -c -mcpu=cortex-m3 -mthumb -o main.o main.i`
+ main.o => main.elf
  + `arm-none-eabi-ld.exe --script=*script-name* -o main.elf main.o`
+ main.elf => main.hex
  + `arm-none-eabi-objcopy.exe -O ihex main.elf main.hex`
+ main.c => main.o
  + `arm-none-eabi-gcc.exe -c -mcpu=cortex-m3 -mthumb -o main.o main.c`
+ Citati obj fajl
  + `arm-none-eabi-objdump.exe -thsd main.o`
  + `arm-none-eabi-objdump.exe -thsd main.elf`

>6. Citanje obj fajla
+ arm-none-eabi-objdump.exe -thsd main.o
+ arm-none-eabi-objdump.exe -thsd main.elf
	
	 



