### William Ruiz
### Julian Tinjaca 
### Jose Garcia 

# Cuestionario Teórico

---

### 01 ¿Qué es un pull request en GitHub?

Un pull request (PR) permite que un desarrollador informe a otros miembros del equipo sobre cambios que desea agregar al proyecto.

Cuando se crea un PR, los colaboradores pueden:

* Revisar el código.
* Hacer comentarios y sugerencias.
* Detectar errores.
* Aprobar o solicitar modificaciones.
* Finalmente fusionar (merge) los cambios.

#### Ejemplo

Un programador crea una nueva funcionalidad en una rama llamada `login-usuarios`. Luego abre un pull request para integrar esos cambios a la rama `main`. Antes de aceptar los cambios, otros desarrolladores revisan el código.

#### Ventajas

* Facilita el trabajo colaborativo.
* Mejora la calidad del código.
* Permite auditoría y seguimiento de cambios.
* Evita errores en la rama principal.

---

### 02 ¿Cómo se crea un pull request en GitHub?

Para crear un pull request en GitHub se siguen estos pasos:

1. Crear una rama nueva en el repositorio.
2. Realizar cambios en el código.
3. Guardar y enviar los cambios (`commit` y `push`).
4. Ingresar al repositorio en GitHub.
5. Hacer clic en el botón **“Compare & pull request”**.
6. Escribir:

   * Título del PR.
   * Descripción de los cambios realizados.
7. Seleccionar:

   * Rama origen (*source branch*).
   * Rama destino (*target branch*).
8. Hacer clic en **“Create pull request”**.

#### Comandos básicos en Git

```bash
git checkout -b nueva-rama
git add .
git commit -m "Se agrega nueva funcionalidad"
git push origin nueva-rama
```

Después de hacer `push`, GitHub mostrará la opción para crear el pull request.

---

### 03 ¿Cómo se aprueba un pull request en GitHub?

La aprobación de un pull request se realiza mediante una revisión del código.

#### Pasos para aprobar un PR

1. Abrir el pull request en GitHub.
2. Revisar los archivos modificados.
3. Hacer comentarios si es necesario.
4. Seleccionar **“Review changes”**.
5. Elegir una opción:

   * **Approve** → aprobar cambios.
   * **Request changes** → solicitar correcciones.
   * **Comment** → dejar observaciones.
6. Hacer clic en **“Submit review”**.

Finalmente, un usuario con permisos puede hacer:

* **Merge pull request**

#### Tipos de merge

* Create a merge commit
* Squash and merge
* Rebase and merge

Cada uno organiza el historial de cambios de forma distinta.

---

### 04 Bibliografía en norma APA (7.ª edición)

GitHub. (s.f.). *About pull requests*. GitHub Docs.
https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/about-pull-requests

GitHub. (s.f.). *Creating a pull request*. GitHub Docs.
https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/creating-a-pull-request

GitHub. (s.f.). *Reviewing proposed changes in a pull request*. GitHub Docs.
https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/reviewing-changes-in-pull-requests/reviewing-proposed-changes-in-a-pull-request
