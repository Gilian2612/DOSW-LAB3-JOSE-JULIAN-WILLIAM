### William Ruiz
### Julian Tinjaca 
### Jose Garcia 

# ¿Cómo descargar un repositorio de GitHub a tu PC?

Existen dos formas principales para descargar un repositorio de GitHub: usando Git o descargando un archivo ZIP.

---

## Opción 1: Descargar usando Git (recomendado)

### Paso 1: Instalar Git

Descarga e instala Git desde:

[Git Official Website](https://git-scm.com/?utm_source=chatgpt.com)

---

### Paso 2: Copiar el enlace del repositorio

1. Ingresa al repositorio en GitHub.
2. Haz clic en el botón verde **“Code”**.
3. Copia el enlace HTTPS del repositorio.

Ejemplo:

```bash id="g7f2k1"
https://github.com/usuario/proyecto.git
```

---

### Paso 3: Abrir la terminal o Git Bash

Ubícate en la carpeta donde deseas descargar el proyecto.

Ejemplo:

```bash id="h3j9m2"
cd Documents
```

---

### Paso 4: Clonar el repositorio

Ejecuta el siguiente comando:

```bash id="k8p4q6"
git clone https://github.com/usuario/proyecto.git
```

---

### Resultado

Git descargará todos los archivos del proyecto en una carpeta con el nombre del repositorio.

---

## Opción 2: Descargar como ZIP

1. Entrar al repositorio en GitHub.
2. Hacer clic en el botón **“Code”**.
3. Seleccionar **“Download ZIP”**.
4. Extraer el archivo ZIP en tu computadora.

---

## Comandos útiles

```bash id="m5x7r9"
git clone URL_DEL_REPOSITORIO
cd nombre-del-proyecto
git status
```

---

## Ventajas de usar Git Clone

* Permite actualizar el proyecto fácilmente.
* Conserva el historial de cambios.
* Facilita colaborar con otros desarrolladores.
* Permite usar ramas y pull requests.
