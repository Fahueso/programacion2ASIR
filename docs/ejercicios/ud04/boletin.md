# Boletín de Ejercicios
# Unidad 5. Programación Orientada a Objetos en Java

## Introducción

En esta unidad has aprendido los fundamentos de la Programación Orientada a Objetos (POO) en Java. Aunque los conceptos básicos ya los conocías gracias a Python, Java introduce nuevas características como el tipado estático, los constructores, la encapsulación mediante modificadores de acceso y la organización del código en clases.

A lo largo de este boletín desarrollarás progresivamente una pequeña aplicación relacionada con el mundo de los videojuegos. El objetivo es aplicar todos los conceptos estudiados en la unidad mediante ejercicios prácticos y progresivos.

Se recomienda realizar los ejercicios en orden, ya que los últimos reutilizan conocimientos desarrollados en los primeros.

---

# Parte I. Clases, objetos y constructores

## Ejercicio 1. Primer videojuego

Crea una clase denominada `Videojuego` con los atributos:

```java
String titulo;
String genero;
double precio;
```

Implementa un constructor que permita inicializar todos los atributos.

Desde `main()`:

1. Crea un objeto de tipo `Videojuego`.
2. Inicialízalo mediante el constructor.
3. Muestra todos sus atributos por pantalla.

### Objetivos

- Declarar una clase.
- Crear objetos.
- Utilizar constructores.

---

## Ejercicio 2. Catálogo básico

Utilizando la clase anterior:

1. Crea cinco videojuegos distintos.
2. Utiliza para cada uno información diferente.
3. Muestra todos los videojuegos por pantalla.

### Ejemplo de salida

```text
Minecraft - Sandbox - 29.99 €
```

---

## Ejercicio 3. Sobrecarga de constructores

Amplía la clase `Videojuego` para incluir:

```java
public Videojuego() {
}
```

y

```java
public Videojuego(
    String titulo,
    String genero,
    double precio
) {
}
```

El constructor vacío deberá asignar valores por defecto razonables.

### Ejemplo

```text
Sin título
Desconocido
0.0
```

Prueba ambos constructores desde `main()`.

---

# Parte II. Encapsulación y getters/setters

## Ejercicio 4. Atributos privados

Modifica la clase `Videojuego` para que todos los atributos sean privados.

```java
private String titulo;
private String genero;
private double precio;
```

Intenta acceder directamente a los atributos desde `main()`.

### Cuestión

¿Qué error produce el compilador?

---

## Ejercicio 5. Getters y setters

Implementa los métodos:

```java
getTitulo()
setTitulo()

getGenero()
setGenero()

getPrecio()
setPrecio()
```

Accede a toda la información exclusivamente mediante estos métodos.

---

## Ejercicio 6. Validación del precio

Modifica:

```java
setPrecio()
```

para que el precio no pueda tomar valores negativos.

Si se intenta asignar un valor incorrecto:

1. No deberá modificarse el precio.
2. Se mostrará un mensaje informativo por pantalla.

### Ejemplo

```java
videojuego.setPrecio(-10);
```

---

## Ejercicio 7. Validación completa

Amplía la validación anterior.

Reglas:

- El título no puede estar vacío.
- El género no puede estar vacío.
- El precio no puede ser negativo.

### Importante

El constructor deberá utilizar los setters para aplicar siempre las mismas reglas.

---

# Parte III. toString()

## Ejercicio 8. Mostrando videojuegos correctamente

Añade a la clase:

```java
@Override
public String toString()
```

La salida deberá tener un formato similar al siguiente:

```text
Minecraft (Sandbox) - 29.99 €
```

---

## Ejercicio 9. Comparando resultados

Muestra por pantalla un objeto `Videojuego`:

1. Antes de implementar `toString()`.
2. Después de implementar `toString()`.

### Explica

¿Qué diferencia observas?

¿Por qué resulta más útil la segunda versión?

---

# Parte IV. Comparación de objetos

## Ejercicio 10. Comparando referencias

Escribe el siguiente código:

```java
Videojuego v1 =
    new Videojuego(
        "Minecraft",
        "Sandbox",
        29.99
    );

Videojuego v2 =
    new Videojuego(
        "Minecraft",
        "Sandbox",
        29.99
    );
```

Muestra el resultado de:

```java
v1 == v2
```

### Cuestión

¿Son el mismo objeto?

