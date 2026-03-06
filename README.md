# Sitio Personal de Claudio Rojas

Sitio web personal construido con Jupyter Book.

## 🚀 Inicio Rápido

### 1. Instalar dependencias

```bash
pip install -r requirements.txt
```

### 2. Construir el sitio localmente

```bash
jupyter-book build .
```

El sitio generado estará en `_build/html/`

### 3. Ver el sitio localmente

```bash
# Opción 1: Abrir directamente
open _build/html/index.html

# Opción 2: Servidor local
cd _build/html
python -m http.server 8000
# Luego abrir: http://localhost:8000
```

## 📤 Publicar en GitHub Pages

### Opción A: Primera vez

1. Crear repositorio en GitHub llamado: `ClaudioRojasMon.github.io`

2. Subir archivos:
```bash
git init
git add .
git commit -m "Initial commit"
git branch -M main
git remote add origin https://github.com/ClaudioRojasMon/ClaudioRojasMon.github.io.git
git push -u origin main
```

3. Publicar con ghp-import:
```bash
jupyter-book build .
ghp-import -n -p -f _build/html
```

4. Tu sitio estará disponible en: `https://claudiorojasmon.github.io`

### Opción B: Actualizaciones posteriores

```bash
# 1. Editar archivos .md
# 2. Reconstruir
jupyter-book build .

# 3. Publicar
ghp-import -n -p -f _build/html
```

## 📁 Estructura del Sitio

```
.
├── _config.yml          # Configuración principal
├── _toc.yml             # Tabla de contenidos (navegación)
├── index.md             # Página de inicio
├── proyectos.md         # Proyectos
├── blog.md              # Blog (índice)
├── publicaciones.md     # Publicaciones académicas
├── contacto.md          # Información de contacto
└── requirements.txt     # Dependencias Python
```

## ✏️ Editar Contenido

Todos los archivos `.md` son texto plano en formato Markdown.

Para agregar una nueva página:
1. Crear archivo `nueva-pagina.md`
2. Agregar referencia en `_toc.yml`
3. Reconstruir con `jupyter-book build .`

## 🎨 Personalización

### Cambiar título y autor
Editar `_config.yml`:
```yaml
title: Tu Título
author: Tu Nombre
```

### Cambiar estructura de navegación
Editar `_toc.yml`

### Agregar logo
1. Agregar imagen en carpeta del proyecto
2. En `_config.yml` actualizar:
```yaml
logo: ruta/a/logo.png
```

## 📝 Agregar Posts al Blog

1. Crear carpeta `posts/` si no existe
2. Crear archivo `posts/mi-post.md`
3. Actualizar `blog.md` con link al nuevo post
4. Reconstruir

## 🔧 Troubleshooting

### Error al construir
```bash
# Limpiar build anterior
jupyter-book clean .

# Reconstruir
jupyter-book build .
```

### Cambios no se reflejan
```bash
# Forzar reconstrucción completa
jupyter-book clean .
jupyter-book build . --all
```

## 📚 Recursos

- [Documentación Jupyter Book](https://jupyterbook.org)
- [Sintaxis MyST Markdown](https://myst-parser.readthedocs.io/)
- [Galería de ejemplos](https://executablebooks.org/en/latest/gallery.html)

## 🆘 Ayuda

Si tienes problemas, revisa:
1. Mensajes de error al construir
2. Documentación oficial de Jupyter Book
3. GitHub Issues del proyecto

---

**Autor:** Claudio Rojas Monsalves  
**Email:** crojasmon@gmail.com  
**LinkedIn:** [linkedin.com/in/claudiorojasmon](https://linkedin.com/in/claudiorojasmon)
