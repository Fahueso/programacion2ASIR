# Unidad 5b. Colecciones de objetos (Conjuntos y tablas hash)
## Introducción

En la unidad anterior hemos aprendido a utilizar la clase `ArrayList` para almacenar colecciones dinámicas de objetos.

Gracias a ello hemos podido gestionar situaciones como:

- Una flota formada por muchos vehículos.
- Un vehículo compuesto por varias ruedas.
- Listados de elementos cuyo tamaño puede variar durante la ejecución.

Por ejemplo:

```java
ArrayList<Vehiculo> vehiculos =
        new ArrayList<>();
```

Sin embargo, las listas no resuelven todos los problemas.

En ocasiones es necesario garantizar que un elemento no pueda almacenarse más de una vez.

Supongamos una aplicación para gestionar vehículos.

Cada vehículo posee un identificador único.

```text
100
101
102
103
```

No tendría sentido registrar dos vehículos con el mismo identificador.

Sin embargo, una lista permite almacenar duplicados.

```java
ArrayList<Integer> ids =
        new ArrayList<>();

ids.add(100);
ids.add(100);
```

Resultado:

```text
100
100
```

Necesitamos una estructura que impida este comportamiento.

Para ello Java proporciona los conjuntos.

---

# 1. ¿Qué es un conjunto?

Un conjunto es una colección que no permite elementos duplicados.

La idea procede directamente de las matemáticas.

Por ejemplo, el conjunto:

```text
{1, 2, 3}
```

es válido.

Sin embargo:

```text
{1, 1, 2, 3}
```

no tendría sentido, ya que un elemento solo puede aparecer una vez.

Java aplica esta misma filosofía mediante la interfaz `Set`.

---

# 2. La interfaz Set

La interfaz `Set` define una colección cuyos elementos son únicos.

Forma parte del Framework de Colecciones de Java.

```text
Collection
│
├── List
│
└── Set
```

Mientras que las listas permiten duplicados, los conjuntos no.

---

# 3. La clase HashSet

La implementación más utilizada de la interfaz `Set` es `HashSet`.

Para utilizarla debemos importar las clases correspondientes.

```java
import java.util.HashSet;
import java.util.Set;
```

---

## Creación de un conjunto

```java
Set<Integer> ids =
        new HashSet<>();
```

El conjunto se crea inicialmente vacío.

---

## Añadir elementos

```java
ids.add(100);

ids.add(101);

ids.add(102);
```

Contenido:

```text
100
101
102
```

---

## Intentar añadir duplicados

```java
ids.add(100);
```

El elemento no se almacena nuevamente.

Contenido:

```text
100
101
102
```

El conjunto sigue conteniendo únicamente tres elementos.

---

# Comparación con Python

Si has trabajado previamente con Python, probablemente ya conoces los conjuntos.

Python:

```python
ids = {100, 101, 102}
```

Java:

```java
Set<Integer> ids =
        new HashSet<>();
```

Ambas estructuras persiguen el mismo objetivo: evitar elementos duplicados.

---

# 4. Operaciones básicas con HashSet

## Añadir elementos

```java
ids.add(200);
```

---

## Eliminar elementos

```java
ids.remove(200);
```

---

## Comprobar si existe un elemento

```java
ids.contains(100);
```

Resultado:

```java
true
```

---

## Obtener el número de elementos

```java
ids.size();
```

---

# 5. Recorrido de un conjunto

Aunque un conjunto no mantiene necesariamente el orden de inserción, podemos recorrer todos sus elementos.

```java
for(Integer id : ids){

    System.out.println(id);

}
```

Salida posible:

```text
100
102
101
```

Observa que el orden puede ser diferente al de inserción.

---

# 6. Aplicación práctica: identificadores de vehículos

Supongamos que nuestra empresa desea controlar los identificadores de todos los vehículos registrados.

Podemos utilizar un conjunto.

```java
Set<Integer> idsVehiculos =
        new HashSet<>();
```

Al registrar un vehículo añadiremos su identificador.

```java
idsVehiculos.add(100);
```

Si alguien intenta registrar el mismo identificador dos veces:

```java
idsVehiculos.add(100);
```

el conjunto evitará el duplicado automáticamente.

---

# 7. Conjuntos de objetos

Hasta ahora hemos almacenado valores simples.

Sin embargo, lo habitual es trabajar con objetos.

Supongamos que disponemos de la siguiente clase.

```java
public class Vehiculo {

    private int id;

    private String marca;

    private Motor motor;

}
```

Podemos crear un conjunto de vehículos.

```java
Set<Vehiculo> vehiculos =
        new HashSet<>();
```

---

# 8. El problema de los objetos duplicados

Consideremos el siguiente código.

```java
Vehiculo v1 =
        new Vehiculo(
                100,
                "Seat",
                motor);

Vehiculo v2 =
        new Vehiculo(
                100,
                "Seat",
                motor);
```

Intuitivamente podría parecer que ambos vehículos son iguales.

Sin embargo:

```java
System.out.println(
        v1.equals(v2));
```

produce:

```text
false
```

---

