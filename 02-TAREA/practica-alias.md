# Práctica de Alias en Bash — Evidencia de Laboratorio

**Sistema:** Ubuntu (VirtualBox) — usuario `vboxuser@Lol`
**Directorio de trabajo:** `~/laboratorio-cli`
**Fecha:** 31 de agosto, 2026

## 1. Investigación: comando para listar todos los alias

En Bash, el comando para listar **todos los alias definidos en la sesión actual** es:

```bash
alias
```

Este comando, sin argumentos, imprime la lista completa de alias activos en el formato `nombre='comando'`.

Variantes útiles:

| Comando | Qué hace |
|---|---|
| `alias` | Lista todos los alias activos en la sesión |
| `alias -p` | Igual que `alias`, pero en formato "portable" (el mismo que usa Bash internamente, ideal para guardar en un script) |
| `alias nombre` | Muestra solo la definición del alias `nombre` |
| `type nombre` | Indica si `nombre` es un alias, función, comando builtin o binario, y muestra su definición si es alias |
| `unalias nombre` | Elimina un alias de la sesión actual |

En esta práctica también se usó `grep -n "alias cduaz" ~/.bashrc` para verificar, dentro del archivo de configuración, si el alias ya existía antes de crearlo.

## 2. Objetivo de la práctica (Diapositiva 15)

Crear un alias personalizado llamado **`cduaz`** que, al ejecutarse, nos lleve directamente al directorio `~/laboratorio-cli`, y dejarlo definido de forma **permanente** en el archivo `~/.bashrc` para que esté disponible en cada nueva sesión de terminal.

## 3. Paso a paso con evidencia

### Paso 1 — Verificar si el alias ya existe en `.bashrc`

Se usó `grep -n` para buscar si la línea del alias `cduaz` ya estaba presente en el archivo de configuración `~/.bashrc`:

```bash
grep -n "alias cduaz" ~/.bashrc
```

**Resultado:** el archivo ya contenía la línea `1:alias cduaz='cd ~/laboratorio-cli'`, confirmando que la definición estaba en la línea 1.

![Verificación con grep del alias cduaz en .bashrc](capturas/01-grep-alias.png)

### Paso 2 — Editar `.bashrc` con `nano` para confirmar/ajustar la definición

Se abrió el archivo con el editor `nano`:

```bash
nano ~/.bashrc
```

Dentro del editor se observa la línea del alias ya definida:

```bash
alias cduaz='cd ~/laboratorio-cli'
```

Esta línea le indica a Bash que, cada vez que se escriba `cduaz`, se ejecute internamente `cd ~/laboratorio-cli`.

![Edición de .bashrc con nano mostrando la línea del alias](capturas/02-nano-bashrc.png)

### Paso 3 — Recargar la configuración, comprobar el alias y probarlo

Después de guardar los cambios en `nano`, se recargó la configuración de Bash sin necesidad de abrir una nueva terminal:

```bash
source ~/.bashrc
```

Se confirmó que el alias quedó registrado en la sesión actual:

```bash
type cduaz
```

**Salida:** `cduaz is aliased to 'cd ~/laboratorio-cli'`

Finalmente se probó el alias y se verificó el resultado con `pwd`:

```bash
cduaz
pwd
```

**Salida:** `/home/vboxuser/laboratorio-cli` — confirmando que el alias funciona correctamente y nos movió al directorio esperado.

![source, type y prueba del alias cduaz con pwd](capturas/03-source-type-cduaz.png)

## 4. Conclusión

Se investigó y comprobó que `alias` (sin argumentos) es el comando para listar todos los alias activos en Bash. Además, se completó la práctica de la diapositiva 15: se creó/verificó el alias `cduaz='cd ~/laboratorio-cli'`, se agregó de forma persistente en `~/.bashrc`, se recargó la configuración con `source`, y se validó su funcionamiento con `type` y `pwd`, confirmando que el alias navega correctamente al directorio `~/laboratorio-cli`.
