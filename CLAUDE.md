# CLAUDE.md — flujo de trabajo de esta web

Web académica de Rafael Gonzalez-Manzanares (academicpages / Jekyll).
Publicada en https://rafaelglezm.github.io/ vía GitHub Actions: cada `git push` a
`main` reconstruye y republica el sitio en 1-2 minutos.

## Quién hace qué (dos agentes, una sola carpeta)

Este repo lo trabajan dos agentes distintos que NO se comunican entre sí; el relevo
lo coordina Rafael y este archivo.

- **Cowork** (sandbox Linux, con la carpeta montada): se encarga del **contenido**.
  Tiene el contexto del CV de Rafael y del vault `rgm_os`. Edita los archivos de
  contenido del sitio. **No hace git push** (no tiene acceso al keychain de macOS) y
  **no debería tocar `.git/`** (ni `git add`/`commit`) para no chocar con Claude Code.
- **Claude Code** (en el Mac, con la credencial en el keychain): se encarga de
  **git y publicación**. Revisa el diff que dejó Cowork, hace `commit` + `push`.

## Archivos de contenido (lo que edita Cowork)

- `_config.yml` — datos generales del sitio y bio del autor.
- `_data/authors.yml` — perfil de la barra lateral (redes, email, ORCID, etc.).
- `_pages/about.md` — texto principal de portada / About.
- `_publications/` — una entrada `.md` por publicación.
- `_talks/`, `_teaching/`, `_portfolio/` — un `.md` por ítem.
- `files/` — PDF del CV y otros adjuntos.

Mantener el front-matter YAML y la estructura existentes. No cambiar el tema.
No subir datos personales que Rafael no quiera públicos.

## Convención de relevo (handoff)

Cuando Cowork termina una tanda de cambios, deja un resumen en `.handoff.md`
(gitignored, no se publica). Formato libre y breve, p. ej.:

```
2026-06-20 — Añadidas 3 publicaciones nuevas (2025-2026), actualizado About y CV.
```

Claude Code, al entrar: lee `.handoff.md`, revisa `git diff`, usa el resumen como
mensaje de commit, hace `commit` + `push`, y luego vacía `.handoff.md`.

## Publicar (solo Claude Code)

```bash
cd /Users/rafael/Documents/rafaelglezm.github.io
git status && git diff        # revisar lo que dejó Cowork
git add -A
git commit -m "<resumen del handoff>"
git push
```

Tras el push, verificar el deploy (Actions en verde) y que
https://rafaelglezm.github.io/ responde.

## Restricciones técnicas (no cambiar)

- `http.version` está fijado a `HTTP/1.1` en este repo (HTTP/2 daba HTTP 400 al
  hacer push tras un proxy). No revertir.
- Autenticación: token classic (`repo`, `workflow`) en el keychain de macOS, vía
  `git credential-osxkeychain`. No poner tokens en `.git/config` ni en la URL del
  remote.

## Si en el futuro se quiere que Cowork publique sin Claude Code

Montar en el entorno de Cowork un token propio fine-grained, limitado a este repo,
con permiso Contents: Read and write, como secreto/credencial de ese sandbox.
