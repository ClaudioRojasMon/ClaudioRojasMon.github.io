# 🚀 Guía para actualizar tu sitio web
**claudiorojasmon.github.io**

---

## 📁 Ubicación del proyecto

```bash
cd ~/Documents/Proyectos-myst/sitio-personal-claudio
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
| `_toc.yml` | Menú de navegación |
| `_config.yml` | Configuración general del sitio |

---

## ✏️ Flujo para hacer cambios

### Paso 1 — Ir a la carpeta del proyecto
```bash
cd ~/Documents/Proyectos-myst/sitio-personal-claudio
```

### Paso 2 — Editar los archivos en VS Code
Abre la carpeta en VS Code y edita el archivo que necesites.
Guarda siempre con **Cmd + S**.

### Paso 3 — Construir y publicar
```bash
jupyter-book build . --all && ghp-import -n -p -f _build/html
```

Espera 2-3 minutos y los cambios aparecerán en el sitio.

---

## 🆕 Agregar un nuevo artículo al blog

### 1. Crear el archivo
```bash
touch posts/nombre-del-articulo.md
```

### 2. Estructura del artículo
```markdown
# Título del artículo

*Fecha de publicación*

---

📄 *Este artículo es un resumen. Para leer el análisis completo:*

👉 [Leer artículo completo en LinkedIn](https://www.linkedin.com/...)

---

## Introducción

Contenido del artículo...
```

### 3. Agregar al blog.md
Abre `blog.md` y agrega la entrada en la sección correspondiente:

```markdown
### Título del artículo
Descripción breve de una o dos líneas.

[Leer artículo](posts/nombre-del-articulo)

**Temas:** Tema1, Tema2, Tema3
```

### 4. Publicar
```bash
jupyter-book build . --all && ghp-import -n -p -f _build/html
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

---

## 🔧 Comandos útiles

| Comando | Para qué sirve |
|---|---|
| `jupyter-book build . --all` | Construye todo el sitio desde cero |
| `ghp-import -n -p -f _build/html` | Publica en GitHub Pages |
| `rm -rf _build` | Borra caché del build (usar si algo no actualiza) |
| `cat nombre-archivo.md` | Ver contenido de un archivo en terminal |
| `ls posts/` | Ver artículos del blog |
| `touch archivo.md` | Crear un archivo nuevo vacío |

---

## ⚠️ Problemas comunes

**El sitio no se actualiza después de publicar**
→ Espera 2-3 minutos y recarga con **Cmd + Shift + R**
→ O abre en ventana incógnita: **Cmd + Shift + N**

**El build falla**
→ Borra el caché y vuelve a construir:
```bash
rm -rf _build && jupyter-book build . && ghp-import -n -p -f _build/html
```

**Un archivo nuevo no aparece en el menú**
→ Agrégalo al `_toc.yml`:
```yaml
chapters:
- file: nombre-archivo
```

---

*Actualizado: Febrero 2026*
