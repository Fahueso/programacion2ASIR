# Ejercicios de Estructuras Condicionales


## Actividad 1: Simulador de Cajero Automático (ATM)

Esta primera actividad se centra en el uso de estructuras condicionales anidadas (`if`, `else if`, `else`).

### Descripción del Problema
Desarrollar una aplicación de consola que simule la interfaz de un cajero automático. El sistema debe validar la identidad del usuario mediante un PIN y permitir la gestión de un saldo inicial.

**Requerimientos:**

1. **Autenticación:** Solicitar un PIN. Si es correcto (1234), se concede acceso al menú; de lo contrario, el programa finaliza.
2. **Menú de Operaciones:**
   - **Opción 1: Consultar Saldo** -> Muestra el saldo actual.
   - **Opción 2: Depositar Dinero** -> Suma un monto al saldo (Validar que sea mayor a 0).
   - **Opción 3: Retirar Dinero** -> Resta un monto al saldo.
     - Validación A: El monto no puede ser mayor al saldo disponible.
     - Validación B: El monto debe ser mayor a 0.
   - **Opción 4: Salir** -> Finaliza la ejecución.
3. **Manejo de Errores:** Informar si la opción seleccionada no es válida.

### Ejemplo de Referencia (Python)
```python
saldo = 1000.0
pin_correcto = "1234"

print("--- BIENVENIDO AL BANCO PYTHON ---")
intento_pin = input("Ingrese su PIN de seguridad: ")

if intento_pin == pin_correcto:
    print("\nPIN Correcto. Acceso concedido.")
    print("\n1. Consultar Saldo\n2. Depositar\n3. Retirar\n4. Salir")
    
    opcion = input("\nSeleccione una opción: ")

    if opcion == "1":
        print(f"Su saldo actual es: ${saldo}")
    elif opcion == "2":
        deposito = float(input("Cantidad a depositar: "))
        if deposito > 0:
            saldo += deposito
            print(f"Depósito exitoso. Nuevo saldo: ${saldo}")
        else:
            print("Error: Cantidad no válida.")
    elif opcion == "3":
        retiro = float(input("Cantidad a retirar: "))
        if retiro <= 0:
            print("Error: Cantidad no válida.")
        elif retiro > saldo:
            print("Error: Fondos insuficientes.")
        else:
            saldo -= retiro
            print(f"Retiro exitoso. Saldo restante: ${saldo}")
    elif opcion == "4":
        print("Gracias por usar nuestros servicios.")
    else:
        print("Opción no válida.")
else:
    print("PIN Incorrecto. Acceso denegado.")
```

!!! warning "Entrega Actividad 1"
    - Archivo .py e implementación traducida a Java.

---

## Actividad 2: Conversor de Unidades de Medida

En esta actividad practicaremos la transición de estructuras `if-elif` hacia la estructura `switch`, la cual es más eficiente para manejar menús de opciones fijas.

### Descripción del Problema
Desarrollar una aplicación que permita convertir una cantidad de metros a otras unidades de longitud mediante un menú de opciones.

**Requerimientos:**

1. **Entrada de Datos:** Solicitar una cantidad en metros (decimal). Validar que no sea negativa.
2. **Menú de Conversión:**
   - **Opción 1: Centímetros** -> (Metros * 100)
   - **Opción 2: Milímetros** -> (Metros * 1000)
   - **Opción 3: Kilómetros** -> (Metros / 1000)
   - **Opción 4: Pulgadas** -> (Metros * 39.37)
   - **Opción 5: Salir** -> Finaliza el programa.
3. **Manejo de Errores:** Informar si la opción seleccionada no es válida.

### Ejemplo de Referencia (Python)
```python
print("--- CONVERSOR DE LONGITUD ---")
metros = float(input("Ingrese la cantidad en metros: "))

if metros < 0:
    print("Error: La medida no puede ser negativa.")
else:
    print("\nSeleccione la unidad de destino:")
    print("1. Centímetros\n2. Milímetros\n3. Kilómetros\n4. Pulgadas\n5. Salir")
    
    opcion = input("\nOpción: ")

    if opcion == "1":
        print(f"Resultado: {metros * 100} cm")
    elif opcion == "2":
        print(f"Resultado: {metros * 1000} mm")
    elif opcion == "3":
        print(f"Resultado: {metros / 1000} km")
    elif opcion == "4":
        print(f"Resultado: {metros * 39.37} in")
    elif opcion == "5":
        print("Saliendo del programa...")
    else:
        print("Opción no válida.")
```

!!! warning "Entrega Actividad 2"
    - Archivo .py e implementación en Java utilizando obligatoriamente la estructura **switch**.
