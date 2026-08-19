---
title: "OSWE Review - Offensive Security Web Expert"
date: 2026-07-26
tagline: OSWE Review 

# ============ CATEGORÍAS Y TAGS ============
categories: [Certificados]
tags: [Hacking WEB, OSCE3]

# ============ CONTENIDO Y VISUALIZACIÓN ============
description: Reviewing OSWE camino al OSCE3

### IMGEN
image:
  path: /assets/img/oswereview/OSWE.png
  alt: WEB-300 OSWE Review
---

Hola nerds, comenzando en mi camino de ser OSCE3 se me dio la oportunidad de cursar [OSWE - Offensive Security Web Expert](https://www.offsec.com/courses/web-300/) de OffSec, este curso es considerado por muchos el curso de hacking web más avanzado, también lo compararé con el curso de [CWEE - Advanced Web Penetration Testing Certification](https://academy.hackthebox.com/preview/certifications/htb-certified-web-exploitation-expert) de HackTheBox con la finalidad de hacer una comparación sincera de cuál es más avanzado y consideraciones que una persona podría tener tanto costos, como es valorado actualmente en el mercado del hacking sobre todo ahora con el avance de la IA, sujétense los lentes nerds que comenzamos!

![OSWE](/assets/img/oswereview/01.webp)

## Un poco sobre OSWE

Esta es la certificación más avanzada que existe en hacking ofrecida por OffSec, una de las empresas líderes en certificados, creadora de Kali Linux entre otras cosas, con un precio base de 1700 dólares te brindan acceso a 3 meses de material y laboratorio en lo que te dura ese acceso, además puedes solicitar la descarga del material de texto que te lo entregan en un PDF más los videos. Una principal diferencia entre esta certificación y otras que existen en el mercado es que está centrado más en el code review, lo que quiere decir white box.

## Requisitos
Como es de suponer uno de los requisitos necesarios para cursar este curso es la capacidad y familiarización con leer y escribir código y entender vulnerabilidades web, entre los lenguajes principales que podrás ver están PHP, JAVA, .NET, Python, etc. Realmente no es necesario que los domines todos, solo uno para scripting como Python, pero que sepas entender código, entender cómo funciona el Modelo MVC (Modelo Vista Controlador) y que tengas muchas ganas de aprender, podrás llevar el curso sin problemas.

## Cómo prepararme
Bueno acá seré directo e iré al grano, si no entiendes las vulnerabilidades web o no sientes que domines las principales te recomendaría comenzar por  [Portswigger Academy](https://portswigger.net/web-security) que es gratuito.
Una vez que tengas el conocimiento de cómo funcionan las vulnerabilidades web lo ideal sería que programes pequeñas webs en PHP usando el modelo MVC mencionado anteriormente con la finalidad de familiarizarte con la misma y entender más cómo funciona la web por dentro.
Con esta experiencia lo siguiente sería ir por [PentesterLab](https://pentesterlab.com/), Pentester Lab te da un descuento con correo de estudiante, recomiendo Pentester Lab porque te enseña desde cómo tirar un GET scripteando a explotación web de CVEs reales, esto te será de mucha ayuda dado que se centran en el code review.

## Cómo abordar el examen
Bueno ahora les compartiré cómo fue mi preparación durante el curso, el curso me tomó 2 semanas en completarlo aproximadamente, pero no te apresures todos tienen su ritmo, todos tienen su ritmo de aprender, dicho esto lo que yo hacía cuando terminaba un módulo es automatizar toda la explotación en un solo archivo exploit.py lo que me sirvió para afrontar el examen, es importante que apuntes los fragmentos en tus notas dado que al ser este un examen de libro abierto los podrás reutilizar, desde lo más simple como enviar todas peticiones por el proxy de Burpsuite hasta como crear tu propio listener con socket.

Siempre lee la guía del examen OSWE porque se actualiza constantemente, también recuerda que el objetivo más importante del examen es entregar un script que automatice toda la explotación (te recomiendo usar Python) sin la intervención del usuario. Puedes lograr el objetivo si tu script hace una de las 2 cosas:
- No te da una reverse shell pero muestra por consola la flag local.txt y proof.txt
- Te da una reverse shell y al momento de tomar tu captura para tu reporte leas con el comando cat las flags


![OSWE](/assets/img/oswereview/03.png)


## OSWE vs CWEE
Considero que esta comparativa puede abordar tranquilamente otra entrada en mi blog así que solo daré la siguiente afirmación:
OSWE es la cert más avanzada en hacking web que hay y CWEE es la cert más difícil de hacking web que hay.

## Conclusiones
Tener una certificación como el OSWE te da un gran valor en el mercado laboral sin contar que es una de las necesarias para el gran ansiado OSCE3, en el mercado actual dado el gran aumento de la IA las certificaciones de OffSec cobran un mayor valor debido al proctored, una persona podría filtrar más rápido a alguien que tiene OSWE sobre alguien que tiene CWEE porque se sabe que CWEE podría resolverlo fácilmente con un agente de IA.

Como últimas palabras quiero decir que las certificaciones te pueden abrir puertas, pero tu conocimiento y el estudio constante las mantienen abiertas.

Si deseas contactarme lo puedes hacer mediante Telegram @XK3NF4, solo uso ese medio para comunicarme así que puedes hacerme las preguntas prudentes sobre alguna duda, no esperes mi respuesta solo pregunta y cuando tenga tiempo lo responderé.

Eso es todo nerds.




![OSWE](/assets/img/oswereview/O2.jpg)
