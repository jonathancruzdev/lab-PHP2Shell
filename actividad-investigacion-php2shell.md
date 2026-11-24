# ACTIVIDAD DE INVESTIGACIÓN

## PHP2Shell: análisis de una vulnerabilidad crítica en PHP

**Materia:** Seguridad e Integridad\
**Clase:** 16 -- Cierre integrador\
**Modalidad:** Trabajo colaborativo\
**Organización:** Equipos de 2 o 3 integrantes\
**Tiempo de investigación:** 15 minutos\
**Puesta en común:** 10 minutos

------------------------------------------------------------------------

## 1. Situación

Durante octubre de 2026 se divulgaron vulnerabilidades críticas que
afectan al intérprete PHP. El caso fue denominado **PHP2Shell** y se
encuentra asociado a dos identificadores:

-   CVE-2026-109618
-   CVE-2026-109619

Las vulnerabilidades pueden permitir la ejecución remota de código en
determinadas condiciones.

Como futuros profesionales del desarrollo web, deberán investigar el
caso utilizando fuentes técnicas confiables y elaborar un diagnóstico.

## 2. Fuentes de consulta

Utilicen principalmente las siguientes fuentes:

1.  **PHP -- Aviso oficial de seguridad:**\
    <https://www.php.net/archive/2026.php>

2.  **NVD -- CVE-2026-109618:**\
    <https://nvd.nist.gov/vuln/detail/CVE-2026-109618>

3.  **NVD -- CVE-2026-109619:**\
    <https://nvd.nist.gov/vuln/detail/CVE-2026-109619>

4.  **CISA -- Alerta de seguridad:**\
    <https://content.govdelivery.com/accounts/USDHSCISA/bulletins/42ff5ac>

5.  **CERT-EU -- Análisis de las vulnerabilidades:**\
    <https://cert.europa.eu/publications/security-advisories/2026-018/>

6.  **NHS England -- Actualización de la amenaza:**\
    <https://digital.nhs.uk/cyber-alerts/2026/cc-4875>

No es necesario leer todos los documentos completos. Identifiquen la
información relevante para responder las consignas.

**Importante:** registren la fecha de consulta y la fecha de publicación
o actualización de cada fuente. La información sobre una vulnerabilidad
puede cambiar a medida que aparecen nuevos análisis y evidencias.

## 3. Consignas de investigación

### Parte A -- Comprender la vulnerabilidad

1.  ¿Qué es PHP2Shell?
2.  ¿Qué componente de PHP está afectado?
3.  ¿Qué diferencias existen entre CVE-2026-109618 y CVE-2026-109619?
4.  ¿Qué significa RCE (*Remote Code Execution*)?
5.  ¿Por qué estas vulnerabilidades representan un riesgo para
    aplicaciones web?

### Parte B -- Analizar el impacto

6.  ¿Qué versiones de PHP fueron afectadas?
7.  ¿Qué versiones incorporaron las correcciones iniciales?
8.  ¿Qué consecuencias podría tener una explotación exitosa?
9.  ¿Qué propiedades de la seguridad de la información podrían verse
    comprometidas: confidencialidad, integridad o disponibilidad?

### Parte C -- Investigar la respuesta

10. ¿Qué medidas recomendó el equipo de desarrollo de PHP?
11. ¿Qué recomendaciones realizó CISA?
12. ¿Por qué es importante identificar todas las instalaciones de PHP
    dentro de una organización?
13. ¿Qué medidas deberían adoptarse si una organización no puede
    actualizar inmediatamente?

### Parte D -- Contrastar fuentes

14. ¿Todas las fuentes presentan la misma información sobre la
    explotación de estas vulnerabilidades?
15. ¿Qué diferencias encuentran entre las publicaciones iniciales y las
    actualizaciones posteriores?
16. ¿Por qué es importante verificar la fecha de publicación de un aviso
    de seguridad?

Al contrastar fuentes, distingan entre:

-   Información técnica confirmada.
-   Recomendaciones de mitigación.
-   Evidencias o reportes de explotación.
-   Hipótesis o posibilidades de impacto.

