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
No hay usuarios ni contraseñas: cada dispositivo se conecta con un **código de acceso** que se ingresa una sola vez.

1. Entrá a https://console.firebase.google.com → **Agregar proyecto** (el plan gratis Spark alcanza).
2. **Compilación → Authentication → Comenzar → Anónimo → Habilitar**.
3. **Compilación → Firestore Database → Crear base de datos** (modo producción, ubicación `southamerica-east1`).
4. En Firestore → **Reglas**: pegá el contenido de `firestore.rules` → **Publicar**.
5. Creá el primer código: en Firestore → **Datos → Iniciar colección** → ID `claves` → ID del documento = tu código (**mínimo 8 letras o números, en MAYÚSCULAS, sin espacios ni guiones**, por ejemplo `K7P2QX9MRA`) → agregá un campo cualquiera (ej. `t` = `1`) → Guardar.
6. **⚙ Configuración del proyecto → Tus apps → Web (`</>`)** → registrá la app y copiá el objeto `firebaseConfig` dentro de `firebase-config.js` (en lugar de `null`).
7. Subí los archivos. En cada dispositivo: **HISTORIAL → Sincronización** → escribí el código → **Conectar**. No se vuelve a pedir.

**Cambiar el código** (por ejemplo si se pierde un celular): HISTORIAL → Sincronización → **Cambiar código**. Los demás dispositivos dejan de tener acceso hasta que ingresen el código nuevo (sus datos quedan guardados en cada uno). Las mayúsculas, espacios y guiones no importan al escribirlo.

Si se borran los datos del navegador o se reinstala la app, ese dispositivo vuelve a pedir el código. En iPhone, Safari y la app agregada al inicio cuentan como dispositivos distintos.

El primer dispositivo que se conecta sube sus datos; los siguientes reciben los de la nube (los historiales y redondeos guardados de cada uno se suman). Si dos personas cargan casillas distintas al mismo tiempo, se combinan; si tocan la misma casilla, queda la última.

> Los datos de `firebase-config.js` no son secretos: lo que protege la información son las reglas de Firestore + el código de acceso (nadie puede leer el código desde la app).

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
