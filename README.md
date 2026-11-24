# Arocs ELS-Kaufmann

## 1. Sube el proyecto desde GitHub web

1. Extrae el ZIP. Crea un repositorio **privado** en GitHub llamado
   `arocs-els-kaufmann`, sin marcar **Add README**.
2. En ese repositorio, usa **uploading an existing file** si está vacío.
   En las cargas siguientes, entra a **Code → Add file → Upload files**.
3. En Windows abre `01_FOTOS`. Arrastra solo su carpeta `public` al cuadro
   de carga y pulsa **Commit changes**. Repite desde la portada del mismo
   repositorio con `02_FOTOS`.
4. Abre `03_TABLERO` y arrastra todos los archivos y carpetas que hay dentro.
   Guarda el último commit en la rama `main`.
5. En la portada del repositorio deben verse `wrangler.jsonc`, `package.json`
   y las carpetas `public`, `scripts` y `src`.

## 2. Publica en Cloudflare

En **Workers & Pages → Create application → GitHub**, selecciona el repositorio nuevo.

| Campo | Valor |
|---|---|
| Worker name | `arocs-els-kaufmann` |
| Production branch | `main` |
| Root directory | Dejar vacío |
| Build command | Dejar vacío |
| Deploy command | `npm run deploy` |
| Preview command | `npx wrangler preview` (si se solicita) |

Pulsa **Deploy**. El registro debe mostrar `Verificación correcta: 64 fotos de referencia y ambos logos.` y después `Success! Build completed`. Si falta una imagen, el despliegue se detiene y el registro indica su ruta. La configuración solicita una base D1 nueva llamada `arocs-cta60`.

## 3. Crea el enlace privado

Abre PowerShell y pega esta línea:

```powershell
$b = New-Object byte[] 32; $rng = [System.Security.Cryptography.RandomNumberGenerator]::Create(); $rng.GetBytes($b); $rng.Dispose(); [BitConverter]::ToString($b).Replace('-', '').ToLowerInvariant()
```

En el Worker nuevo, ve a **Settings → Runtime variables and secrets → Add variable**. Marca **Production** y **Secret**. En **Key**, escribe `AROCS_ACCESS_KEY`. En **Value**, pega los 64 caracteres que generaste. Pulsa **Add variable and deploy**.

Abre una ventana de incógnito. Pega la URL nueva de Cloudflare, añade `/#acceso=` y pega la misma clave a continuación. Guarda el enlace completo antes de entrar. Escribe tu nombre y selecciona uno de los 52 VIN. Verifica el avance individual (64 puntos), el general (3.328 revisiones), los dos logos y las fotos de **1.1** y **23.1**.

La sesión del navegador dura siete días. El equipo puede volver a entrar con el mismo enlace.
