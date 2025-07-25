# Tratamiento de TTY

<pre class="language-java"><code class="lang-java"><strong>Script /dev/null -c bash
</strong></code></pre>

Salida

```java
Script started, file is /dev/null
```

Luego de esto presionamos `ctrl_z` para suspender la shell.

Salida:

```javastacktrace
zsh: suspended  nc -nlvp 443
```

Ahora resetearemos la configuración de la shell que dejamos en segundo plano indicando **reset** y **xterm:**

```javascript
[1]  + continued  nc -nlvp 443
```

Escribir reset:

<pre class="language-javastacktrace"><code class="lang-javastacktrace"><strong>                                reset
</strong></code></pre>

Salida:

```javascript
reset: unknown terminal type unknown
```

Tipo de terminal:

```java
Terminal type? xterm
```

* `export TERM=xterm` -> Debemos hacer esto ya que a pesar de haberle indicado que queríamos una **xterm** al momento de reiniciarlo la variable de entorno **TERM** vale **dump** (Se usa esta variable para poder usar los atajos de teclado).
* `export SHELL=bash` -> Para que nuestra shell sea una bash

```javascript
export TERM=xterm
```

```javascript
export SHELL=bash
```
