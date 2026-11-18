# Arqueo Oficial

App web (PWA) adaptada del Excel **ARQUEO OFICIAL 2026.xlsm**. Funciona en el celular, se instala como app y anda sin internet.

## Qué incluye (versión 6)
- **Arqueo**: billetes por sector (Planta Alta, Ventanilla, Torneo de Poker) + paquetes de Castito / Fichas (normal y plus). Total por denominación y total general.
- **VERIFICAR** (botón al final de la tabla de Arqueo, a la derecha, junto al tachito y el disket): ventana emergente como en el Excel, con el total por billete y el Cargo. Se cierra con VOLVER. Abajo tiene "Ver detalle por sector".
- **Premios** (botón POKER / hoja REDONDEO del Excel): original y redondeo de cada premio con su diferencia. La lista arranca con 20 premios; al cargar el último aparece otro renglón vacío, y los renglones vacíos que sobran al final se quitan solos. Billetes de cada premio con selector ‹ ›, total de billetes de todos los premios (los de $20.000 van solo en fajos de 100) y listado para imprimir en 4 copias.
- **HISTORIAL** (botón abajo, al lado de CONFECCIÓN): ventana con los arqueos guardados por fecha y turno (se pueden volver a abrir) y la copia de seguridad (exportar/importar .json).
- **CONFECCIÓN** (botón abajo): ventana chica para editar cuántos billetes lleva cada paquete, con botón para volver a los valores del Excel.

Los datos se guardan en el dispositivo (anda sin internet) y, si configurás Firebase, se **sincronizan automáticamente entre todos los dispositivos** (arqueo actual, confección, historial y redondeos guardados). El punto al lado del título indica el estado: verde = conectado, naranja = sin conexión (los cambios se suben al volver), rojo = error.

## Sincronizar con Firebase (una sola vez)
1. Entrá a https://console.firebase.google.com → **Agregar proyecto** (el plan gratis Spark alcanza).
2. **Compilación → Authentication → Comenzar → Correo electrónico/contraseña → Habilitar**. En la pestaña **Usuarios → Agregar usuario**: creá el usuario (correo + contraseña) que van a usar todos los dispositivos.
3. **Compilación → Firestore Database → Crear base de datos** (modo producción, ubicación `southamerica-east1`).
4. En Firestore → **Reglas**: pegá el contenido de `firestore.rules`, cambiando `CORREO-DEL-USUARIO@ejemplo.com` por el correo del paso 2 → **Publicar**.
5. **⚙ Configuración del proyecto → Tus apps → Web (`</>`)** → registrá la app y copiá el objeto `firebaseConfig` dentro de `firebase-config.js` (en lugar de `null`).
6. Subí los archivos. En cada dispositivo: **HISTORIAL → Sincronización** → correo y contraseña → **Conectar** (queda conectado).

El primer dispositivo que se conecta sube sus datos; los siguientes reciben los de la nube (los historiales y redondeos guardados de cada uno se suman). Si dos personas cargan casillas distintas al mismo tiempo, se combinan; si tocan la misma casilla, queda la última.

> Los datos de `firebase-config.js` no son secretos: lo que protege la información son las reglas de Firestore + el usuario y contraseña.

### Opcional: publicar en Firebase Hosting en vez de GitHub Pages
Con [Firebase CLI](https://firebase.google.com/docs/cli) instalado: `firebase login`, `firebase use --add` (elegí el proyecto) y `firebase deploy`. Queda en `https://TU-PROYECTO.web.app` y también publica las reglas de `firestore.rules`.

## Publicar en GitHub Pages
1. Creá un repositorio nuevo en github.com (por ejemplo `arqueo-oficial`), público.
2. Botón **Add file → Upload files** y arrastrá **todo el contenido** de esta carpeta (index.html, firebase-config.js, manifest.json, sw.js, README.md y la carpeta `icons`). **Commit changes**.
3. En el repo: **Settings → Pages → Source: Deploy from a branch → Branch: main / (root) → Save**.
4. En 1-2 minutos queda en `https://TU-USUARIO.github.io/arqueo-oficial/`.

## Instalar en el celular
- **Android (Chrome)**: abrí el link → menú ⋮ → **Instalar app** / Agregar a pantalla principal.
- **iPhone (Safari)**: abrí el link → botón Compartir → **Agregar a inicio**.

## Actualizar
Subí los archivos nuevos al repo. Si el celular sigue mostrando la versión vieja, cerrá y abrí la app otra vez.
(Opcional: en `sw.js` cambiá `arqueo-v1` por `arqueo-v2`, etc.)
