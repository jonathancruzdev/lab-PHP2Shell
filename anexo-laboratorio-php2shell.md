# ANEXO I

# Preparación del entorno de laboratorio con Docker

**Materia:** Seguridad e Integridad\
**Actividad:** Análisis de vulnerabilidades y remediación -- PHP2Shell\
**Herramientas:** Docker Desktop, Docker Compose y Visual Studio Code\
**Sistema operativo de referencia:** Windows 10/11

## 1. Introducción

En este anexo aprenderemos a preparar un entorno de ejecución web
utilizando Docker. Construiremos una aplicación sencilla basada en PHP y
Apache, la ejecutaremos dentro de un contenedor y posteriormente
actualizaremos la versión de PHP para analizar el proceso de
remediación.

Trabajaremos con dos versiones:

  Versión      Uso en la práctica
  ------------ -----------------------------------------------
  PHP 8.5.11   Versión anterior a la corrección de PHP2Shell
  PHP 8.5.13   Versión posterior a la corrección

**Importante:** la versión vulnerable se utilizará exclusivamente con
fines educativos, dentro de un entorno local y aislado. No debe
utilizarse para alojar aplicaciones reales ni exponerse a Internet. No
vamos a ejecutar exploits.

## 2. Requisitos previos

-   Computadora con Windows 10 u 11.
-   Conexión a Internet para descargar las imágenes iniciales.
-   Docker Desktop instalado.
-   Visual Studio Code o un editor de texto.
-   Terminal PowerShell.

### 2.1. Instalar Docker Desktop

Ingresar al sitio oficial:
<https://www.docker.com/products/docker-desktop/>

Descargar e instalar Docker Desktop para Windows. Durante la
instalación, utilizar la configuración recomendada con WSL 2, si está
disponible.

Una vez instalado:

1.  Abrir Docker Desktop.
2.  Esperar a que el servicio indique que Docker está funcionando.
3.  Abrir PowerShell.
4.  Ejecutar:

``` powershell
docker --version
docker compose version
```

Si ambos comandos devuelven información de versión, Docker está
disponible.

**Evidencia 1:** captura de pantalla con los resultados de ambos
comandos.

## 3. Crear el proyecto

En PowerShell, ejecutar:

``` powershell
mkdir laboratorio-php2shell
cd laboratorio-php2shell
```

Crear esta estructura:

``` text
laboratorio-php2shell/
│
├── compose.yaml
├── Dockerfile
│
└── src/
    └── index.php
```

La carpeta `src` contendrá nuestra aplicación PHP. Los archivos
`Dockerfile` y `compose.yaml` permitirán construir y ejecutar el
entorno.

## 4. Crear el Dockerfile

Crear un archivo llamado `Dockerfile` en la raíz del proyecto y copiar:

``` dockerfile
ARG PHP_VERSION=8.5.11

FROM php:${PHP_VERSION}-apache
```

**¿Qué significa?**

-   `ARG PHP_VERSION`: define una variable para seleccionar la versión
    de PHP.
-   `FROM`: indica la imagen base que se utilizará.
-   `php:8.5.11-apache`: utiliza una imagen de PHP que incluye Apache.

La variable permitirá cambiar la versión de PHP sin modificar la
estructura del proyecto.

## 5. Crear el archivo compose.yaml

Crear `compose.yaml` en la raíz del proyecto y copiar:

``` yaml
services:
  web:
    build:
      context: .
      args:
        PHP_VERSION: "8.5.11"

    container_name: php2shell-lab

    ports:
      - "127.0.0.1:8080:80"

    volumes:
      - ./src:/var/www/html:ro

    networks:
      - laboratorio

networks:
  laboratorio:
    internal: true
```

