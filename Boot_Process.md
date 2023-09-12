## Boot Process

Pasi power on kompjuterin:

### 1.Ekzekutohet BIOS/UEFI firmware 
> BIOS/UEFI performon "hardware check" (POST)
> - sigurohet qe cdo komponent hardware eshte funksional(CPU, memory,storage) 
> - identifikon "boot device" qe permban OS (HDD, SSD, USB Drive) 

### 2.Ekzekutimi i fazes se pare te boot loader

> BIOS pasi identifikon "boot device", ngarkon sektorin e pare te tij ne memorie(RAM). Sektori i pare permban MBR. 
> MBR- Master Boot Record: kur ngarkohet ne RAM ekzekutohen ne nje kod te vogel qe starton fazen e pare te boot loader dhe faza e pare starton pastaj fazen e dyte. 
> llojet e boot loaders jane: 
>                           - GRUB 
>                           - LILO

### 3.Boot loader lexon file e konfigurimit per te percaktuar cilin OS dhe kernel do te load dhe pastaj e ngarkon ate ne RAM. 

### 4.Pasi kernel load ne RAM starton procesi i pare init/system.d me PID1

> system.d:
>         - menaxhon servicet(units)
>         - pergjegjese per te startuar gjithe user-space services dhe processes 

### 5.Runlevels
1. init0 ~ Shutdown
2. init1 ~ Single user mode(safemode)
3. init2 ~ Multi user mode, UI without networking 
4. init3 ~ Multi user mode, UI with network
5. init4 ~ Mund te personalizohet
6. init5 ~ User interface me GUI
7. init7 ~ Reboot 