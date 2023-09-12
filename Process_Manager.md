### Process Manager

**Llojet e proceseve:**

1. Parent process
-ekzekuton  fork() syscall

2. Child process
-krijohet nga nje parent process

3. Orphan Process
-vazhdon te ekzekutohet edhe pse proseci prind eshte terminuar ose ka perfunduar. Nuk kthehet ne zombie process

4. Daemon Process
-krijohet nga nje child process dhe pastaj ben exit

5. Zombie Process
-ekziston ne  process table edhe pse eshte e terminuar 

**Menaxhimi i memories**
 
Per te verifikuar gjendjen e saj perdorim komanden:

`$ free -m`    

> opsioni -m shfaq vleren ne megabytes

__buff/cache__ - tregon sa memorie po perdorim ne megabytes

__available__ - sa memorie kemi te disponueshme

Rrjeshti i dyte eshte swap. e cila ndodh kur memoria behet 'crowded'


**Monitorimi i System Health me iostat dhe lsof**

__iostat__ - shfaq raportin e CPU utilization 

`$ iostat -c`

Nese sistemi eshte 'busy' ath __%iowait__ do te rritet.
Kjo nenkupton qe serveri eshte duke transferuar ose kopjuar nje vlere te madhe files
Nepermjete kesaj komande mund te kontrollojme operacionet e read dhe write  per te patur nje info te plote se cfare nuk shkon 

Komanda `lsof` na shfaq files e hapur
Nese e shoqerojme me emrin e file si path i plote mund te gjejme se nga cili proces ose service po perdoret ai file

**Perllogaritja e system load**

__System load__ eshte sasia e procesimit per sistemin qe eshte aktualisht duke punuar(nuk eshte menyra perfekte per te matur performancen e sistemit por te jep disa evidenca)

**Actual Load = Total Load (uptime) / No. of CPUs**

Per te gjetur uptime perdorim komanden:

`$uptime`

Per te pare server load per 1, 5 dhe 15 min perdorim komanden:

`$top`
 
Load mesatar eshte 0.00 min i pare , 0.01 tek min i 5 dhe 0.05 tek min i 15

> Kur load rritet, sistemi vendos ne rradh procesoret dhe nese ka disa core procesori, sistemi e shperndan load ne menyre te barabarte per cdo cores ne menyre qe te balancohet puna.
> Mund te themi se vlera mesatare me e pertatshme per load eshte 1.
> Kjo nuk nenkupton qe rritja e saj eshte gjithmone problem por nese vlera qendron per nje kohe te gjate e larte, ath eshte problem. 

**Monitorimi i disk I/O me iotop**

Sistemi fillon te behet i ngadalt si rezultat i nivelit te larte te aktivitetit ne disk, keshtu qe eshte e nevojshme te monitorojme aktivitetin e disk(te indetifikosh se kush proces se user e shkaktojne keta aktivitet ne disk)

Per kete na ndihmone komanda: `iotop`

- monitoron ne realtime
- mund ta install

`$ apt install iotop`

- nese e ekzekuton komanden pa opsion ath te liston te gjitha proceset 
- nese e liston me -o liston proceset qe shkaktojne aktivitetin ne disk

`$ iotop -o`
 
**Komanda ps** 

Liston te gjitja proceset qe jane duke u ekzekutuar 

`$ ps aux`
 
- ps ~ process status 
- a ~ tregon informacion rreth te gjithe proceseve ne sistem, jo thjesht ato te lidhura me procesin aktual 
- u ~  tregon informacion te detajuar rreth cdo procesi ne nje user-oriented format
- x ~ tregon info rreth cdo procesi qe nuk eshte i bashkengjitur ne nje termina 


**Menaxhimi i services nepermjet systemd**

Nepermjet komandes systemctl ne mund te start, stop, check statusin e services.  
`$ systemctl status <service_name>`

`$ systemctl stop <service_name>`

`$ systemctl start <service_name>`

Ne vend qe te perdorim komanden `chkconfig`  per te bere enable ose disable nje service mund te perdoret komanda `systemctl`.

`$ systemctl enable <service_name>`

`$ systemctl disable <service_name>`

Per te pare proceset qe i perkasin nje servic specifik shikon komanden:

`$ systemd-cgtop`

Mund te nxjerresh nje list e permbajtjes se service:
 
`systemd-cgls`

**pgrep dhe systemctl**

Per te marr process ID perdorim komandat:

**1. pgrep**

`$ pgrep servicename`

-nese shfq me shume info se thjeshte process ID atehere PID me vleren me te vogel eshte parent process ID

**2. systemctl**

`$ systemctl status <service_name>`

**Proceset nice dhe renice**
 
> Ne linux `nice` eshte edhe command-line utility edhe koncept qe lidhet me prioritetin e proceseve.
> Nje vlere e larte e `nice` tregon prioritet i ulet per procesin ne lidhje me CPU-ne.
> `nice` range eshte nga -20 ne +19
> Komanda `nice` vendos vleren per proces ne kohen e krijimit kurse komanda `renice` e rregullon vleren me vone.
> Nje user i thjesht  mund te rriti vleren e `nice` (prioritet i ulet ) por nuk mund ta uli ate (prioritet i larte ), kurse root user i bene te dyja.
 
`$ nice -n 5 ./myscript`

`$sudo renice -5  2213`




**Kill signal**

Komanda kill perdoret per te terminuar service ose application

__Metoda safe kill__

`$kill process ID`
 
__Metoda hang up__
 
`$kill -1 process ID`

__Metoda forced kill__

`$kill -9 process ID`

> -9 nenkupton SIGKILL 

`$kill -9 serviceName`

Dhe mund te perdoresh komanden `pgrep` te sigurohesh qe te gjithe proceset qe i perkasin atit service jane killed

`pgrep serviceName`