
# 📘 Práctica ED01 – Lenguajes compilados e interpretados en acción (versión Linux)

---

## 🔹 Preparación del entorno en Linux

Antes de comenzar las prácticas, instala lo necesario en tu ordenador:

### 1. Crear carpeta de trabajo

1. Abre la **Terminal**.
2. Ejecuta:

   ```bash
   mkdir ~/MisProyectos
   cd ~/MisProyectos
   ```
3. A partir de ahora, guarda aquí todos los programas de la práctica.

📌 **Nota importante:**
En Ubuntu, al igual que en macOS, es mejor **no trabajar en las carpetas Descargas, Documentos o Escritorio**, ya que están pensadas para otros usos y pueden dar problemas de permisos o desorganización.
Crear `~/MisProyectos` permite mantener el código separado y organizado en un único sitio.

### 2. Editor simple recomendado

Tienes dos opciones principales para escribir tu código en **texto plano (UTF-8)**:

* **Gedit** (ya viene en muchas instalaciones de Ubuntu, pero puedes asegurarte instalándolo):

  ```bash
  sudo apt install -y gedit
  ```

* **Kate** (editor más avanzado, recomendado si quieres más funcionalidades como pestañas, búsqueda potente, minimapa de código, etc.):

  ```bash
  sudo apt update
  sudo apt install -y kate
  ```

📌 **Nota:** para esta práctica usaremos editores de texto simples o un poco vitaminados, como **Gedit o Kate**.

### 3. Instalar Python

Normalmente ya viene instalado. Compruébalo con:

```bash
python3 --version
pip3 --version
```

Si no aparece, instálalo con:

```bash
sudo apt update
sudo apt install -y python3 python3-pip
```

### 4. Instalar compilador C (GCC)

1. Instala las herramientas de compilación:

   ```bash
   sudo apt install -y build-essential
   ```
2. Comprueba:

   ```bash
   gcc --version
   ```

---

📌 **Notas técnicas importantes:**

* En Ubuntu, igual que en macOS, para ejecutar un programa en la carpeta actual debes escribir `./` delante:

  ```bash
  ./area
  ```
* No es necesario usar `chcp 65001` (eso es solo para Windows). Ubuntu ya usa UTF-8 en la terminal.

---

## Parte 1. Python (interpretado)

1. Abre **Gedit** o VS Code y copia este código en `area.py` (**con error intencionado: falta una comilla**):

```python
# Calcular el área de un círculo en Python
radio = 5
area = 3.14159 * radio ** 2
print("El área del círculo es:, area)
```

2. Ejecuta en Terminal:

   ```bash
   python3 area.py
   ```

   Observa el **mensaje de error de sintaxis** y anótalo.

3. Corrige el error (añade la comilla que falta):

```python
print("El área del círculo es:", area)
```

4. Vuelve a ejecutar y haz una **captura de pantalla** con el resultado.

---

## Parte 2. C (compilado)

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

2. En **Terminal**, compila con:

   ```bash
   gcc area.c -o area
   ```

3. Anota el **mensaje de error**.
4. Corrige el error (añade el `;` que falta), compila de nuevo y ejecuta:

   ```bash
   ./area
   ```

5. Haz una **captura de la ejecución correcta**.

---

## Parte 3. Comparación inicial

1. ¿Cuándo se detectó el error en Python y en C?
2. ¿Qué diferencia notas entre ejecutar Python y C?

---

## Parte 4. Comparación de velocidad (con bucle)

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
gcc bucle.c -o bucle
```

Después ejecuta ambos programas:

```bash
python bucle.py

./bucle
```

3. Haz una captura de los tiempos medidos en Python y en C.
4. Reflexiona: ¿qué lenguaje tardó más? ¿por qué crees que ocurre?
