# Ejercicios propuestos

## Ejercicio 1. De Python a Java

Observa esta función en Python:

```python
def cuadrado(n):
    return n * n
```

Escribe su equivalente en Java.

### Solución

```java
public static int cuadrado(int n) {
    return n * n;
}
```

---

## Ejercicio 2. Método sin retorno

Escribe un método llamado `saludar` que reciba un nombre y muestre:

```text
Hola Francisco
```

### Solución

```java
public static void saludar(String nombre) {
    System.out.println("Hola " + nombre);
}
```

Uso:

```java
saludar("Francisco");
```

---

## Ejercicio 3. Calculadora sencilla

Crea un método llamado `sumar` que reciba dos números enteros y devuelva la suma.

### Solución

```java
public static int sumar(int a, int b) {
    return a + b;
}
```

---

## Ejercicio 4. Número mayor

Haz un método que reciba dos enteros y devuelva el mayor.

### Solución

```java
public static int mayor(int a, int b) {

    if (a > b) {
        return a;
    }

    return b;
}
```

---

## Ejercicio 5. Es par

Crea un método que reciba un número y devuelva `true` si es par y `false` en caso contrario.

### Solución

```java
public static boolean esPar(int n) {
    return n % 2 == 0;
}
```

---

## Ejercicio 6. Contar caracteres

Crea un método que reciba una cadena y devuelva el número de caracteres.

### Solución

```java
public static int longitud(String texto) {
    return texto.length();
}
```

---

## Ejercicio 7. Intercambio imposible

¿Qué mostrará este programa?

```java
public static void intercambiar(int a, int b) {

    int aux = a;
    a = b;
    b = aux;

}
```

```java
int x = 5;
int y = 10;

intercambiar(x, y);

System.out.println(x);
System.out.println(y);
```

### Solución

```text
5
10
```

Las variables originales no cambian porque los parámetros reciben una copia de los valores.

---

## Ejercicio 8. Modificar un array

¿Qué mostrará este programa?

```java
public static void modificar(int[] numeros) {
    numeros[0] = 999;
}
```

```java
int[] datos = {1, 2, 3};

modificar(datos);

System.out.println(datos[0]);
```

### Solución

```text
999
```

---

## Ejercicio 9. Error de compilación

Indica qué error tiene el siguiente código:

```java
public static void prueba() {

    int x = 10;

}

public static void main(String[] args) {

    System.out.println(x);

}
```

### Solución

La variable `x` solo existe dentro del método `prueba()`. Fuera de él no puede utilizarse.

---

## Ejercicio 10. Variable local

¿Qué valor se mostrará?

```java
public static void metodo() {

    int numero = 20;

    System.out.println(numero);

}
```

```java
int numero = 50;

metodo();

System.out.println(numero);
```

### Solución

```text
20
50
```

Cada variable pertenece a un ámbito diferente.

---

## Ejercicio 11. Estadísticas de notas

Diseña los siguientes métodos:

```java
calcularMedia()
obtenerMayor()
obtenerMenor()
```

El programa trabajará con:

```java
double[] notas = {7.5, 8, 9, 4, 6};
```

Y mostrará:

```text
Media: 6.9
Mayor: 9.0
Menor: 4.0
```

### Solución

```java
public static double calcularMedia(double[] notas) {

    double suma = 0;

    for (double nota : notas) {
        suma += nota;
    }

    return suma / notas.length;
}
```

```java
public static double obtenerMayor(double[] notas) {

    double mayor = notas[0];

    for (double nota : notas) {

        if (nota > mayor) {
            mayor = nota;
        }

    }

    return mayor;
}
```

```java
public static double obtenerMenor(double[] notas) {

    double menor = notas[0];

    for (double nota : notas) {

        if (nota < menor) {
            menor = nota;
        }

    }

    return menor;
}
```

---

# Reto final

Dada esta función Python:

```python
def contar_pares(lista):
    contador = 0

    for n in lista:
        if n % 2 == 0:
            contador += 1

    return contador
```

Tradúcela a Java.

### Solución

```java
public static int contarPares(int[] lista) {

    int contador = 0;

    for (int n : lista) {

        if (n % 2 == 0) {
            contador++;
        }

    }

    return contador;
}
```