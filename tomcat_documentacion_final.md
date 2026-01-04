# Documentación final de Tomcat

## Arquitectura básica de Tomcat
  1. Componentes principales:
      * **Catalina**: Motor de servlet que implementa el ciclo de vida de los servlets y maneja las solicitudes HTTP.
      * **Coyote**: Conector HTTP que permite que Tomcat funcione como un servidor web independiente.
      * **Jasper**: Motor de JSP encargado de compilar y ejecutar páginas JSP.
      * **Cluster**: Componente opcional que permite la configuración de balanceo de carga y replicación de sesiones.
      * **Valve y Realm**: Componentes para seguridad y filtrado de solicitudes.
  2. Flujo de solicitud:
      * El cliente realiza una solicitud HTTP.
      * Coyote recibe la solicitud y la pasa a Catalina.
      * Catalina determina qué servlet o JSP debe procesar la solicitud.
      * El servlet/JSP genera la respuesta.
      * La respuesta se devuelve al cliente a través de Coyote.

## Configuración del servidor
Tomcat se configura principalmente mediante archivos XML ubicados en el directorio `conf`. Estos archivos son:
  * **server.xml**: Configuración global del servidor (conectores, hosts, puertos).
  * **web.xml**: Configuración de aplicaciones web (mapeos de servlets, filtros, seguridad).
  * **context.xml**: Configuración de contexto para aplicaciones específicas.
  * **tomcat-users.xml**: Gestión de usuarios y roles para administración y acceso.

## Integración con servidor web
Tomcat se puede integrar con servidores web mediante conectores:
  * **mod_jk**: Conector AJP para integración con Apache HTTPD.
  * **mod_proxy_ajp** o **mod_proxy_http**: Alternativa basada en proxy inverso.

Esta integración permite:
  * Balanceo de carga.
  * Servir contenido estático con Apache y dinámico con Tomcat.
  * Mayor seguridad y control de acceso.

## Seguridad aplicada
Tomcat ofrece varias medidas de seguridad:
  * Autenticación y autorización mediante tomcat-users.xml y Realms.
  * Conexiones seguras (HTTPS) usando certificados SSL en el conector.
  * Roles y permisos para administrar el acceso a la consola.
  * Valves de seguridad para control de IP, limitación de accesos y protección contra ataques.

## Pruebas de rendimiento
Para evaluar el rendimiento de Tomcat se pueden utilizar herramientas como:
  * **Apache JMeter**: Generación de carga simulada y pruebas de estrés.
  * **Gatling**: Pruebas de carga avanzadas con escenarios complejos.
  * **Monitorización interna**: Manager y JMX para revisar el uso de hilos, conexiones activas y el tiempo de respuesta de servlets.
Como buenas prácticas:
  * Habilitar thread pool adecuado (maxThreads) según la carga.
  * Configurar keep-alive y compresión HTTP para optimizar rendimiento.
  * Evitar sesiones innecesarias en aplicaciones que no lo requieran.

## Recomendaciones de administración
  * Mantener Tomcat actualizado con los últimos parches.
  * Hacer copias de seguridad regulares de:
    * conf/
    * webapps/
    * logs/
  * Monitorear logs (catalina.out, localhost.log) para detectar errores.
  * Configurar alertas de uso de memoria y CPU mediante JMX o herramientas externas.
  * Separar Tomcat de la base de datos y otros servicios críticos para mejorar seguridad y rendimiento.

## Despliegue en contenedores
Tomcat es ideal para contenedores Docker debido a su ligereza y portabilidad. Ventajas de usar contenedores son:
  * Aislamiento de la aplicación y el servidor.
  * Despliegue reproducible en diferentes entornos.
  * Fácil escalado horizontal con Kubernetes u otros orquestadores.
