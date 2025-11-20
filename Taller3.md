---
title: "Taller 3"
date: 2025-10-23
draft: false
---
# **Taller 3 --- Paradigmas de Programación**

**Alumno:** Kevin Humberto Soto Ortiz\
**Matrícula:** 377689\
**Universidad Autónoma de Baja California**\
**Facultad de Ingeniería, Arquitectura y Diseño**\
**Ingeniería en Software y Tecnologías Emergentes**

------------------------------------------------------------------------

## **Ejercicio 1**

### **Analiza el código y determina la salida del programa. Explica qué tipo de memoria se usa.**

El programa utiliza:

-   **Memoria estática**: para la variable global.
-   **Memoria automática**: para las variables locales dentro de las
    funciones.
-   **No hay memoria dinámica**, ya que no se usa `malloc` ni `free`.

------------------------------------------------------------------------

## **Ejercicio 2**

### **Analiza el código y encuentra el error relacionado con memoria dinámica.**

El error consiste en:

Se utiliza el puntero `ptr` **después de liberar la memoria** mediante
`free(ptr)`.\
Esto genera un **puntero colgante (dangling pointer)** y produce
**comportamiento indefinido**.

### **Solución:**

-   Usar la memoria **antes** de llamar a `free(ptr)`.

-   Asignar:

    ``` c
    ptr = NULL;
    ```

    después de liberarlo para evitar errores.

------------------------------------------------------------------------

## **Ejercicio 3**

### **1. ¿Cuál es la salida esperada del programa?**

-   La variable global `x` inicia en **0**.

-   El hilo ejecuta la función `incrementar()`, donde ocurre:

    ``` c
    x++;
    ```

-   Debido a que el programa usa:

    ``` c
    pthread_join(thread, NULL);
    ```

    el hilo principal **espera** a que el hilo termine.

### **Resultado final:**

**x = 1**

------------------------------------------------------------------------

### **2. ¿Qué pasa si removemos `pthread_join(thread, NULL);`?**

El hilo principal **no espera** al hilo secundario. Por lo tanto, el
comportamiento puede variar:

#### **Caso 1:**

El hilo **no alcanza** a ejecutar `x++` antes del `printf`.\
Salida:\
**Valor final de x: 0**

#### **Caso 2:**

El hilo **sí alcanza** a ejecutar `x++` a tiempo.\
Salida:\
**Valor final de x: 1**

------------------------------------------------------------------------

## **Resumen**

-   Con `pthread_join` → el valor **siempre** termina siendo **1**.\
-   Sin `pthread_join` → la salida puede ser **0** o **1**, dependiendo
    del tiempo de ejecución.