Justifica tu respuesta.

---

## Ejercicio 11. Implementando equals()

Dos videojuegos se considerarán iguales cuando tengan:

- El mismo título.
- El mismo género.

Implementa:

```java
@Override
public boolean equals(Object obj)
```

Prueba el método con varios ejemplos.

### Ejemplo

```java
Videojuego v1 =
    new Videojuego(
        "Minecraft",
        "Sandbox",
        29.99
    );

Videojuego v2 =
    new Videojuego(
        "Minecraft",
        "Sandbox",
        15.00
    );
```

### Cuestión

¿Deben considerarse iguales?

Justifica tu respuesta.

---

# Parte V. Relaciones entre objetos

## Ejercicio 12. Clase Desarrolladora

Crea una nueva clase:

```java
Desarrolladora
```

con los atributos:

```java
private String nombre;
private String pais;
```

Implementa:

- Constructor.
- Getters.
- Setters.
- `toString()`.

---

## Ejercicio 13. Relación entre videojuegos y desarrolladoras

Modifica la clase `Videojuego`.

Cada videojuego deberá pertenecer a una desarrolladora.

```java
private Desarrolladora desarrolladora;
```

Actualiza:

- Constructores.
- Getters.
- Setters.
- `toString()`.

---

## Ejercicio 14. Creación de objetos relacionados

Desde `main()`:

1. Crea varias desarrolladoras.
2. Crea varios videojuegos asociados a ellas.
3. Muestra toda la información por pantalla.

### Ejemplo

```text
Minecraft (Sandbox)
Desarrolladora: Mojang Studios
País: Suecia
```

---

## Ejercicio 15. Referencias nulas

Crea un videojuego cuya desarrolladora sea:

```java
null
```

Intenta ejecutar:

```java
videojuego.getDesarrolladora().getNombre();
```

### Cuestión

¿Qué ocurre al ejecutar el programa?

Describe el error observado.

---

## Ejercicio 16. Evitando errores con null

Modifica el ejercicio anterior.

Antes de acceder a los datos de la desarrolladora, comprueba que existe:

```java
if (videojuego.getDesarrolladora() != null)
```

Si no existe desarrolladora asociada, muestra un mensaje informativo.

### Ejemplo

```text
Este videojuego todavía no tiene desarrolladora asignada.
```

---



# Proyecto Final
## Ejercicio 17. Catálogo de videojuegos

Desarrolla una aplicación formada por las siguientes clases.

### Clase Desarrolladora

Atributos mínimos:

- nombre
- pais

### Clase Videojuego

Atributos mínimos:

- titulo
- genero
- precio
- desarrolladora

### Requisitos obligatorios

#### Constructores

Todas las clases deberán disponer de constructores adecuados.

#### Encapsulación

Todos los atributos deberán declararse mediante:

```java
private
```

#### Getters y setters

Los datos deberán consultarse y modificarse únicamente mediante métodos públicos.

#### Validación

Como mínimo:

- El título no puede estar vacío.
- El género no puede estar vacío.
- El precio no puede ser negativo.
- El nombre de la desarrolladora no puede estar vacío.

#### Métodos especiales

Implementar:

```java
toString()
```

y

```java
equals()
```

en la clase `Videojuego`.

#### Elementos estáticos

Añade a la clase `Videojuego`:

```java
private static int totalVideojuegos = 0;
```

El contador deberá incrementarse cada vez que se cree un objeto `Videojuego`.

Implementa además:

```java
public static int getTotalVideojuegos()
```

que devuelva el número total de videojuegos creados.

Añade también la constante:

```java
public static final double IVA = 0.21;
```

e implementa:

```java
public double getPrecioConIva()
```

que devuelva el precio final aplicando el IVA al precio base.

#### Relaciones

Cada videojuego deberá pertenecer a una desarrolladora.

### Programa principal

Desde `main()`:

1. Crea al menos tres desarrolladoras.
2. Crea al menos seis videojuegos.
3. Muestra toda la información.
4. Compara varios videojuegos utilizando `equals()`.
5. Comprueba el funcionamiento de las validaciones.
6. Comprueba el comportamiento cuando una desarrolladora vale `null`.
7. Muestra el número total de videojuegos creados utilizando `Videojuego.getTotalVideojuegos()`.
8. Muestra el precio con IVA de varios videojuegos utilizando `getPrecioConIva()`.