### ¿Qué estamos configurando?

  -----------------------------------------------------------------------
  Configuración                       Función
  ----------------------------------- -----------------------------------
  `build`                             Construye la imagen utilizando
                                      nuestro Dockerfile

  `PHP_VERSION`                       Selecciona la versión de PHP

  `container_name`                    Define el nombre del contenedor

  `ports`                             Permite acceder a Apache desde el
                                      puerto local 8080

  `volumes`                           Vincula nuestra carpeta de código
                                      con el contenedor

  `networks`                          Conecta el servicio a una red de
                                      laboratorio

  `internal: true`                    Crea una red interna sin
                                      conectividad de salida hacia redes
                                      externas
  -----------------------------------------------------------------------

El puerto está vinculado exclusivamente a `127.0.0.1`, por lo que el
servicio queda accesible desde la propia computadora y no desde otros
equipos de la red. No modifiquen estas configuraciones para publicar el
servicio en Internet.

## 6. Crear nuestra aplicación PHP

Dentro de `src`, crear un archivo llamado `index.php` y copiar:

``` php
<?php

$version = PHP_VERSION;
$sapi = PHP_SAPI;

$extensiones = get_loaded_extensions();

sort($extensiones);

?>

<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">

    <title>Laboratorio PHP2Shell</title>

    <style>
        body {
            font-family: Arial, sans-serif;
            background: #f1f5f9;
            margin: 0;
            padding: 40px;
        }

        main {
            max-width: 750px;
            margin: auto;
            background: white;
            padding: 30px;
            border-radius: 12px;
        }

        h1 { color: #0f766e; }

        .dato {
            background: #f1f5f9;
            padding: 12px;
            margin: 10px 0;
            border-radius: 6px;
        }

        .aviso {
            color: #92400e;
            background: #fef3c7;
            padding: 12px;
            border-radius: 6px;
        }
    </style>
</head>

<body>
<main>
    <h1>Laboratorio PHP2Shell</h1>
    <p>Entorno de práctica de Seguridad e Integridad.</p>

    <div class="dato">
        <strong>Versión de PHP:</strong>
        <?= htmlspecialchars($version) ?>
    </div>

    <div class="dato">
        <strong>SAPI:</strong>
        <?= htmlspecialchars($sapi) ?>
    </div>

    <div class="dato">
        <strong>Servidor:</strong>
        Apache
    </div>

    <h2>Extensiones habilitadas</h2>
    <ul>
        <?php foreach ($extensiones as $extension): ?>
            <li><?= htmlspecialchars($extension) ?></li>
        <?php endforeach; ?>
    </ul>

    <div class="aviso">
        Entorno educativo local. No utilizar con información real.
    </div>
</main>
</body>
</html>
```

Este archivo muestra la versión de PHP utilizada por la aplicación, la
SAPI que ejecuta el código y las extensiones habilitadas. No utilizamos
`phpinfo()` porque puede revelar información sensible sobre la
configuración del servidor.

## 7. Construir y ejecutar el entorno

Abrir PowerShell dentro de la carpeta `laboratorio-php2shell`.

Primero, verificar la configuración:

``` powershell
docker compose config
```

Si no aparecen errores, construir la imagen y ejecutar el servicio:

``` powershell
docker compose up -d --build
```

Consultar los contenedores activos:

``` powershell
docker ps
```

Debería aparecer un contenedor llamado `php2shell-lab`.

### Acceder a la aplicación

Abrir el navegador e ingresar a:

<http://localhost:8080>

Debería visualizarse la página del laboratorio con la información de
PHP.

**Evidencia 2:** captura de pantalla donde se visualice la aplicación
funcionando y la versión de PHP.

## 8. Inspeccionar el entorno desde Docker

Consultar la versión de PHP:

``` powershell
docker compose exec web php -v
```

Consultar las extensiones:

``` powershell
docker compose exec web php -m
```

Consultar los archivos de configuración:

``` powershell
docker compose exec web php --ini
```

Consultar los módulos de Apache:

``` powershell
docker compose exec web apache2ctl -M
```

Consultar los registros del servicio:

``` powershell
docker compose logs --tail=50 web
```

Comparar los resultados obtenidos desde la terminal con los que muestra
el navegador.

**Pregunta:** ¿Por qué es importante verificar la versión de PHP que
utiliza realmente la aplicación y no solamente consultar la versión
instalada en la computadora?

