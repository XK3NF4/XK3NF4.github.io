---
title: "OSCP vs CPTS"
date: 2026-01-02
tagline: OSCP vs CPTS
tagline: OSCP vs CPTS

# ============ CATEGORÍAS Y TAGS ============
categories: [Certificados]
tags: [Certificados, OSCP+, CTPS]

# ============ CONTENIDO Y VISUALIZACIÓN ============
description: OffSec Certified Professional+ (OSCP+) vs HTB Certified Penetration Testing Specialist (HTB CPTS)

### IMGEN
image:
  path: /assets/img/oscpvscpts/01.svg
  alt: OSCP+ vs CPTS

---

Esto pretende ser un review completamente honesto sobre las certificaciones [OSCP+ de Offensive Security](https://www.offsec.com/courses/pen-200/) y [CPTS de Hack The Box](https://academy.hackthebox.com/preview/certifications/htb-certified-penetration-testing-specialist), en la que veremos cuál elegir según a dónde queramos llegar y nuestros objetivos como pentesters.

## Descripción general de OSCP y CPTS
Ambas certificaciones están enfocadas en pentesting web e infraestructura (servidores Linux, Windows e infraestructura de Active Directory) y ambas se encuentran en la categoría "entry level" o al menos eso es lo que afirman ambas empresas. Más adelante veremos si realmente lo son o no.

## Precios y Requisitos
### OSCP
Precio: $1,749 USD (curso con laboratorios + 1 intento de examen).

Requisitos: no cuenta con ningún requisito obligatorio, salvo agendar con antelación la fecha en la que rendirás el examen. como recomendación ajusta la fecha a tu zona horaria y resérvala con tiempo, porque los cupos pueden llenarse y las fechas disponibles pueden quedar alejadas por la demanda de otros estudiantes.

### CPTS
Precio: 210 USD por el voucher del examen (sin contar el path de estudio) e incluye 2 intentos.

Requisitos: Cuenta con un path obligatorio que debes completar para poder rendir el examen. Puedes acceder a este path comprando una suscripción o adquiriendo cubos para desbloquear módulos. La opción más económica es vincular un correo de estudiante como correo secundario para pagar la suscripción mensual de 8 USD y completar el path.

### Importante
Dependiendo del plan que compres, el OSCP puede ser de 90 días, 1 año, etc. El material y el acceso solo durarán ese tiempo, pero ofrecen la opción de descargar un PDF con el material y los videos. En cambio en el CPTS, una vez completas un módulo (independientemente del plan de pago) el acceso a ese módulo es de por vida.


## Material de Estudio y Metodología

En cuanto al material el CPTS suele destacar por lo general ofrece un contenido más amplio y explica las vulnerabilidades con más detalle que el OSCP. Además también cambia la metodología de aprender y eso puede influir bastante en qué opción encaja mejor.
​

En el OSCP normalmente practicas, al final de cada laboratorio, lo que te acaban de enseñar (sin contar los labs avanzados ni el examen). En cambio, en el CPTS muchas veces tendrás que ir más allá de lo que te muestran, porque su enfoque busca que investigues y conectes ideas por tu cuenta “pensar fuera de la caja”. Así que aquí toca decidir si prefieres un aprendizaje más guiado y alineado con el índice o uno que te empuje a explorar más allá del contenido base.
​
## Te prepara para el examen?
En el OSCP es común tener que complementar por tu cuenta, sobre todo en explotacion web y en  el CPTS el temario suele cubrir lo que aparece, pero igual te exige razonamiento y creatividad.

## Formato del examen
### OSCP
Tiene una duración total de 48 horas: 23 h 45 min de examen práctico y 24 horas adicionales para subir el reporte. Durante el examen y el proceso estás bajo proctoring. Necesitas 70 puntos minimo

### CPTS
Tienes 10 días para completar el examen práctico y el reporte técnico, y necesitas un mínimo de 12 flags para pasar. Además no es proctored.
​
### Importante
El reporte es clave en ambos, si el reporte no cumple los requisitos (faltan pasos, evidencias o no es reproducible), puedes perder puntos o incluso desaprobar, aunque hayas conseguido los objetivos técnicos. En CPTS se exige un reporte con más requisitos, lo que lo hace más exigente.

## Experiencia Personal
En lo personal, y según muchos profesionales que rindieron el CPTS, se puede afirmar que el CPTS suele ser más duro que el OSCP, tanto en el examen práctico como en el reporte. No volvería a hacer ese reporte ni aunque me pagaran.

## Tips Para Aprobar

### OSCP

- Haz los laboratorios A, B y C, porque son muy similares al examen en algunas partes (sin entrar en spoilers).
- Trata de abordar Active Directory primero ya que en general suele ser más fácil que las máquinas individuales.
- Recuerda las limitaciones que tendrás en los labs A, B y C.
- No pierdas tu tiempo en los rabbit holes.
- Enumerar, enumerar y enumerar.

### CPTS
- Practica mucho Active Directory, no todo es BloodHound.
- El laboratorio empresarial practícalo como si fuera el examen intenta pwnearlo por tu cuenta.
- El módulo de reporte es el más importante del path.
- Enumerar, enumerar y enumerar.

## Mercado Laboral
Actualmente, el OSCP suele estar mejor visto por los equipos de Recursos Humanos, aunque ya existen ofertas laborales que piden CPTS. Esto pasa en parte porque el OSCP lleva más tiempo en el mercado y porque es un examen con proctoring, lo que a algunas empresas les sirve como señal rápida de “validación” del proceso.

## Palabras Finales
En realidad, el hecho de que el OSCP tenga proctoring no lo exime de que pueda haber trampas (no fomento hacer trampas solo menciono la realidad). 

Si eres alguien que quiere hacer el CPTS y el OSCP o incluso si solo quieres hacer el OSCP te recomiendo completar primero el path del CPTS y luego ir a por el OSCP.

Y por último, si apruebas el CPTS, puedes pagar para recibir tu certificado en físico.

![CPTS](/assets/img/oscpvscpts/02.png)
