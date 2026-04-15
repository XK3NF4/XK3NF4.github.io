---
title: "Oculto tras las Sombras de mis Redirectores"
date: 2026-03-18
tagline: Redirectores

# ============ CATEGORÍAS Y TAGS ============
categories: [Red Team]
tags: [OPSEC, phishing, C2, mod_rewrite]

# ============ CONTENIDO Y VISUALIZACIÓN ============
description: Tu no me puedes ver - Redirecciones en ejercicios de Red Team.

### IMGEN
image:
  path: /assets/img/redirectores/01.jpg
  alt: Tu no me puedes ver
---


Hola nerds! Una vez más leerán mi intento de blog, pero bueno, espero que les sirva el uso de redirectores en sus ejercicios de phishing, C2, etc. Siempre con fines éticos y de aprendizaje ese es el motivo de compartir mi conocimiento (sí, lo típico para que no me jodan luego). Feliz hacking chavales!

## Introducción
En las operaciones de Red Team y en las emulaciones/simulaciones de adversario, es importante mantener vivo nuestra infraestructura, ya sea de C2, phishing, etc. Debemos asumir que, tarde o temprano, seremos descubiertos (o tal vez no, en ciertos casos), pero nuestro objetivo principal es pasar desapercibidos el mayor tiempo posible. Es aquí donde entran los principios de OPSEC aplicados a nuestra infraestructura, siendo la implementación de redirectores una de las tácticas. En esta entrada, les enseñaré el uso de Apache `mod_rewrite`.

`mod_rewrite` nos permite crear reglas inteligentes para decidir qué tráfico llega a nuestro servidor, qué tráfico es redirigido a un sitio legítimo y qué tráfico es simplemente descartado. En otras palabras, `mod_rewrite` actúa como un proxy.

## Un Poco Más de mod_rewrite!
`mod_rewrite` es un módulo de Apache HTTP Server que proporciona un motor de reescritura de URLs basado en reglas. Utiliza regex para evaluar URLs entrantes y transformarlas, redirigirlas o bloquearlas según condiciones definidas.

Bueno, en este punto más de uno recordará el rendimiento de Nginx sobre Apache y se hará la pregunta "Por qué no usar un proxy inverso convencional como Nginx?" Mi respuesta es la lógica condicional.

Mientras que un proxy inverso convencional como Nginx puede reenviar tráfico, mod_rewrite permite crear lógica condicional compleja que evalúa múltiples variables de cada petición HTTP antes de decidir qué hacer con ella.

## Fundamentos de mod_rewrite
Solo tienes que instalar Apache y habilitar los modulos rewrite , proxy y proxy_http.  

```bash
sudo apt install apache2
sudo a2enmod rewrite proxy proxy_http
```

Verifica que `mod_rewrite` está cargado

```bash
apache2ctl -M | grep rewrite
```

### Ubicación de Reglas
Las reglas de `mod_rewrite` dependiendo de dónde se coloquen, su alcance y comportamiento variarán, presento 3 a continuación.

#### 1 - Configuración del VirtualHost

Se puede agregar a los `VirtualHost` y las reglas se aplicarán a dominios o subdominios específicos. 

```apache
# File: /etc/apache2/sites-enabled/000-default.conf
<VirtualHost *:80>
    ServerName ejemplo.com
    RewriteEngine On
    # Reglas aquí
</VirtualHost>
```

#### 2 - Archivos `.htaccess`

Las reglas en `.htaccess` se aplicaran a directorios y subdirectorios


```apache
# /var/www/html/.htaccess
RewriteEngine On
# Reglas aquí
```

<!-- >Nota OPSEC: Se prefiere la configuración en el VirtualHost porque los archivos .htaccess pueden ser descubiertos si un atacante o defensor logra listar archivos del servidor web. Además, las reglas en VirtualHost son más eficientes ya que se cargan una sola vez al iniciar Apache, mientras que .htaccess se lee en cada petición. -->

Para que `.htaccess` funcione, necesitas configurar `AllowOverride`:

```apache
<Directory /var/www/html>
    AllowOverride All
</Directory>
```

#### 3 - Location

Las reglas tambien se pueden aplicar a directivas especificas como `<Location>` para que coincidan con rutas URL específicas. 

```apache
<Location "/login">
    RewriteEngine On
    # Rules here #
</Location>
```

## Sintaxis Básica de Reglas

Una regla de `mod_rewrite` tiene esta estructura fundamental:

```apache
RewriteEngine On             # Activa el motor de reescritura
RewriteCond %{VARIABLE} patrón [flags]    # definimos qué requisitos debe cumplir la petición como venir de una IP específica o tener un User-Agent de Windows para que la regla se ejecute
RewriteRule patrón destino [flags]        # Regla de reescritura, define qué patrón buscamos en la URL y a dónde vamos a enviar al usuario o qué archivo le vamos a mostrar
```
aca un ejemplo:

```apache
RewriteEngine on

# Los Filtros o Condiciones
# [TestString] [CondPattern] [Flags]
RewriteCond %{HTTP_USER_AGENT} ^Mozilla.* [NC]

# Regla
# [Pattern] [Substitution] [Flags]
RewriteRule ^login$ /sitio_clonado.html [L]
```

Tranquilo, ahora toca desglosarlo.

