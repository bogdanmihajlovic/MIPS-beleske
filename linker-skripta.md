1. Nacin
SECTIONS
{
	*ime_sekcije* *adresa_sekcije* :
	 {
	 	*obj_fajlovi iz kojih uzimati sekcije*(*sekcije koje se uzimaju*)
	 }
}

primer:
SECTIONS
{
	prva 0x0000FF00 :
	{
		main.o(.text) /* umesto main.o '*' wildcard za sve fajlove iz komande*/
	}
}

2. Nacin
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

primer:

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


3. Nacin (definisanje VMA i LMA adrese)

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


Nacin pokretanje linker skripte:

arm-none-eabi-ld.exe --script=*ime_skripte* *ulazni_obj_fajlovi* -o *name*.elf


