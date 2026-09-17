Este es un detalle fundamental. Si tus alumnos ya están acostumbrados a estructurar sus scripts de Python con `def main()` y el bloque `if __name__ == "__main__":`, el salto a Java será **mucho más natural**, ya que Java obliga a hacer exactamente lo mismo (tener un punto de entrada definido).

He actualizado los apuntes para resaltar que el `public static void main` de Java es el equivalente directo a esa estructura de Python.

---

# UD1 — Introducción a la programación. Lenguaje Java

!!! abstract "¿Qué aprenderás en esta unidad?"
    - Entender qué es un programa, un algoritmo y cómo se relacionan.
    - Conocer el ciclo de vida del software.
    - Distinguir entre compiladores e intérpretes, y entender el modelo híbrido de Java.
    - Manejar variables, constantes y tipos de datos (Tipado Dinámico vs. Estático).
    - Escribir y evaluar expresiones con operadores aritméticos, relacionales y lógicos.
    - Escribir tus primeros programas en Java: entrada, procesamiento y salida.

---

## 1. Conceptos fundamentales

### 1.1 Programador y usuario
- Un **programador/a** escribe las instrucciones que un ordenador debe seguir.
- Un **usuario/a** utiliza la aplicación resultante para obtener un resultado.

---

### 1.2 Algoritmo, programa y aplicación

| Concepto | Definición sencilla |
|---|---|
| **Algoritmo** | Secuencia finita de pasos para resolver un problema. Es la *receta*. |
| **Programa** | Algoritmo expresado en un lenguaje que entiende el ordenador. |
| **Aplicación** | Conjunto de programas que trabajan juntos para realizar una tarea compleja. |

#### Pseudocódigo: el paso intermedio
El pseudocódigo nos permite centrarnos en la **lógica** sin preocuparnos por la sintaxis estricta de ningún lenguaje.

```
INICIO
  LEER numero1
  LEER numero2
  resultado ← numero1 + numero2
  ESCRIBIR "El resultado es: ", resultado
FIN
```

---

### 1.3 Programa y procesador
Un programa consta de **Instrucciones** (acciones) y **Datos** (información).

#### Comparativa: El Punto de Entrada (Main)

En Python, aprendisteis a organizar el código usando una función `main()` y el bloque `if __name__ == "__main__":` para evitar que el código se ejecutara al importar el módulo. **En Java, esta estructura no es opcional, es obligatoria.**

=== "Python"
    ```python
    def main():
        print("¡Hola Mundo!")

    if __name__ == "__main__":
        main()
    ```

=== "Java"
    ```java
    public class HolaMundo {
        public static void main(String[] args) {
            System.out.println("¡Hola Mundo!");
        }
    }
    ```

**Análisis de la equivalencia:**
1. `public class HolaMundo`: En Java, todo debe vivir dentro de una clase.
2. `public static void main(String[] args)`: Este método es el equivalente exacto al `if __name__ == "__main__":` de Python. Es el **único lugar** donde el ordenador comienza a ejecutar el programa.
3. `System.out.println`: El comando para imprimir en consola con salto de línea.

#### Paradigmas de programación
1. **Programación estructurada** — secuencias, condicionales y bucles.
2. **Programación modular** — división en funciones/métodos.
3. **Programación orientada a objetos (POO)** — el paradigma principal de Java.

---

### 1.4 Ciclo de vida del software
*(Análisis $\rightarrow$ Diseño $\rightarrow$ Codificación $\rightarrow$ Pruebas $\rightarrow$ Mantenimiento)*.

---

### 1.5 Intérprete vs. Compilador

=== "Intérprete (Modelo Python)"
    - Traduce y ejecuta el código **línea a línea**.
    - No genera un fichero ejecutable independiente.
    - Más lento, pero más flexible para depurar.

=== "Compilador (Modelo C/C++)"
    - Traduce **todo el código de golpe** a un fichero ejecutable.
    - El programa resultante es más rápido.
    - Si hay un error, hay que recompilar todo.

---

### 1.6 Java: El modelo híbrido

