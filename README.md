# 📘 Práctica ED01 – Lenguajes compilados e interpretados en acción

📌 **Objetivo:** comprobar la diferencia entre ejecutar un programa interpretado (Python) y uno compilado (C), editando primero con un editor simple.

---

## 🔹 Preparación del entorno en Windows

Antes de comenzar las prácticas, instala lo necesario en tu ordenador:

### 1. Editor simple recomendado

* **Bloc de notas** (incluido en Windows) o
* **Notepad++** 👉 [https://notepad-plus-plus.org/downloads/](https://notepad-plus-plus.org/downloads/)

### 2. Instalar Python

1. Descarga desde 👉 [https://www.python.org/downloads/](https://www.python.org/downloads/)
2. Instala la versión 3.x marcando la casilla **“Add Python to PATH”**.
3. Comprueba en **CMD**:

   ```bash
   python --version
   ```

### 3. Instalar compilador C (GCC con WinLibs)

1. Entra en 👉 [https://winlibs.com/#download-release](https://winlibs.com/#download-release)
2. Descarga el archivo:

   * **GCC 15.2.0 (with POSIX threads) + MinGW-w64 13.0.0 (UCRT) – Win64 – Zip archive**
3. Descomprime el archivo en `C:\mingw64`.
4. Añade al **PATH** de Windows la ruta:

   ```
   C:\mingw64\bin
   ```

   Pasos:

   * Pulsa `Win + R`, escribe `sysdm.cpl` y pulsa Intro.
   * Entra en **Opciones avanzadas** → **Variables de entorno**.
   * Edita la variable `Path` del sistema → **Nuevo** → escribe `C:\mingw64\bin`.
   * Acepta y guarda cambios.
5. Abre **CMD** y comprueba:

   ```bash
   gcc --version
   ```

---

📌 **Notas técnicas importantes:**

* Si usas **PowerShell o Windows Terminal**, para ejecutar un programa en la carpeta actual debes escribir:

  ```powershell
  .\area.exe
  ```

  En **CMD clásico**, basta con:

  ```bash
  area.exe
  ```

* Si los acentos no se ven bien en la salida (ejemplo: “├¡rea” en vez de “área”), ejecuta antes:

  ```bash
  chcp 65001
  ```

  Esto cambia la consola a **UTF-8**, que muestra correctamente caracteres acentuados y ñ.

---

### Parte 1. Python (interpretado)

1. Abre **Notepad++** o Bloc de Notas y copia este código en `area.py` (**con error intencionado: falta una comilla**):

```python
# Calcular el área de un círculo en Python
radio = 5
area = 3.14159 * radio ** 2
print("El área del círculo es:, area)
```

2. Ejecuta en CMD:

   ```bash
   python area.py
   ```

   Observa el **mensaje de error de sintaxis** y anótalo.

3. Corrige el error (añade la comilla que falta):

```python
print("El área del círculo es:", area)
```

4. Vuelve a ejecutar y haz una **captura de pantalla** con el resultado.

---

### Parte 2. C (compilado)

1. Copia este código en `area.c` (**con error intencionado: falta punto y coma**):

```c
#include <stdio.h>

int main() {
    int radio = 5        // <-- error intencionado
    float area = 3.14159 * radio * radio;
    printf("El área del círculo es: %f\n", area);
    return 0;
}
```

2. En **CMD**, compila con:

   ```bash
   gcc area.c -o area.exe
   ```
3. Anota el **mensaje de error**.
4. Corrige el error (añade el `;` que falta), compila de nuevo y ejecuta:

   ```bash
   chcp 65001
   area.exe
   ```
5. Haz una **captura de la ejecución correcta**.

---

### Parte 3. Comparación inicial

1. ¿Cuándo se detectó el error en Python y en C?
2. ¿Qué diferencia notas entre ejecutar Python y C?

---

### Parte 4. Comparación de velocidad (con bucle)

1. Sustituye el programa en Python por este código:

```python
import time

inicio = time.time()

suma = 0
for i in range(100000000):   # cien millones
    suma += i

fin = time.time()
print("Suma final:", suma)
print("Tiempo en segundos:", fin - inicio)
```

2. Haz lo mismo en C (`bucle.c`):

```c
#include <stdio.h>
#include <time.h>

int main() {
    clock_t inicio, fin;
    inicio = clock();

    long long suma = 0;
    for (long long i = 0; i < 100000000; i++) {
        suma += i;
    }

    fin = clock();
    double tiempo = (double)(fin - inicio) / CLOCKS_PER_SEC;

    printf("Suma final: %lld\n", suma);
    printf("Tiempo en segundos: %f\n", tiempo);
    return 0;
}
```

Primero debes compilar el programa en C, como ya hemos visto anteriormente:

```bash
gcc bucle.c -o bucle.exe
```

Después ejecuta ambos programas:

```bash
python bucle.py

bucle.exe
```

3. Haz una captura de los tiempos medidos en Python y en C.
4. Reflexiona: ¿qué lenguaje tardó más? ¿por qué crees que ocurre?

---

📌 **Entrega**:

* Entrega un documento con:

  * Capturas de pantalla de las ejecuciones, con y sin errores.
  * Respuestas a las reflexiones.

