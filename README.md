# Arqueo Oficial

App web (PWA) adaptada del Excel **ARQUEO OFICIAL 2026.xlsm**. Funciona en el celular, se instala como app y anda sin internet.

## Qué incluye (versión 6)
- **Arqueo**: billetes por sector (Planta Alta, Ventanilla, Torneo de Poker) + paquetes de Castito / Fichas (normal y plus). Total por denominación y total general.
- **VERIFICAR** (botón abajo a la derecha en Arqueo): ventana emergente como en el Excel, con el total por billete y el Cargo. Se cierra con VOLVER. Abajo tiene "Ver detalle por sector".
- **Premios** (botón POKER / hoja REDONDEO del Excel): original y redondeo de cada premio con su diferencia. Botones para agregar y quitar premios. Billetes de cada premio con selector ‹ ›, total de billetes de todos los premios (los de $20.000 van solo en fajos de 100) y listado para imprimir en 4 copias.
- **HISTORIAL** (botón abajo, al lado de VERIFICAR): ventana con los arqueos guardados por fecha y turno (se pueden volver a abrir) y la copia de seguridad (exportar/importar .json).
- **CONFECCIÓN** (botón abajo): ventana chica para editar cuántos billetes lleva cada paquete, con botón para volver a los valores del Excel.

Los datos quedan guardados **solo en el dispositivo** (localStorage del navegador).

## Publicar en GitHub Pages
1. Creá un repositorio nuevo en github.com (por ejemplo `arqueo-oficial`), público.
2. Botón **Add file → Upload files** y arrastrá **todo el contenido** de esta carpeta (index.html, manifest.json, sw.js, README.md y la carpeta `icons`). **Commit changes**.
3. En el repo: **Settings → Pages → Source: Deploy from a branch → Branch: main / (root) → Save**.
4. En 1-2 minutos queda en `https://TU-USUARIO.github.io/arqueo-oficial/`.

## Instalar en el celular
- **Android (Chrome)**: abrí el link → menú ⋮ → **Instalar app** / Agregar a pantalla principal.
- **iPhone (Safari)**: abrí el link → botón Compartir → **Agregar a inicio**.

## Actualizar
Subí los archivos nuevos al repo. Si el celular sigue mostrando la versión vieja, cerrá y abrí la app otra vez.
(Opcional: en `sw.js` cambiá `arqueo-v1` por `arqueo-v2`, etc.)
