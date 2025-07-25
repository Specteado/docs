---
hidden: true
---

# Clave pública SSH - ES

## Pasos para crear una clave pública SSH en Linux/macOS:

1. **Generar el par de claves SSH usando el comando `ssh-keygen`.** Ejecuta el siguiente comando:

```bash
ssh-keygen -t rsa -b 4096 -C "tu_correo@ejemplo.com"
```

Aqui:

* `-t rsa`: Especifica el tipo de clave, en este caso RSA (puedes usar otros tipos como `ed25519`).
* `-b 4096`: Especifica el tamaño de la clave en bits (4096 es un tamaño seguro para RSA).
* `-C "tu_correo@ejemplo.com"`: Es un comentario opcional que se añade a la clave pública para identificarla (normalmente se usa una dirección de correo electrónico).

1. **Guardar las claves:** Después de ejecutar el comando, te pedirá una ubicación para guardar el par de claves. Por defecto, se guardará en `~/.ssh/id_rsa` (clave privada) y `~/.ssh/id_rsa.pub` (clave pública). Puedes presionar `Enter` para aceptar la ubicación predeterminada.
2. **Proteger la clave privada con una frase de paso (opcional):** El sistema te pedirá una frase de paso (passphrase) opcional para proteger la clave privada. Puedes dejarlo en blanco si prefieres no usar una frase de paso, pero se recomienda usar una por razones de seguridad.
3.

    **Clave generada:** Una vez que completes los pasos anteriores, tendrás dos archivos:

    * **`~/.ssh/id_rsa`**: Tu clave privada. **Debe mantenerse segura y nunca compartirse.**
    * **`~/.ssh/id_rsa.pub`**: Tu clave pública. Esta es la clave que compartirás con los servidores a los que deseas conectarte.

## Ver la clave pública

Para ver el contenido de la clave pública (que normalmente se encuentra en `~/.ssh/id_rsa.pub`), puedes usar el siguiente comando:

```bash
cat ~/.ssh/id_rsa.pub
```

El contenido de este archivo es lo que deberás añadir al archivo `~/.ssh/authorized_keys` en los servidores a los que deseas conectarte.

### Ejemplo de clave pública SSH:

Una clave pública RSA se verá algo así:

```java
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQC0...truncated...xample+user@domain.com
```

Este es el valor que compartirías para que otros puedan autenticarse usando tu clave pública, mientras tú mantienes la clave privada en tu posesión para asegurar la autenticación segura.