### Sintaxis de RewriteEngine 
```apache
RewriteEngine on
```
Sin esta directiva en `on`, Apache ignorará todas las reglas siguientes.



### Sintaxis de RewriteCond
```apache
# RewriteCond [TestString] [CondPattern] [Flags]
RewriteCond %{HTTP_USER_AGENT} ^Mozilla.* [NC]
```

Esta es la condición que se buscará antes de ejecutar la regla.

#### TestString

En `TestString` puede ir una variable global del servidor, una variable de entorno o simplemente, cualquier dato relacionado con la solicitud en este caso, `HTTP_USER_AGENT`.

>En Apache, cuando usamos variables globales (como `HTTP_USER_AGENT`, `REMOTE_ADDR` o `QUERY_STRING`), siempre deben ir precedidas por `%` y encerradas en llaves `{}`. Esto diferencia una variable del servidor de una cadena de texto cualquiera.

Variables de servidor que más uso

| Variable | Descripción | Ejemplo |
|----------|-------------|---------|
| `%{REQUEST_URI}` | URI solicitada | `/updates/check` |
| `%{HTTP_USER_AGENT}` | User-Agent del cliente | `Mozilla/5.0...` |
| `%{REMOTE_ADDR}` | IP del cliente | `192.168.1.100` |
| `%{HTTP_HOST}` | Encabezado Host | `ejemplo.com` |
| `%{QUERY_STRING}` | Parámetros GET | `id=123&session=abc` |
| `%{HTTP_REFERER}` | Encabezado Referer | `https://google.com` |
| `%{HTTP_COOKIE}` | Cookies del cliente | `session=xyz` |
| `%{REQUEST_METHOD}` | Método HTTP | `GET`, `POST` |
| `%{HTTPS}` | Si es HTTPS | `on` / `off` |
| `%{HTTP:X-Custom-Header}` | Cualquier encabezado | Valor personalizado |
| `%{TIME_HOUR}` | Hora actual del servidor | `14` |

ref: [mas variables ](https://httpd.apache.org/docs/2.4/mod/mod_rewrite.html#rewritecond)


#### CondPattern
Ahora, en `CondPattern` va una regex que define la condición. Si la `TestString` coincide con este patrón, la `RewriteRule` se aplicará. En este caso, usamos `^Mozilla.*` para filtrar por este `User-Agent` específico.

#### Flags
Los `flags` son parámetros opcionales que se añaden al final de una directiva para alterar o controlar cómo se procesa una condición o una regla. Sin ellos, el motor de reescritura es muy rígido, pero con ellos ganamos más flexibilidad.

Por ejemplo, el flag [NC] (No Case) le indica a Apache que realice la comparación sin distinguir entre mayúsculas y minúsculas para detectar User-Agents que varían ligeramente.

Podemos encadenar múltiples condiciones para crear filtros robustos. Por defecto, cuando colocas varias directivas `RewriteCond` una tras otra, Apache las procesa usando un operador lógico `AND`. Esto significa que todas las condiciones deben cumplirse para que la `RewriteRule` final se ejecute.

Flags principales:
 
| Flag | Descripción |
|------|-------------|
| `[R=301]` | Redirección permanente |
| `[R=302]` | Redirección temporal |
| `[P]` | Proxy (reenvío transparente al backend) |
| `[L]` | Last — deja de procesar reglas |
| `[NC]` | No Case — sin distinción mayúsculas/minúsculas |
| `[OR]` | OR lógico entre condiciones |
| `[F]` | Forbidden — devuelve 403 |
| `[QSA]` | Query String Append — conserva parámetros |
| `[CO]` | Cookie — establece una cookie |
| `[E]` | Environment — establece variable de entorno |
| `[NE]` | No Escape — no codifica caracteres especiales |

Aca tienes mas [flags](https://httpd.apache.org/docs/current/rewrite/flags.html).


### Sintaxis de RewriteRule

```apache
# RewriteRule [Pattern] [Substitution] [Flags]
RewriteRule ^login$ /sitio_clonado.html [L]
```

Esta es la directiva que define finalmente qué vamos a hacer con la solicitud, la dejamos pasar al C2? , la enviamos a un sitio legítimo o simplemente la bloqueamos?

#### Pattern

Una va un regex que debe coincidir con la URL solicitada por el cliente.

#### Substitution

Es la URL de destino o la ruta interna a la que se reescribirá o redirigirá la petición. Aquí podras mandar a la victima a de tu Team Server o tu landing page.

#### Flags

Son modificadores que controlan el comportamiento de la regla como lo que vimos en RewriteCond

Un error común es pensar que las reglas se aplican de forma aleatoria. En realidad, mod_rewrite funciona de forma secuencial, muy similar a cómo un firewall procesa sus reglas (ACLs).

Las reglas se evalúan de arriba hacia abajo. Si una solicitud coincide con un patrón y tiene la bandera [L], el motor se detiene ahí mismo y ejecuta la acción. Si no tiene el flag [L], el motor continuará evaluando las reglas siguientes, lo que podría arruinar tu OPSEC si una regla posterior sobreescribe la anterior.

Aca tienes mas [flags](https://httpd.apache.org/docs/current/rewrite/flags.html).

## Diagrama

>[!Tip]
Es una buena práctica de OPSEC tener un servidor de salto.

![diagrama](/assets/img/redirectores/02.png)

Tu no me puedes ver!