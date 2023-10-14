>1. Način

	SECTIONS
	{
		*ime_sekcije* *adresa_sekcije* :
		{
			*obj_fajlovi iz kojih uzimati sekcije* (*sekcije koje se uzimaju*)
		}
	}

	Primer:

	SECTIONS
	{
		prva 0x0000FF00 :
		{
			main.o(.text) /* umesto main.o '*' wildcard za sve fajlove iz komande */
		}
	}

>2. Način

	MEMORY
	{
		*ime_regiona* (rwx) : ORIGIN = *adresa*, LENGTH = *velicina*
	}
	SECTIONS
	{
		*ime_sekcije* :
		{
			*obj_fajlovi*(*sekcije*)
		} > *ime_regiona*
	}
	
	Primer:
	
	MEMORY
	{
		PRVI_REGION (rwx) : ORIGIN = 0x0000FF00, LENGTH = 32k
	}
	SECTIONS
	{
		kod :
		{
			*(.text)
		} > PRVI_REGION
	}

>3. Način (definisanje VMA i LMA adrese)

	MEMORY
	{
		PRVI_REGION (rwx) : ORIGIN = 0x0000FF00, LENGTH = 32k
		DRUGI_REGION (rwx) : ORIGIN = 0x76547645, LENGTH = 32k
	}
	SECTIONS
	{
		podaci :
		{
			*(.data)
		} > PRVI_REGION AT>DRUGI_REGION
	}



 
>Način pokretanja linker skripte:

	arm-none-eabi-ld.exe --script=*ime_skripte* *ulazni_obj_fajlovi* -o *name*.elf
