# Hascat

<figure><img src="../../.gitbook/assets/image (1).webp" alt=""><figcaption></figcaption></figure>

## Introducción

Hashcat es una potente herramienta de recuperación de contraseñas que utiliza técnicas de ataque por diccionario, fuerza bruta y ataques híbridos para descifrar contraseñas hash. Esta guía te proporcionará una visión general sobre cómo instalar, configurar y utilizar Hashcat para descifrar contraseñas.

## Uso Básico

### Sintaxis de Hashcat

```javastacktrace
hashcat [opciones] [hashfile] [wordlist]
```

* **`[opciones]`**: Opciones de ataque, modo y configuración.
* **`[hashfile]`**: Archivo que contiene los hashes que deseas descifrar.
* **`[wordlist]`**: Archivo de texto que contiene posibles contraseñas.

### Ejemplos de uso

#### Atacar Hashes con un Diccionario

Supongamos que tienes un archivo llamado `hash.txt` con hashes SHA-512 y un archivo de diccionario llamado `rockyou.txt`. Para iniciar un ataque por diccionario, usa el siguiente comando:

```sh
hashcat -m 1700 -a 0 hash.txt rockyou.txt
```

* `-m 1700`: Modo de hash para SHA-512.
* `-a 0`: Modo de ataque por diccionario.

#### Guardar resultados en un Archivo

Para guardar los resultados en un archivo, usa la opción `--outfile`:

```bash
hashcat -m 1700 -a 0 hash.txt rockyou.txt --outfile cracked.txt
```

### Ver el estado del Ataque

Mientras Hashcat está en ejecución, puedes ver el progreso en la terminal. Hashcat también muestra estadísticas como el número de hashes descifrados y la velocidad de procesamiento.

## Opciones Avanzadas

### Modo de Ataque

* **Ataque por Diccionario (`-a 0`)**: Utiliza un archivo de diccionario para comparar con los hashes.
* **Ataque de Fuerza Bruta (`-a 3`)**: Intenta todas las combinaciones posibles de caracteres.
* **Ataque Híbrido (`-a 6` y `-a 7`)**: Combina ataques por diccionario con ataques de fuerza bruta.

### Modos de Hash

* **`-m 0`**: MD5
* **`-m 100`**: SHA1
* **`-m 1400`**: SHA-256
* **`-m 1700`**: SHA-512

Ver más [Modos de Hash](https://hashcat.net/wiki/doku.php?id=example_hashes)

## Reglas

Puedes aplicar reglas al diccionario para modificar las contraseñas (por ejemplo, agregar números o caracteres especiales). Utiliza el parámetro `-r`:

```bash
hashcat -m 1700 -a 0 hash.txt rockyou.txt -r rules/best64.rule
```

## Cracking con GPU

Si tienes una GPU, Hashcat puede usarla para acelerar el proceso de desciframiento. Asegúrate de que los controladores y las bibliotecas OpenCL o CUDA estén instalados y configurados correctamente.

## Ver Resultados

Una vez que Hashcat termine, puedes ver los resultados en el archivo de salida especificado o en la salida de la terminal. El formato de la salida generalmente es:

```
hash:contraseña
```

## Consejos Útiles

* **Actualiza Hashcat**: Las versiones más recientes pueden incluir mejoras y nuevos modos de ataque.
* **Optimiza Tu Diccionario**: Un diccionario bien curado puede acelerar el proceso de desciframiento.
* **Usa GPU si es Posible**: Las GPU pueden acelerar significativamente el proceso de cracking.

## Recursos Adicionales

* [Hashcat Official Documentation](https://hashcat.net/wiki/)
* [Hashcat Forum](https://hashcat.net/forum/)
* [Hashcat GitHub Repository](https://github.com/hashcat/hashcat)