## ¿Por qué ocurre esto?

Para Java, ambos objetos ocupan posiciones diferentes en memoria.

```text
v1 ----> Objeto A

v2 ----> Objeto B
```

Aunque sus atributos tengan los mismos valores, siguen siendo objetos distintos.

---

# 9. El método equals()

Java utiliza el método `equals()` para determinar si dos objetos deben considerarse iguales.

Por defecto compara referencias de memoria.

Por ello dos objetos distintos producen:

```java
false
```

aunque sus atributos coincidan.

---

# 10. Redefiniendo la igualdad

En nuestro sistema un vehículo podría identificarse mediante su atributo `id`.

Dos vehículos con el mismo identificador deberían considerarse iguales.

```java
@Override
public boolean equals(Object obj){

    if(this == obj){

        return true;

    }

    if(obj == null){

        return false;

    }

    if(getClass() != obj.getClass()){

        return false;

    }

    Vehiculo otro =
            (Vehiculo) obj;

    return id == otro.id;
}
```

Ahora dos vehículos con el mismo identificador serán considerados iguales.

---

# 11. ¿Qué es una función hash?

Los conjuntos no comparan todos los objetos entre sí continuamente.

Eso sería muy costoso.

Para localizar elementos rápidamente utilizan una técnica denominada hash.

Una función hash transforma un objeto en un número entero.

```text
Vehículo
      ↓
 hashCode()
      ↓
 845721
```

Este valor permite localizar los elementos de forma eficiente.

---

# 12. El método hashCode()

Cuando redefinimos `equals()` también debemos redefinir `hashCode()`.

Ambos métodos deben ser coherentes entre sí.

Si dos objetos son iguales según `equals()`, deben producir el mismo valor hash.

Una implementación sencilla sería:

```java
@Override
public int hashCode(){

    return Objects.hash(id);

}
```

No olvides importar:

```java
import java.util.Objects;
```

---

# 13. equals() y hashCode() trabajando juntos

Cuando añadimos un objeto a un `HashSet`, Java realiza dos pasos.

## Paso 1

Obtiene el valor hash.

```text
hashCode()
```

---

## Paso 2

Si encuentra otro objeto con el mismo hash, utiliza:

```text
equals()
```

para confirmar si son realmente iguales.

El proceso puede representarse de la siguiente forma:

```text
Objeto
   │
   ▼
hashCode()
   │
   ▼
Posición hash
   │
   ▼
equals()
   │
   ▼
¿Duplicado?
```

Gracias a este mecanismo los conjuntos pueden detectar elementos repetidos con gran rapidez.

---

# 14. Evitando vehículos duplicados

Una vez redefinidos `equals()` y `hashCode()`, podemos utilizar un conjunto de vehículos.

```java
Set<Vehiculo> vehiculos =
        new HashSet<>();
```

Añadimos el primer vehículo.

```java
vehiculos.add(v1);
```

Intentamos añadir otro vehículo con el mismo identificador.

```java
vehiculos.add(v2);
```

El conjunto conservará un único vehículo.

---

# 15. Caso práctico: registro de vehículos

La siguiente clase representa un registro de vehículos.

```java
public class RegistroVehiculos {

    private Set<Vehiculo>
            vehiculos;

}
```

Constructor:

```java
public RegistroVehiculos(){

    vehiculos =
            new HashSet<>();

}
```

---

## Registrar vehículos

```java
public void registrarVehiculo(
        Vehiculo vehiculo){

    vehiculos.add(vehiculo);

}
```

Si el vehículo ya existe según las reglas definidas por `equals()` y `hashCode()`, no será añadido nuevamente.

---

## Mostrar vehículos registrados

```java
public void mostrarVehiculos(){

    for(Vehiculo vehiculo
            : vehiculos){

        System.out.println(
                vehiculo);
    }
}
```

---

# 16. Más allá de los conjuntos

Los conjuntos resultan ideales cuando necesitamos evitar duplicados.

Sin embargo, todavía presentan una limitación.

Supongamos la siguiente pregunta.

> ¿Dónde se encuentra el vehículo con identificador 100?

Con un conjunto debemos recorrer todos los elementos.

Esto nos lleva a una nueva necesidad:

```text
identificador → vehículo
```

o, de forma más general:

```text
clave → valor
```

Para resolver este problema Java proporciona las tablas hash basadas en mapas, que estudiaremos en la siguiente unidad.

---

# Resumen

- Un conjunto es una colección que no permite elementos duplicados.
- La interfaz principal es `Set`.
- La implementación más utilizada es `HashSet`.
- Los elementos se añaden mediante `add()`.
- Los elementos pueden comprobarse mediante `contains()`.
- Un `HashSet` utiliza funciones hash para localizar elementos.
- Los objetos almacenados en un conjunto deben implementar correctamente `equals()` y `hashCode()`.
- Dos objetos considerados iguales deben producir el mismo valor hash.
- Los conjuntos resultan especialmente útiles para garantizar la unicidad de los datos.
- Constituyen la base conceptual para comprender las tablas hash y estructuras más avanzadas como `HashMap`.