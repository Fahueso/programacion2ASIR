
## El concepto de `JAVA_HOME`

Para que el sistema operativo y otras aplicaciones (como Tomcat, Maven o IntelliJ) sepan dónde está instalado el Kit de Desarrollo de Java (JDK), no basta con que el comando `java` funcione. Necesitan una referencia absoluta al directorio raíz de la instalación. Esa referencia es la variable de entorno **`JAVA_HOME`**.

### 1. ¿Qué es exactamente `JAVA_HOME`?
`JAVA_HOME` es una variable de entorno que apunta a la carpeta principal donde reside la instalación de Java. 

**Ejemplo de rutas típicas:**
*   **En Linux:** `/usr/lib/jvm/java-17-openjdk-amd64`
*   **En Windows:** `C:\Program Files\Java\jdk-17`

Dentro de esa carpeta, la JVM espera encontrar una estructura fija: una carpeta `bin` (con los ejecutables), una carpeta `lib` (con las librerías) y otras carpetas de configuración.

### 2. La diferencia entre `JAVA_HOME` y el `PATH`
Este es el punto donde más confusiones hay. No son lo mismo:

*   **El `PATH`**: Es una lista de carpetas donde el sistema busca ejecutables. Si añades `JAVA_HOME/bin` al `PATH`, puedes escribir `java` en cualquier terminal y el sistema lo encontrará. **El PATH es para el usuario.**
*   **`JAVA_HOME`**: Es una variable que usan **otras aplicaciones**. Por ejemplo, si instalas un servidor de aplicaciones, este no busca el comando `java` en el PATH, sino que pregunta: *"¿Dónde está la variable `JAVA_HOME`?"* para saber qué versión de Java usar y dónde están las librerías internas. **El JAVA_HOME es para el software.**

### 3. Configuración en el Servidor (Linux)

Para un SysAdmin, configurar `JAVA_HOME` correctamente es vital para evitar que el servidor use la versión equivocada de Java.

#### Configuración Temporal (Solo para la sesión actual):
```bash
export JAVA_HOME=/usr/lib/jvm/java-17-openjdk-amd64
export PATH=$JAVA_HOME/bin:$PATH
```

#### Configuración Permanente (Para todos los usuarios):
Se debe añadir al archivo `/etc/profile` o `/etc/environment`:
```bash
# Añadir al final del archivo /etc/profile
export JAVA_HOME=/usr/lib/jvm/java-17-openjdk-amd64
export PATH=$JAVA_HOME/bin:$PATH
```

### 4. ¿Cómo verificar que está bien configurado?
Para comprobar que el sistema reconoce la variable y que apunta a la versión correcta, ejecuta:

```bash
echo $JAVA_HOME
```
Y para comprobar que el ejecutable coincide con esa ruta:
```bash
java -version
```

### 📌 Resumen para los apuntes:
*   **`JAVA_HOME`**: Directorio raíz de la instalación de Java.
*   **Uso**: Obligatorio para que herramientas externas (servidores, IDEs, build tools) encuentren la JVM.
*   **Relación**: `JAVA_HOME` $\rightarrow$ apunta a la carpeta $\rightarrow$ la carpeta `/bin` se añade al `PATH` $\rightarrow$ el comando `java` funciona.