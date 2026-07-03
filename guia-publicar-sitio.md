# 🚀 Guía para actualizar tu sitio web
**claudiorojasmon.github.io**

---

## 📁 Ubicación del proyecto

```bash
cd ~/Documents/Proyectos-myst/sitio-personal-myst
```

---

## 📝 Archivos principales

| Archivo | Qué contiene |
|---|---|
| `index.md` | Página de inicio |
| `about.md` | Acerca de mí |
| `blog.md` | Índice del blog |
| `proyectos.md` | Proyectos |
| `servicios.md` | Servicios |
| `contacto.md` | Contacto |
| `posts/` | Carpeta con artículos del blog |
| `_static/` | Imágenes y CSS |
| `myst.yml` | Configuración general y menú de navegación |

---

## ✏️ Flujo para hacer cambios

### Paso 1 — Ir a la carpeta del proyecto
```bash
cd ~/Documents/Proyectos-myst/sitio-personal-myst
```

### Paso 2 — Editar los archivos en VS Code
Abre la carpeta en VS Code y edita el archivo que necesites.
Guarda siempre con **Cmd + S**.

### Paso 3 — Previsualizar localmente (opcional)
```bash
myst start
```
Abre el navegador en `http://localhost:3000` para ver los cambios antes de publicar.
Cuando termines de mirar, corta el servidor con **Ctrl + C** antes de seguir.

### Paso 4 — Construir y publicar

⚠️ **Importante:** `myst build --html` termina de compilar el sitio y **después arranca un servidor de preview que se queda corriendo para siempre** (vas a ver "Starting Book Theme" y "Server started on port 3000"). Por eso **no se puede encadenar con `&&`** — el segundo comando nunca llegaría a ejecutarse. Hacelo en dos pasos separados:

```bash
myst build --html
```
Esperá a ver `📚 Built 15 pages for project...` y a que arranque el servidor, después **Ctrl + C** para cortarlo.

```bash
ghp-import -n -p -f _build/html
```

Espera 1-2 minutos y los cambios aparecerán en el sitio. Verificá siempre en una **ventana de incógnito** (`Cmd + Shift + N`) para evitar caché vieja del navegador.

---

## 🆕 Agregar un nuevo artículo al blog

### 1. Crear el archivo
```bash
touch posts/nombre-del-articulo.md
```

### 2. Estructura del artículo
```markdown
---
title: Título corto para el menú
---

# Título completo del artículo

*Fecha de publicación*

---

Contenido del artículo...

---

**Temas:** Tema1, Tema2, Tema3
```

### 3. Agregar al myst.yml
Abre `myst.yml` y agrega el archivo bajo `children` del blog:

```yaml
    - file: blog
      children:
        - file: posts/nombre-del-articulo
```

### 4. Agregar al blog.md
Abre `blog.md` y agrega la entrada en la sección correspondiente:

```markdown
### Título del artículo
Descripción breve de una o dos líneas.

[Leer artículo](posts/nombre-del-articulo)

**Temas:** Tema1, Tema2, Tema3
```

### 5. Publicar
```bash
myst build --html
```
(Ctrl + C cuando arranque el servidor)
```bash
ghp-import -n -p -f _build/html
```

---

## 🖼️ Agregar una imagen nueva

```bash
cp ~/ruta/de/la/imagen.png _static/nombre-imagen.png
```

Y referenciarla en cualquier `.md`:
```markdown
![descripción](_static/nombre-imagen.png)
```

O con control de tamaño:
````markdown
```{image} _static/nombre-imagen.png
:width: 400px
:align: center
```
````

---

## 🔧 Comandos útiles

| Comando | Para qué sirve |
|---|---|
| `myst start` | Previsualizar el sitio en `localhost:3000` |
| `myst build --html` | Construir el sitio (termina en un servidor de preview, cortar con Ctrl+C) |
| `ghp-import -n -p -f _build/html` | Publicar en GitHub Pages |
| `rm -rf _build` | Borrar caché del build |
| `ls posts/` | Ver artículos del blog |
| `touch archivo.md` | Crear un archivo nuevo vacío |
| `git remote -v` | Ver si la URL del repo tiene algo raro pegado (ver más abajo) |

---

## 🔑 El token de GitHub expiró (Password authentication is not supported)

Si `ghp-import` te tira un error como:
```
remote: Invalid username or token. Password authentication is not supported for Git operations.
fatal: Authentication failed
```

Tu token de acceso personal expiró. Solución:

1. Andá a **github.com/settings/tokens**
2. Buscá el token llamado **"sitio-personal"** → hacé clic en su nombre → **"Regenerate token"**
3. Elegí una fecha de expiración (no "No expiration") → copiá el token nuevo (empieza con `ghp_...`) y guardalo en un lugar seguro
4. Corré `ghp-import -n -p -f _build/html` de nuevo
5. Cuando te pida usuario y contraseña:
   - **Username:** `ClaudioRojasMon`
   - **Password:** pegá el token nuevo (no se ve nada al pegarlo en la terminal, es normal)

**Fecha de expiración actual del token:** 1 de julio de 2027 — poné un recordatorio en el calendario para fines de junio 2027.

⚠️ Si en algún momento `git remote -v` muestra un token pegado directo en la URL (`https://usuario:ghp_...@github.com/...`), limpiala con:
```bash
git remote set-url origin https://github.com/ClaudioRojasMon/ClaudioRojasMon.github.io.git
```

---

## ⚠️ Problemas comunes

**El sitio no se actualiza después de publicar**
→ Espera 1-2 minutos y recarga con **Cmd + Shift + R**
→ O abre en ventana incógnita: **Cmd + Shift + N**
→ Si sigue sin aparecer, andá a `Settings → Pages` en el repo de GitHub y confirmá que "Branch" diga **`gh-pages`** (no `main`, no "GitHub Actions")

**El build falla**
→ Borra el caché y vuelve a construir:
```bash
rm -rf _build && myst build --html
```
(Ctrl + C cuando arranque el servidor, después `ghp-import -n -p -f _build/html`)

**Un archivo nuevo no aparece en el menú**
→ Agrégalo al `myst.yml` bajo `toc`:
```yaml
toc:
  - file: nombre-archivo
```

**Nota sobre despliegue:** el sitio se publica únicamente vía `ghp-import` a la rama `gh-pages`. No existe (ni debe existir) ningún GitHub Action automático — se eliminó `deploy.yml` en julio 2026 porque generaba un despliegue fantasma con una versión distinta de MyST que rompía el sitio. Si en algún momento aparece un archivo en `.github/workflows/`, hay que revisarlo con cuidado antes de dejarlo activo.

---

*Actualizado: Julio 2026*