Java combina ambos mundos:
1. **Compilación** — `javac` traduce `.java` $\rightarrow$ **Bytecode** (`.class`).
2. **Interpretación** — La **JVM (Java Virtual Machine)** interpreta el bytecode.

!!! success "Write Once, Run Anywhere"
    Gracias a la JVM, el mismo fichero `.class` funciona en Windows, Linux o macOS sin cambios.

---

### 1.7 Corrección de programas
- **Testing** — Pruebas de entrada y salida.
- **Debugging** — Ejecución paso a paso.

**Tipos de error:**
- **Sintaxis:** En Java, el compilador te avisa **antes** de ejecutar. En Python, muchos saltan al llegar a la línea.
- **Ejecución:** Errores en tiempo real (ej. división por cero).
- **Lógico:** El programa corre, pero el resultado es incorrecto.

---

### 1.8 ¿Qué lenguaje elegir?
*(C: Velocidad/Hardware | Java: Empresarial/Android | Python: IA/Data Science)*.

---

## 2. La información

### 2.1 ¿Qué son los datos?
Toda información se reduce a bits (0s y 1s). Usamos tipos de datos para abstraer esta complejidad.

---

### 2.2 Variables (Tipado Dinámico vs. Estático)

En Python, una variable es una etiqueta. En Java, es una **caja de tamaño y tipo fijo**.

=== "Python (Dinámico)"
    ```python
    edad = 17        # Python deduce que es un entero
    edad = "Diecisiete" # ¡Válido! La variable cambia de tipo
    ```

=== "Java (Estático)"
    ```java
    int edad = 17;   // Obligatorio decir que es 'int'
    // edad = "Diecisiete"; // ERROR DE COMPILACIÓN
    ```

---

### 2.3 Constantes

=== "Python (Convención)"
    ```python
    PI = 3.1416 # Solo es constante porque el programador lo decide
    PI = 4.0    # Python permite cambiarlo
    ```

=== "Java (Obligatorio)"
    ```java
    final double PI = 3.1416; 
    // PI = 4.0; // ERROR: El compilador impide el cambio
    ```

---

### 2.4 Nombres e identificadores
Reglas: Letras, dígitos y `_`. No empezar por número. No usar palabras reservadas.
**Convenio CamelCase en Java:** `nombreVariable` (minúscula inicial), `NombreClase` (mayúscula inicial).

---

### 2.5 Tipos de datos
- **Simples:** `edad`, `precio`, `activo`.
- **Compuestos:** `fechaNacimiento` (día, mes, año).

---

## 3. Instrucciones y Operadores

### 3.1 Expresiones
Combinación de operandos y operadores que produce un resultado.

---

### 3.2 Operadores aritméticos

| Operación | Python | Java | Nota |
|---|---|---|---|
| **Suma/Resta/Mult** | `+`, `-`, `*` | `+`, `-`, `*` | Idénticos |
| **División** | `/` (siempre float) | `/` (entera si son `int`) | En Java `5/2` es `2` |
| **División Entera** | `//` | `(int) (a / b)` | Java usa el casting |
| **Módulo (Resto)** | `%` | `%` | Idénticos |
| **Potencia** | `a ** b` | `Math.pow(a, b)` | Java usa una función |

---

### 3.3 Operadores relacionales
`>`, `<`, `==`, `!=`, `>=`, `<=` (Idénticos en ambos lenguajes).

---

### 3.4 Operadores lógicos

| Lógica | Python | Java |
|---|---|---|
| **Y (AND)** | `and` | `&&` |
| **O (OR)** | `or` | `||` |
| **NO (NOT)** | `not` | `!` |

**Ejemplo comparativo:**
=== "Python"
    ```python
    if (edad > 18) and (tiene_ticket):
        print("Entra")
    ```
=== "Java"
    ```java
    if (edad > 18 && tieneTicket) {
        System.out.println("Entra");
    }
    ```

---

### 3.5 Funciones y Métodos

=== "Python"
    ```python
    def area_triangulo(base, altura):
        return base * altura / 2
    ```

=== "Java"
    ```java
    float areaTriangulo(float base, float altura) {
        return base * altura / 2;
    }
    ```
