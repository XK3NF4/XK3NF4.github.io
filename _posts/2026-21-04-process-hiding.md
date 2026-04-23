---
title: "Process Hiding: Direct Kernel Object Manipulation"
date: 2026-04-20
tagline: Process Hiding 

# ============ CATEGORÍAS Y TAGS ============
categories: [Malware]
tags: [Kernel, Rootkits, WinDbg, RedTeam]

# ============ CONTENIDO Y VISUALIZACIÓN ============
description: Cómo los rootkits manipulan el kernel para ocultar procesos

### IMGEN
image:
  path: /assets/img/process-hiding/01.png
  alt: Process Hiding: Direct Kernel Object Manipulation
---

Bien, este es uno de los temas que más me apasionan, podría escribir por la eternidad sobre esto, pero hoy hablaremos de una de las técnicas que usan los rootkits para ocultar procesos de software que corre en modo usuario y monitorea procesos.

Herramientas como Task Manager, Process Explorer, Process Hacker, etc. La forma en que enumeran los procesos es recorriendo el `ActiveProcessLinks`.


## ActiveProcessLinks

Cuando se crea un proceso, el kernel crea una estructura `EPROCESS` para identificarlo. Los `EPROCESS` contienen varios campos, entre ellos `ActiveProcessLinks`. Lo que hace es enlazar dos punteros por cada proceso: [Flink y Blink](https://www.vergiliusproject.com/kernels/x64/windows-10/22h2/_LIST_ENTRY). La estructura EPROCESS vive en kernel space y no es accesible directamente desde user mode, aunque el kernel expone parte de su información a través de APIs como `NtQuerySystemInformation` que es justamente lo que usan las herramientas mencionadas

Como podemos ver, el offset de esta propiedad (ActiveProcessLinks) en Windows 10 es `+0x448`:

```
dt nt!_EPROCESS
```
![offset ActiveProcessLinks](/assets/img/process-hiding/02.png)

## Un poco más de EPROCESS

La forma de imaginar los `EPROCESS` es como una lista enlazada que vincula el `Flink` y `Blink` de cada proceso. `FLINK` contiene la dirección del siguiente proceso y `BLINK` contiene la dirección del proceso anterior.

Esta imagen ayuda a visualizar lo que estoy describiendo:

![EPROCESS ESTRUCTURA](/assets/img/process-hiding/03.png)


Pongamos un ejemplo si queremos referenciar el `ActiveProcessLinks` de un `EPROCESS`, tomamos la dirección base de ese `EPROCESS` y le sumamos el offset `+0x448`. Y si queremos acceder a `FLINK` o `BLINK` específicamente, sumamos sus offsets correspondientes: `FLINK = +0x000` y `BLINK = +0x008` (más adelante veremos cómo hacer cada cosa en práctica).

## Process Hiding

Luego de ver los conceptos de cómo funcionan las cosas, veremos cómo ocultar procesos. Tomaremos `cmd.exe` como nuestro proceso objetivo, pero en la práctica este puede ser el proceso de nuestro rootkit, etc.

Vemos cómo nuestro proceso `cmd.exe` es visible con las herramientas mencionadas:

![EPROCESS ESTRUCTURA](/assets/img/process-hiding/04.png)

Vamos con esto para ocultarnos.

Identificamos el `EPROCESS` address de `cmd.exe`:

```
!process 0 0 cmd.exe
```
![EPROCESS CMD](/assets/img/process-hiding/05.png)

Ahora necesitamos la dirección del proceso anterior y del siguiente. Para eso inspeccionamos los campos `FLINK` y `BLINK` de nuestro `EPROCESS`:

```
dt nt!_LIST_ENTRY ffff88869dcb5080+0x448
```

![LIST ENTRY](/assets/img/process-hiding/06.png)

Ya que tenemos las dos direcciones del `ActiveProcessLinks` del proceso anterior y el siguiente, tenemos que:

- Modificar el `FLINK` del proceso anterior para que apunte al siguiente proceso
- Modificar el `BLINK` del siguiente proceso para que apunte al proceso anterior



Modificamos el `FLINK` del proceso anterior:

```
eq 0xffff8886`9d32d4c8 0xffff8886`9e22d4c8
```

Modificamos el `BLINK` del siguiente proceso:

```
eq 0xffff8886`9e22d4c8+0x008 0xffff8886`9d32d4c8
```
![CAMBIO FLINK BLINK](/assets/img/process-hiding/07.png)

Ahora ponemos en `NULL` los valores `FLINK` y `BLINK` de nuestro `EPROCESS`:


```
eq ffff88869dcb5080+0x448 0x0
```

```
eq ffff88869dcb5080+0x448+0x008 0x0
```

>para el demo los ponemos en NULL, pero en la práctica se hace self-referencing para evitar romperlo

Validamos los cambios:
```
dt nt!_LIST_ENTRY ffff88869dcb5080+0x448
```
Y continuamos con la ejecución:

```
g
```

![FLINK Y BLINK EN NULL](/assets/img/process-hiding/08.png)

Como podemos ver, ocultamos exitosamente nuestro proceso `cmd.exe`.

![OCULTAR PROCESO](/assets/img/process-hiding/09.png)

eso es todo nerds.