No consideren que una vulnerabilidad fue explotada en un sistema
determinado si las fuentes consultadas no aportan evidencias para
afirmarlo.

## 4. Análisis aplicado

Imaginen que una institución educativa utiliza una plataforma web
desarrollada en PHP.

La plataforma:

-   Se encuentra publicada en Internet.
-   Gestiona usuarios y contraseñas.
-   Almacena información académica.
-   Utiliza una versión de PHP potencialmente afectada.

Respondan:

1.  ¿Qué activos deberían protegerse prioritariamente?
2.  ¿Qué riesgos identifican?
3.  ¿Qué acciones deberían realizarse inmediatamente?
4.  ¿Qué evidencias buscarían para determinar si existió un incidente?
5.  ¿Qué medidas recomendarían para evitar situaciones similares?

Fundamenten las respuestas utilizando los conceptos trabajados durante
la cursada.

## 5. Producto esperado

Cada equipo deberá elaborar una síntesis de investigación que contenga:

-   Descripción de PHP2Shell.
-   Identificación de las dos vulnerabilidades.
-   Versiones afectadas y corregidas.
-   Impactos potenciales.
-   Recomendaciones de seguridad.
-   Conclusión del equipo.
-   Fuentes consultadas, con sus respectivas fechas.

**Formato de presentación:** una hoja de síntesis o una diapositiva por
equipo.

La producción debe ser clara, breve y estar fundamentada. No se espera
copiar fragmentos de las fuentes, sino interpretar la información y
expresarla con palabras propias.

## 6. Puesta en común

Cada equipo dispondrá de aproximadamente dos minutos para compartir:

-   Un hallazgo técnico.
-   Un riesgo relevante.
-   Una recomendación de seguridad.

El resto de los equipos podrá realizar preguntas o complementar la
información.

Durante la exposición deberán poder identificar qué fuente respalda cada
afirmación.

## 7. Reflexión final

**¿Por qué un desarrollador web debería mantenerse informado sobre las
vulnerabilidades de los componentes que utiliza, incluso cuando no
participa directamente en su desarrollo?**

Relacionen la respuesta con los siguientes conceptos:

-   Gestión de riesgos.
-   Cadena de suministro de software.
-   Mantenimiento y actualización de componentes.
-   Desarrollo seguro.
-   Auditoría y gestión de incidentes.

------------------------------------------------------------------------

## 8. Distribución del trabajo por equipos

El docente podrá asignar un enfoque diferente a cada equipo para ampliar
la variedad de resultados.

  -----------------------------------------------------------------------
  Equipo                  Enfoque                 Tarea principal
  ----------------------- ----------------------- -----------------------
  1                       Análisis técnico        Investigar cómo
                                                  funcionan las
                                                  vulnerabilidades y qué
                                                  componente de PHP está
                                                  involucrado.

  2                       Impacto y riesgos       Analizar qué podría
                                                  ocurrir en un servidor
                                                  web y qué activos
                                                  podrían verse
                                                  comprometidos.

  3                       Respuesta y mitigación  Investigar las
                                                  recomendaciones
                                                  oficiales y las
                                                  versiones corregidas.

  4                       Fuentes y evolución     Comparar publicaciones,
                                                  fechas, alertas y
                                                  diferencias entre la
                                                  información inicial y
                                                  las actualizaciones
                                                  posteriores.
  -----------------------------------------------------------------------

Si hay más equipos, se pueden repetir los enfoques y pedirles que
comparen sus conclusiones.

## 9. Criterios de trabajo

Se tendrá en cuenta:

-   La pertinencia y confiabilidad de las fuentes consultadas.
-   La capacidad para identificar información técnica relevante.
-   La comparación crítica de distintas publicaciones.
-   La relación entre vulnerabilidad, amenaza, activo e impacto.
-   La fundamentación de las medidas recomendadas.
-   La claridad de la síntesis y de la exposición oral.

**Idea central:** investigar una vulnerabilidad no consiste solamente en
encontrar una noticia o conocer un identificador CVE. Implica comprender
el problema, verificar la información, evaluar sus consecuencias y
fundamentar decisiones de seguridad.