*Nota: En Java debemos declarar el tipo de dato que devuelve la función (`float`) y el tipo de cada parámetro.*

---

## 4. El lenguaje Java

### 4.1 Ejemplos básicos: Generador de Azar

=== "Python"
    ```python
    import random

    def main():
        numero = random.randint(0, 9)
        print(f"Tu número de la suerte es: {numero}")

    if __name__ == "__main__":
        main()
    ```

=== "Java"
    ```java
    import java.util.Random;            

    public class Azar {
        public static void main(String[] args) {
            Random rd = new Random();
            int numero = rd.nextInt(10);
            System.out.println("Tu número de la suerte es: " + numero); 
        }
    }
    ```

---

### 4.2 Elementos básicos del lenguaje
- **Comentarios:** `//` (línea), `/* */` (bloque) en Java $\rightarrow$ `#` en Python.
- **Identificadores:** CamelCase en Java $\rightarrow$ snake_case en Python.

---

### 4.3 Tipos de datos en Java (Los 8 Primitivos)

Java es más específico que Python para ahorrar memoria:

| Java | Uso | Python |
|---|---|---|
| `byte`, `short`, `int`, `long` | Enteros | `int` |
| `float`, `double` | Decimales | `float` |
| `boolean` | Lógica | `bool` |
| `char` | Un carácter | `str` (de longitud 1) |

---

### 4.4 Declaración de variables y constantes

=== "Python"
    ```python
    precio = 7.25
    ```

=== "Java"
    ```java
    double precio = 7.25;
    float precio_f = 7.25f; // Requiere 'f' al final
    ```

---

### 4.5 Operadores en Java (Novedades)

Java introduce el incremento/decremento, que no existe en Python:

=== "Python"
    ```python
    x = 5
    x += 1 # x ahora vale 6
    ```

=== "Java"
    ```java
    int x = 5;
    x++; // x ahora vale 6
    ```

---

### 4.6 Conversión de tipos (Casting)

=== "Python"
    ```python
    n = int(14.67) # 14
    s = str(42)    # "42"
    ```

=== "Java"
    ```java
    int n = (int) 14.67f;    // Casting explícito (se trunca)
    String s = String.valueOf(42); // Método específico
    ```

---

### 4.7 La clase Math
Java agrupa las funciones matemáticas en `Math`.
- `Math.pow(a, b)` $\approx$ `a ** b`
- `Math.sqrt(a)` $\approx$ `math.sqrt(a)`
- `Math.random()` $\approx$ `random.random()`

---

### 4.8 Literales
- **Char:** `'a'` (comilla simple).
- **String:** `"Hola"` (comilla doble).
- **Escape:** `\n` (salto), `\t` (tabulador).

---

### 4.9 Entrada y salida estándar

#### Comparativa de lectura de datos

=== "Python"
    ```python
    def main():
        nombre = input("Nombre: ")
        edad = int(input("Edad: "))
        print(f"Hola {nombre}, tienes {edad} años")

    if __name__ == "__main__":
        main()
    ```

=== "Java"
    ```java
    import java.util.Scanner;

    public class Main {
        public static void main(String[] args) {
            Scanner sc = new Scanner(System.in);

            System.out.print("Nombre: ");
            String nombre = sc.nextLine();

            System.out.print("Edad: ");
            int edad = sc.nextInt();

            System.out.println("Hola " + nombre + ", tienes " + edad + " años");
        }
    }

---

## 📝 Resumen de la unidad

| Concepto | Java | Python |
|---|---|---|
| **Ejecución** | Compilador $\rightarrow$ JVM | Intérprete |
| **Tipado** | Estático (Obligatorio) | Dinámico (Automático) |
| **Bloques** | Llaves `{ }` | Indentación |
| **Fin línea** | Punto y coma `;` | Salto de línea |
| **Lógica** | `&&`, `||`, `!` | `and`, `or`, `not` |
| **Entrada** | `Scanner` | `input()` |
| **Punto entrada** | `public static void main` | `if __name__ == "__main__":` |