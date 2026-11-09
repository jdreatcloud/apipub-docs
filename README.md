# EatCloud · API pública de donaciones (pbapi)

Documentación para que los equipos de desarrollo de los clientes se integren con EatCloud:
crear anuncios de donación, consultar su gestión y verificar códigos de gestión.

**Documentación en línea:** https://<organizacion>.github.io/<repositorio>/

## Contenido

| Archivo | Para qué sirve |
|---|---|
| `openapi.yaml` | **Fuente oficial.** Endpoints, campos, ejemplos y códigos de error en formato OpenAPI (antes llamado Swagger). |
| `index.html` | Página tipo Swagger que se publica en GitHub Pages. Lee `openapi.yaml`; no hay que editarla. |
| `insomnia/coleccion-insomnia.json` | Colección lista para importar en Insomnia, con ambientes de desarrollo y producción. |

## Inicio rápido

1. Solicite a EatCloud sus credenciales (usuario y contraseña), su `cua_master` y su `cua_user`.
   **Las credenciales se entregan por canal privado y nunca se publican aquí.**
2. Importe el archivo en su herramienta:
   - **Insomnia:** *Import → From File →* `insomnia/coleccion-insomnia.json`. En el ambiente *Base* complete
     `usuario` y `contrasena`, y elija *Desarrollo* o *Producción*.
   - **Postman u otra herramienta:** importe `openapi.yaml`.
3. Haga sus pruebas en **desarrollo** (`https://devdonantes.eatcloud.info`) antes de pasar a producción.

Todas las operaciones son `POST` a la misma URL:

```
https://devdonantes.eatcloud.info/pbapi/{cua_master}/{cua_user}   (desarrollo)
https://donantes.eatcloud.info/pbapi/{cua_master}/{cua_user}      (producción)
```

La operación se indica con el campo `_operation` del body: `create_donation`, `gestion_exitosa`,
`gestion_no_exitosa`, `gestion_pendiente` o `gestion_verificar_codigo`.

---

## Para el equipo de EatCloud

### Publicar en GitHub Pages (una sola vez)

1. Suba estos archivos a la raíz del repositorio (rama `main`).
2. *Settings → Pages → Source: Deploy from a branch →* rama `main`, carpeta `/ (root)` → *Save*.
3. En uno o dos minutos aparece la URL publicada. Reemplácela arriba en este README.

> La página de GitHub Pages es **pública**. No agregue credenciales, tokens, datos personales
> ni URLs internas a ningún archivo de este repositorio.

### Cuando la API cambie

1. Edite **solo** `openapi.yaml` (en GitHub: abrir el archivo → ✏️ → *Commit changes*).
2. Suba la versión en `info.version` (ej. `3.0.0` → `3.1.0`).
3. Agregue una línea al historial de abajo.
4. Si el cambio obliga al cliente a ajustar su integración (campo nuevo obligatorio, cambio de URL,
   cambio de formato), avísele directamente.
5. Si cambió algún request o ejemplo, regenere la colección de Insomnia o pídale a Claude que lo haga.

## Historial de cambios

| Versión | Fecha | Cambios |
|---|---|---|
| 3.0.0 | 2026-11-09 | Primera publicación: creación, consulta y verificación de código de gestión. |
