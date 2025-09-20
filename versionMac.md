
# 📘 Práctica ED01 – Lenguajes compilados e interpretados en acción (versión macOS)

📌 **Objetivo:** comprobar la diferencia entre ejecutar un programa interpretado (Python) y uno compilado (C), editando primero con un editor simple.

---

## 🔹 Preparación del entorno en macOS

### 1. Crear carpeta de trabajo

Antes de comenzar, crea una carpeta dentro de tu **home** (carpeta personal) para organizar todos tus proyectos.

- Abre la **Terminal** y ejecuta:

   ```bash
   mkdir ~/MisProyectos
   cd ~/MisProyectos
   ```

- Aquí guardarás todos los archivos de la práctica.

📌 **Nota importante:**
No es recomendable guardar ni ejecutar código en **Descargas, Documentos o Escritorio**, ya que desde macOS Catalina existe una capa de seguridad que puede impedir la ejecución de programas en esas carpetas.
Además, trabajar en `~/MisProyectos` te ayuda a separar claramente tu código del resto de archivos del sistema.

### 2. Instalar Homebrew

Antes de nada, instala **Homebrew**, que es un **gestor de paquetes para macOS** (similar a `apt` en Linux o `chocolatey` en Windows).

📌 **Ventajas de Homebrew:**

* Permite instalar programas fácilmente desde la terminal.
* Se actualiza con un simple comando, sin tener que descargar instaladores manualmente.
* Garantiza configuraciones correctas para Python, compiladores, editores de texto, etc.

1. Abre la aplicación **Terminal**.

2. Ejecuta:

   ```bash
   /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
   ```

3. Al terminar, Homebrew mostrará instrucciones para añadirlo al **PATH**.
   👉 **Copia y pega exactamente esas líneas** en la terminal, ya que pueden variar según el modelo de Mac (Intel o Apple Silicon).

4. Comprueba que funciona:

   ```bash
   brew --version
   ```

5. Para actualizar Homebrew más adelante:

   ```bash
   brew update
   ```

### 3. Editor simple recomendado

Para escribir código necesitamos un editor de texto en **formato plano (UTF-8)**.
En macOS se recomienda **CotEditor**, un editor sencillo, parecido a Notepad++, que guarda directamente en UTF-8 por defecto.

#### 🔹 Instalación con Homebrew (recomendada)

Si ya tienes **Homebrew** instalado, la forma más fácil es desde la terminal:

```bash
brew install --cask coteditor
```

Más adelante, para actualizar CotEditor:

```bash
brew upgrade --cask coteditor
```

#### 🔹 Instalación desde la web oficial

1. Descarga CotEditor desde 👉 [https://coteditor.com/](https://coteditor.com/).
2. Dependiendo de lo que descargues, tendrás un archivo `.zip` o `.dmg`.

**Si es `.zip`:**

1. Abre **Finder** y ve a la carpeta **Descargas**.
2. Haz **doble clic** sobre el archivo `.zip`.
3. Se descomprimirá y aparecerá la aplicación `CotEditor.app`.
4. Arrastra la aplicación a la carpeta **Aplicaciones** (en la barra lateral izquierda del Finder).
5. Una vez copiada, ya podrás abrirla desde **Launchpad** o con **Spotlight** (`⌘ + barra espaciadora`).
6. Borra el archivo `.zip` de Descargas, ya no lo necesitas.

**Si es `.dmg`:**

1. Abre **Finder** y ve a la carpeta **Descargas**.
2. Haz **doble clic** sobre el archivo `.dmg`.
3. Se abrirá una ventana que suele mostrar el icono de la aplicación y un acceso directo a la carpeta **Aplicaciones**.
4. Arrastra el icono de **CotEditor** hacia el icono de **Aplicaciones**.
5. Una vez copiada, cierra la ventana y en **Finder**, en la barra lateral, pulsa en el icono de expulsar (`⏏`) para “expulsar” la imagen de disco.
6. Borra el archivo `.dmg` de la carpeta **Descargas**, ya no lo necesitas.
7. Abre la aplicación desde **Launchpad** o con **Spotlight** (`⌘ + barra espaciadora`).

### 4. Instalar Python (con Homebrew)

1. Instala Python 3 con Homebrew:

   ```bash
   brew install python
   ```

2. Crea alias para simplificar comandos. Edita el archivo de configuración de la shell (`.zshrc`):

   ```bash
   nano ~/.zshrc
   ```

   Añade al final:

   ```bash
   alias pip="python3 -m pip"
   alias py="python3"
   alias python="python3"
   ```

   Guarda (`CTRL + O`), cierra (`CTRL + X`) y recarga la configuración:

   ```bash
   source ~/.zshrc
   ```

3. Comprueba la instalación:

   ```bash
   python --version
   pip --version
   ```

### 5. Instalar compilador C

En macOS el compilador por defecto es **clang** (equivalente a gcc en Linux).

1. Instala las herramientas de línea de comandos de Xcode:

   ```bash
   xcode-select --install
   ```
2. Comprueba:

   ```bash
   gcc --version
   ```

👉 Nota: En macOS, el comando `gcc` no corresponde al compilador GNU GCC, sino que en realidad es un enlace al compilador oficial de Apple (*Clang*). Por eso puedes usar indistintamente `gcc` o `clang`, ya que ambos ejecutan el mismo compilador en este sistema.

---

📌 **Notas técnicas importantes:**

* Para ejecutar un programa en la carpeta actual, en macOS siempre debes poner `./` delante:

  ```bash
  ./area
  ```
* En macOS **no es necesario usar `chcp 65001`**, porque la terminal ya trabaja en UTF-8 por defecto. Los acentos y ñ deberían mostrarse bien.

---

## Parte 1. Python (interpretado)

1. Abre **CotEditor** y copia este código en `area.py` (**con error intencionado: falta una comilla**):

```python
# Calcular el área de un círculo en Python
radio = 5
area = 3.14159 * radio ** 2
print("El área del círculo es:, area)
```

2. Ejecuta en Terminal:

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

---

📌 **Entrega**:

* Entrega un documento con:

  * Capturas de pantalla de las ejecuciones, con y sin errores.
  * Respuestas a las reflexiones.