**Evidencia 3:** guardar capturas de los comandos y sus resultados.

## 9. Actualizar PHP a una versión corregida

En `compose.yaml`, buscar:

``` yaml
PHP_VERSION: "8.5.11"
```

Modificar por:

``` yaml
PHP_VERSION: "8.5.13"
```

Esta versión es posterior a PHP 8.5.12, que incorporó las correcciones
iniciales para las vulnerabilidades PHP2Shell.

Guardar el archivo.

### 9.1. Reconstruir la imagen

Ejecutar:

``` powershell
docker compose build --pull --no-cache
```

Este comando vuelve a construir la imagen y solicita la imagen base al
registro, evitando reutilizar la caché de construcción.

### 9.2. Recrear el contenedor

Ejecutar:

``` powershell
docker compose up -d --force-recreate
```

Docker recreará el contenedor utilizando la nueva versión configurada.

### 9.3. Verificar la actualización

Ejecutar:

``` powershell
docker compose exec web php -v
```

También pueden ingresar nuevamente a <http://localhost:8080>.

La aplicación deberá mostrar la nueva versión de PHP.

**Evidencia 4:** captura donde se observe la versión actualizada.

## 10. Comparación de resultados

Completar la siguiente tabla:

  Elemento                  Antes de actualizar   Después de actualizar
  ------------------------- --------------------- -----------------------
  Versión PHP                                     
  SAPI                                            
  Servicio Apache                                 
  Aplicación disponible                           
  Extensiones habilitadas                         

Responder:

1.  ¿Qué archivo fue necesario modificar?
2.  ¿Por qué fue necesario reconstruir la imagen?
3.  ¿Actualizar PHP en la computadora anfitriona habría producido el
    mismo resultado?
4.  ¿Qué diferencia existe entre una imagen Docker y un contenedor?
5.  ¿Cómo podemos comprobar que la aplicación utiliza la versión
    corregida?

## 11. Detener y eliminar el entorno

Una vez finalizada la actividad, detener y eliminar los recursos del
proyecto:

``` powershell
docker compose down
```

Este comando detiene y elimina el contenedor y la red creada por
Compose. Las imágenes descargadas pueden permanecer en la computadora.

Para verificar que el contenedor ya no está ejecutándose:

``` powershell
docker ps
```

## 12. Problemas frecuentes

### Docker no responde

Verificar que Docker Desktop esté iniciado y que el servicio se
encuentre funcionando.

### El puerto 8080 está ocupado

Puede existir otra aplicación utilizando ese puerto. Cambiar la
configuración:

``` yaml
ports:
  - "127.0.0.1:8081:80"
```

Luego acceder mediante <http://localhost:8081>.

### No se puede descargar la imagen

Verificar la conexión a Internet y que Docker Desktop pueda acceder a
Docker Hub. También pueden intentar:

``` powershell
docker pull php:8.5.11-apache
```

### La aplicación no muestra los cambios

Verificar que `index.php` esté guardado y que el volumen esté
correctamente configurado.

### El contenedor no inicia

Consultar los registros:

``` powershell
docker compose logs web
```

## 13. Entrega del anexo

Este anexo forma parte del laboratorio práctico PHP2Shell.

Cada equipo deberá conservar las evidencias obtenidas durante la
preparación del entorno y utilizarlas para completar el informe técnico
solicitado en la guía principal.

**Evidencias mínimas:**

-   Docker instalado y funcionando.
-   Estructura del proyecto.
-   Aplicación ejecutándose con PHP 8.5.11.
-   Resultado de los comandos de inspección.
-   Aplicación ejecutándose después de la actualización a PHP 8.5.13.
-   Tabla comparativa de resultados.

**Reflexión final:**

¿Qué importancia tiene la actualización de los componentes y
dependencias de una aplicación web dentro de un proceso de desarrollo
seguro?

La seguridad de una aplicación no depende únicamente del código que
escribimos. También depende de los componentes, servicios, bibliotecas y
entornos de ejecución sobre los cuales funciona.
