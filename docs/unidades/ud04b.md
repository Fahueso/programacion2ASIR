# Atributos y métodos estáticos (`static`)

Hasta ahora todos los atributos y métodos que hemos utilizado pertenecían a un objeto concreto.

Por ejemplo:

```java
Alumno a1 = new Alumno("Ana", 18);
Alumno a2 = new Alumno("Luis", 20);
```

Cada objeto tiene su propia edad:

```java
System.out.println(a1.getEdad()); // 18
System.out.println(a2.getEdad()); // 20
```

Sin embargo, hay ocasiones en las que cierta información pertenece a la clase completa y no a cada objeto individual.

Para ello Java proporciona la palabra reservada:

```java
static
```

---

## Atributos estáticos

Supongamos que queremos saber cuántos alumnos se han creado.

No tendría sentido guardar ese dato dentro de cada objeto.

```java
public class Alumno {

    private String nombre;

    private static int totalAlumnos = 0;

    public Alumno(String nombre) {
        this.nombre = nombre;
        totalAlumnos++;
    }

}
```

Si ejecutamos:

```java
Alumno a1 = new Alumno("Ana");
Alumno a2 = new Alumno("Luis");
Alumno a3 = new Alumno("Marta");
```

La variable compartida contendrá:

```text
3
```

Solo existe una copia de `totalAlumnos`, compartida por todos los objetos de la clase.

---

## Acceso a un atributo estático

La forma correcta es utilizar el nombre de la clase:

```java
System.out.println(
        Alumno.totalAlumnos
);
```

Aunque Java permite acceder mediante un objeto:

```java
a1.totalAlumnos;
```

no es una buena práctica porque puede dar la impresión de que el dato pertenece a ese objeto concreto.

---

## Comparativa con Python

### Python

```python
class Alumno:

    total_alumnos = 0

    def __init__(self, nombre):
        self.nombre = nombre
        Alumno.total_alumnos += 1
```

### Java

```java
public class Alumno {

    private String nombre;

    private static int totalAlumnos = 0;

    public Alumno(String nombre) {
        this.nombre = nombre;
        totalAlumnos++;
    }

}
```

El concepto es exactamente el mismo: el dato pertenece a la clase y no a cada objeto.

---

## Restricción importante

Un método estático no puede acceder directamente a atributos de instancia.

Incorrecto:

```java
public class Alumno {

    private String nombre;

    public static void mostrarNombre() {
        System.out.println(nombre);
    }

}
```

Esto produce un error de compilación.

¿Por qué?

Porque un método estático puede ejecutarse sin que exista ningún objeto.

```java
Alumno.mostrarNombre();
```

Java no sabe a qué alumno pertenece el atributo `nombre`.

---

## El método `main()` es estático

Ahora podemos comprender mejor algo que llevamos utilizando desde el principio:

```java
public static void main(String[] args)
```

El método `main()` es estático porque Java necesita ejecutarlo antes de que exista ningún objeto.

Al iniciar el programa, la JVM llama directamente a:

```java
Principal.main(args);
```

A partir de ese punto se crean los objetos necesarios.

---

# Constantes con `static final`

En muchos programas existen valores que nunca cambian.

Por ejemplo:

```java
public static final int EDAD_MINIMA = 18;
```

o

```java
public static final double IVA = 0.21;
```

La palabra reservada:

```java
final
```

impide que el valor sea modificado después de su inicialización.

Intentar hacerlo genera un error de compilación:

```java
IVA = 0.10;
```

---

## Convención de nombres

Las constantes se escriben completamente en mayúsculas, utilizando guiones bajos para separar palabras.

```java
public static final int MAX_RUEDAS = 8;

public static final double IVA = 0.21;

public static final String PAIS = "España";
```

---

## Ejemplo completo

```java
public class Vehiculo {

    public static final int RUEDAS_MINIMAS = 2;

    private String marca;

    public Vehiculo(String marca) {
        this.marca = marca;
    }

}
```

Uso:

```java
System.out.println(
        Vehiculo.RUEDAS_MINIMAS
);
```

Salida:

```text
2
```

---

## Comparativa Python vs Java

| Concepto | Python | Java |
|-----------|-----------|-----------|
| Atributo de clase | `total = 0` | `static int total = 0;` |
| Método estático | `@staticmethod` | `static` |
| Constante | Convención | `static final` |
| Acceso | `Clase.atributo` | `Clase.atributo` |

---

## Cuándo utilizar `static`

Utiliza `static` cuando el dato o comportamiento pertenece a toda la clase:

- Contadores de objetos creados.
- Métodos de utilidad matemática.
- Conversión de datos.
- Constantes compartidas.
- Método `main()`.

Evita usar `static` cuando el dato depende de cada objeto concreto.

Por ejemplo:

```java
private String nombre;
private int edad;
```

No deberían ser estáticos porque cada alumno posee valores distintos.