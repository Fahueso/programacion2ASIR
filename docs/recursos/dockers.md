# Guía de Operaciones: Despliegue de Java con Docker

Este documento tiene como objetivo proporcionar al Administrador de Sistemas las herramientas necesarias para empaquetar, ejecutar y monitorizar aplicaciones Java utilizando contenedores, asegurando la estabilidad del servidor y la eficiencia de los recursos.

## 1. ¿Por qué Containerizar Java? (El enfoque de Operaciones)

Ejecutar una aplicación Java directamente sobre el sistema operativo ("Bare Metal") presenta riesgos operativos. La containerización con Docker soluciona los cuatro problemas principales de la infraestructura:

### A. Aislamiento de Dependencias (Dependency Hell)
En un servidor tradicional, instalar varias versiones de Java (ej. Java 8 y Java 17) para diferentes aplicaciones provoca conflictos de rutas y variables de entorno (`JAVA_HOME`).
*   **Solución Docker:** Cada contenedor es una burbuja independiente. La aplicación A puede llevar Java 8 y la aplicación B Java 17 en el mismo servidor sin enterarse la una de la otra.

### B. Control Estricto de Recursos (El Muro de RAM)
Java es conocido por intentar reservar la mayor cantidad de memoria posible. Un error de configuración en el Heap (`-Xmx`) puede provocar que la aplicación consuma toda la RAM del servidor, provocando que el sistema operativo colapse.
*   **Solución Docker:** Docker impone un límite físico. Si definimos un límite de 512MB, el contenedor no puede excederlo, protegiendo la estabilidad del resto del servidor.

### C. Portabilidad e Inmutabilidad
El despliegue tradicional depende de que el servidor de destino esté configurado exactamente igual que el de pruebas.
*   **Solución Docker:** La imagen es inmutable. Lo que se probó en el entorno de desarrollo es exactamente lo mismo que se despliega en producción. Se elimina el riesgo de "en mi máquina funcionaba".

### D. Ciclo de Vida Limpio
Las instalaciones manuales dejan residuos (archivos temporales, logs dispersos, configuraciones huérfanas).
*   **Solución Docker:** Los contenedores son efímeros. Para actualizar o limpiar, se destruye el contenedor y se lanza uno nuevo. El servidor permanece limpio.

---

## 2. Anatomía del Dockerfile para Java (Nivel Operativo)

Para un SysAdmin, el Dockerfile no es código, es una **receta de infraestructura**. Para aplicaciones donde ya disponemos del archivo `.jar`, utilizamos la siguiente estructura optimizada:

```dockerfile
# 1. Imagen Base: JRE ligero sobre Alpine Linux
# Usamos JRE (Runtime) en lugar de JDK para reducir peso y aumentar seguridad
FROM eclipse-temurin:17-jre-alpine

# 2. Directorio de Trabajo
# Evitamos usar la raíz del sistema para mantener el orden
WORKDIR /app

# 3. Transferencia del Artefacto
# Copiamos el archivo compilado desde el host al contenedor
COPY MiPrograma.jar app.jar

# 4. Tuning de la JVM para Contenedores
# Definimos variables de entorno para que Java sea consciente de Docker
ENV JAVA_OPTS="-XX:+UseContainerSupport -XX:MaxRAMPercentage=75.0"

# 5. Punto de Entrada
# Ejecutamos la app usando las variables de tuning definidas arriba
ENTRYPOINT ["sh", "-c", "java $JAVA_OPTS -jar app.jar"]
```

### Análisis de los puntos clave para el administrador:
*   **`jre-alpine`**: Reduce la imagen de ~300MB a ~100MB. Menos espacio en disco y despliegues más rápidos.
*   **`UseContainerSupport`**: Es el flag más importante. Evita que la JVM ignore los límites de RAM de Docker y cause un crash del sistema.
*   **`MaxRAMPercentage=75.0`**: En lugar de fijar un valor como `-Xmx512m`, le decimos a Java que use el 75% de la RAM que el administrador le asigne al contenedor en el momento del arranque.

---

## 3. Gestión del Ciclo de Vida y Ejecución

Dependiendo de la naturaleza de la aplicación, el administrador debe elegir la estrategia de ejecución adecuada:

### A. Tareas Efímeras (Jobs / Scripts)
Para programas que realizan una tarea y luego terminan.
*   **Comando:** `docker run --rm -m 256m mi-app-java`
*   **Clave:** El flag `--rm` elimina el contenedor automáticamente al finalizar, evitando la acumulación de "contenedores zombie".

### B. Servicios Permanentes (API / Web / Backend)
Para aplicaciones que deben estar activas 24/7.
*   **Comando:** `docker run -d --name mi-servicio --restart always -m 512m mi-app-java`
*   **Claves:**
    *   `-d`: Ejecuta en segundo plano (detached).
    *   `--restart always`: Asegura que la app vuelva a subir si el servidor se reinicia o si la app peta.
    *   `-m 512m`: Establece el límite físico de RAM.

### C. Operaciones de Mantenimiento
*   **Ver logs en tiempo real:** `docker logs -f mi-servicio`
*   **Detener el servicio:** `docker stop mi-servicio`
*   **Reiniciar el servicio:** `docker restart mi-servicio`
*   **Entrar al contenedor para inspección:** `docker exec -it mi-servicio sh`

---

## 4. Matriz de Decisión: Ejecución Directa vs Docker

| Situación | Ejecución Directa (`java -jar`) | Ejecución en Docker | Recomendación SysAdmin |
| :--- | :--- | :--- | :--- |
| **Múltiples versiones de Java** | Conflictos de `JAVA_HOME` | Aislamiento total | **Docker** |
| **Control de RAM** | Basado en confianza (`-Xmx`) | Límite físico forzado | **Docker** |
| **Actualización de App** | Reemplazo manual de archivos | Cambio de imagen y restart | **Docker** |
| **Seguridad** | Riesgo de acceso root al SO | Usuario limitado en contenedor | **Docker** |
| **Velocidad de despliegue** | Lenta (Instalar $\rightarrow$ Configurar) | Instantánea (`docker run`) | **Docker** |