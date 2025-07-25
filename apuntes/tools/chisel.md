# Chisel

**Chisel** es un túnel rápido TCP/UDP, transportado sobre HTTP, asegurado vía SSH. Un único ejecutable que incluye cliente y servidor.

Escrito en Go (golang).

**Chisel** es principalmente útil para pasar a través de cortafuegos, aunque también se puede utilizar para proporcionar un punto final seguro en su red.

## Descarga

{% embed url="https://github.com/jpillora/chisel" %}

<figure><img src="../../.gitbook/assets/image (2).png" alt="" width="563"><figcaption></figcaption></figure>

Entramos en el apartado R**eleases** y descargamos la de nuestro sistema operativo

Para Linux:

* [chisel\_1.10.0\_linux\_386.gz](https://github.com/jpillora/chisel/releases/download/v1.10.0/chisel_1.10.0_linux_386.gz)
* [chisel\_1.10.0\_linux\_amd64.gz](https://github.com/jpillora/chisel/releases/download/v1.10.0/chisel_1.10.0_linux_amd64.gz)

Para Windows:

* [chisel\_1.10.0\_windows\_386.gz](https://github.com/jpillora/chisel/releases/download/v1.10.0/chisel_1.10.0_windows_386.gz)
* [chisel\_1.10.0\_windows\_amd64.gz](https://github.com/jpillora/chisel/releases/download/v1.10.0/chisel_1.10.0_windows_amd64.gz)

## Uso

<figure><img src="../../.gitbook/assets/image (3).png" alt="" width="563"><figcaption></figcaption></figure>

1º Nos pasamos la herramienta de chisel a la maquina puente

2º Creamos un servidor de chisel en nuestro equipo

```bash
./chisel server -p 8888 --reverse
```

3º Creamos el cliente proxy en la maquina puente

```java
./chisel client 192.168.1.59:8888 R:socks
```

4º Configuramos el fichero de `proxychains`

<figure><img src="../../.gitbook/assets/image (7).avif" alt="" width="563"><figcaption></figcaption></figure>

5º Uso final

```haskell
proxychains comando que quieras usar 
```

## Port forwarding

1º Nos pasamos la herramienta de chisel a la maquina puente

2º Creamos un servidor de chisel en nuestro equipo

```bash
./chisel server -p 8888 --reverse
```

3º Creamos el cliente proxy en la maquina puente, diciendo su puerto que queremos que sea el nuestro

```java
./chisel client 192.168.1.59:8888 R:22:127.0.0.1:22
```

{% hint style="info" %}
Aqui le estamos diciendo que su puerto 22 sea el nuestro
{% endhint %}

4º Configuramos el fichero de `proxychains`

5º Uso final

```bash
proxychains comando que quieras usar 
```

## Videos

{% embed url="https://youtu.be/6eOA8JKKqUk?si=qbRRYPZvZ_ji9Uwx" %}
