---
title: "OSEP Review - Offensive Security Experienced Penetration Tester"
date: 2026-08-22
tagline: OSEP Review 

# ============ CATEGORÍAS Y TAGS ============
categories: [Certificados]
tags: [AD, EVASION, OSEP, OSCE3]

# ============ CONTENIDO Y VISUALIZACIÓN ============
description: Reviewing OSEP camino al OSCE3

### IMGEN
image:
  path: /assets/img/osepreview/OSEP.png
  alt: PEN-300 OSEP Review
---

Hola nerds, una vez más por acá? bueno vamos al grano, esto será una review corta pero sincera sobre la certificación [OSEP - OffSec Experienced Penetration Tester](https://www.offsec.com/courses/pen-300/) hace unas semanas OffSec sacó por primera vez un descuento para el pack de 3 meses de sus cursos (menos para la nueva de IA OSAI), el precio regular es de $1,749 USD pero con el descuento era $1,400 USD así que aproveché la oportunidad y lo compré dado que es parte de las cert que necesito para obtener mi ansiado [OSCE3](https://www.offsec.com/certificates/osce3/) así que en esta entrada hablaré de mi proceso con el curso, si es necesario alguna certificación previa para cursarlo, requisitos previos que en mi opinión serán necesarios, entre otras cosas, así que comenzamos!

![OSEP](/assets/img/osepreview/01.webp)


## Un poco sobre OSEP
Esta es una certificación impartida por OffSec, una empresa líder en certificación de ciberseguridad, está centrada en evasión, técnicas avanzadas de Active Directory, movimiento lateral, ataques client side, etc, realmente el Syllabus es de acceso público así que lo dejo por acá abajo:
- Operating System and Programming Theory
- Client-Side Code Execution with Office
- Client-Side Code Execution with Jscript
- Process Injection and Migration
- Introduction to Antivirus Evasion
- Advanced Antivirus Evasion
- Application Whitelisting
- Bypassing Network Filters
- Linux Post Exploitation
- Windows Post Exploitation
- Kiosk Breakouts
- Windows Credentials
- Windows Lateral Movement
- Linux Lateral Movement
- Microsoft SQL Attacks
- Active Directory Exploitation
- Combining the Pieces

## Requisitos
Bien, acá OffSec dice textualmente que se requiere una certificación como OSCP o conocimientos equivalentes para cursar OSEP, realmente yo considero que no lo necesitas, si te gustan las certificaciones podrías ir antes por un CPTS o CRTP que te darán conocimientos necesarios en Active Directory y otra opinión personal, si es que quieres solo enfocarte en las técnicas mostradas, lánzate al curso con conocimientos básicos de programación, Windows internals y debugging (WinDbg de preferencia), esto lo digo porque dependiendo del plan que tengas tienes que aprovechar los 3 meses al máximo y por ejemplo en una parte enseñan bypass a AMSI manual con WinDbg, si no vas con los conocimientos mencionados antes tu curva de aprendizaje será más alta y por ende te tomará más tiempo absorberlo.

## Cómo prepararme
Bueno lo comenté un antes, realmente la mejor forma de prepararte antes de ingresar es tener conocimientos de AD como los podría dar un CPTS, CRTP o simplemente hacer muchas máquinas de HackTheBox de Active Directory a conciencia (entendiendo el por qué de las cosas) e ir con conocimiento de un lenguaje de programación, te diré que aprendas C antes que C#, te preguntarás por qué? si el curso está impartido mayormente en C# y mi respuesta automática es que la forma correcta de aprender es C y assembly y la forma correcta de desplegar las cosas es C#, C++, Rust, etc y por último ir entendiendo cómo funcionan los procesos en Windows, qué es un PE file y ya podrías comenzar el curso sin problema.

## Cómo abordar el examen
Es un examen largo realmente, si estás atascado en un ataque y no puedes continuar a pesar de que lo intentaste de varias formas diferentes reinicia el laboratorio, prueba en otra máquina, etc. Algo que aprendí acá en esta certi es que si tienes mucho tiempo y estás cansado, duerme. Agendé mi examen a las 2pm, a partir de la 1am me quedé 4 horas atascado en algo hasta las 4am, entonces me obligué a dormir, pedí al proctor que pausara mi cámara y por protocolo pausó mi VPN, luego de descansar retomé el examen y en lo que estaba atascado lo resolví en 10 minutos, así que descansen. Por último no se maten con cosas muy complejas, sean simples pero efectivos.

![](/assets/img/osepreview/02.png)

## Realmente enseña evasión?
No. Por el precio algunos esperamos contenido sobre EDRs o al menos contenido actualizado sobre evasión de AV, las técnicas mostradas en el curso son muy flojas, necesita una actualización, recomendaría este curso solo si quieres sacar el OSCE3 o estás comenzando y quieres una introducción más avanzada que el OSCP sobre hacking de interno/infraestructura.

## CAPE vs OSEP
Hacer esta comparación es un poco desproporcional porque el CAPE se centra en AD abarcando técnicas más avanzadas que el OSEP y el CAPE no está centrada en evasión como el OSEP, así que compararlas no tiene sentido.

## Despedida

Sea cual sea su objetivo siempre quieran el aprendizaje real, esto no se basa en solo tener una certificación por farmear aura. Bien, una vez dicho esto si tienen alguna duda pueden ponerse en contacto conmigo a través de Telegram @XK3NF4, eventualmente respondo más a menudo por ese medio.

Eso es todo nerds.

![](/assets/img/osepreview/03.png)
