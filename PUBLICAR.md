# Cómo publicar este sitio en GitHub Pages

Este es un sitio Jekyll basado en la plantilla **academicpages**, ya rellenado con tus datos del CV. La URL final será **https://rafaelglezm.github.io**.

## 1. Crear el repositorio
1. En GitHub (cuenta `rafaelglezm`), crea un repositorio **público** llamado exactamente `rafaelglezm.github.io`. No añadas README ni .gitignore (esta carpeta ya los trae).

## 2. Subir el contenido
**Opción A (terminal, recomendada):** desde esta carpeta:

```bash
cd rafaelglezm.github.io
git init
git add .
git commit -m "Initial academicpages site"
git branch -M main
git remote add origin https://github.com/rafaelglezm/rafaelglezm.github.io.git
git push -u origin main
```

**Opción B (web):** en el repositorio vacío, usa "uploading an existing file" y arrastra todo el contenido de esta carpeta.

## 3. Activar GitHub Pages
En el repositorio: **Settings → Pages → Build and deployment → Source: GitHub Actions**. La plantilla incluye el workflow en `.github/workflows`, así que el sitio se compila solo en cada push. En 1-2 minutos estará en https://rafaelglezm.github.io.

## 4. Previsualizar en local (opcional)
Con Docker (incluido): `docker compose up` y abre http://localhost:4000. O con Ruby: `bundle install && bundle exec jekyll serve`.

---

## Puntos a revisar / completar [CHECK]
- **Foto**: sustituye `images/profile.png` (ahora es la imagen de la plantilla) por tu retrato, mismo nombre.
- **Charlas con fecha o sede aproximada** (marcadas `[CHECK]` en el cuerpo del archivo): ESC Cardio-Oncology 2025, HDR UK 2025, ponencia invitada en cardiotoxicidad, y los cursos de Cardiología para Atención Primaria. Ajusta fecha/lugar en `_talks/`.
- **Google Scholar / Scopus / ResearchGate**: si tienes perfil, añade la URL en `_config.yml` (campos `googlescholar`, `scopus`, `researchgate`) y aparecerán los iconos en la barra lateral.
- **Comunicaciones 2018-2022**: están en un Excel del dossier, no detalladas aquí. Si quieres incorporarlas, pásamelas y genero las entradas.
- **Email mostrado**: configurado como `rafael.gonzalez@imibic.org` (corresponding). Cámbialo en `_config.yml` si prefieres otro.

## Contenido generado
- About (`_pages/about.md`)
- 68 publicaciones (`_publications/`), con enlace a DOI/PubMed y marcas de autoría principal y decil 1 (D1).
- 10 charlas/congresos y moderaciones (`_talks/`).
- 8 entradas de docencia (`_teaching/`): 3 tesis dirigidas, dirección de TFG (n=17), docencia UCO, tutoría y formación SEC/HURS.
- CV (`_pages/cv.md`) con formación, afiliaciones, contratos ISCIII, premios, servicio editorial y la lista completa de TFG.
