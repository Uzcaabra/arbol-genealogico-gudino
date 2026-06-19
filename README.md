# 🌳 Árbol Genealógico — Familia Gudiño

Aplicación web colaborativa para visualizar y editar el árbol genealógico de la Familia Gudiño (Santa Lucía del Tuy · Miranda · Venezuela).

Funciona como una sola página HTML pública en GitHub Pages. Los datos se guardan en Firebase Realtime Database y se sincronizan en tiempo real para todos los familiares que abran el link.

---

## 🔗 Link público

```
https://Uzcaabra.github.io/arbol-genealogico-gudino/
```

Comparte este link con la familia. No hace falta crear cuenta ni instalar nada — se abre directo en el navegador del teléfono.

---

## ⚙️ Configurar Firebase (paso a paso)

> Sin este paso la app funciona en modo demo local (sin sincronización). Cada persona ve su propia copia de los datos.

### Paso 1 — Crear el proyecto en Firebase

1. Ve a [https://console.firebase.google.com](https://console.firebase.google.com) e inicia sesión con tu cuenta de Google.
2. Haz clic en **"Agregar proyecto"**.
3. Nombre del proyecto: `arbol-genealogico-gudino` (o el que prefieras).
4. Desactiva Google Analytics (no lo necesitas).
5. Haz clic en **"Crear proyecto"** y espera ~30 segundos.

### Paso 2 — Crear la Realtime Database

1. En el menú lateral, ve a **Compilación → Realtime Database**.
2. Haz clic en **"Crear una base de datos"**.
3. Elige la región más cercana (ej. `us-central1`).
4. Selecciona **"Empezar en modo de prueba"** (después restringimos).
5. Haz clic en **"Habilitar"**.

### Paso 3 — Obtener las credenciales

1. En el menú lateral, haz clic en el ícono de engranaje ⚙️ → **"Configuración del proyecto"**.
2. Desplázate hasta la sección **"Tus apps"**.
3. Si no hay ninguna app, haz clic en el ícono **`</>`** (Web).
4. Registra la app con el nombre `arbol-web` (sin Firebase Hosting).
5. Firebase te mostrará un bloque `firebaseConfig` con tus credenciales. Se ve así:

```js
const firebaseConfig = {
  apiKey: "AIzaSy...",
  authDomain: "arbol-genealogico-gudino.firebaseapp.com",
  databaseURL: "https://arbol-genealogico-gudino-default-rtdb.firebaseio.com",
  projectId: "arbol-genealogico-gudino",
  storageBucket: "arbol-genealogico-gudino.appspot.com",
  messagingSenderId: "123456789",
  appId: "1:123456789:web:abcdef..."
};
```

### Paso 4 — Pegar las credenciales en el código

Abre `index.html` y busca el bloque marcado así:

```html
<!-- ══════════════════════════════════════════
     FIREBASE CONFIG — Reemplaza estos valores
     ══════════════════════════════════════════ -->
```

Reemplaza los valores `"TU_..."` con los que copiaste de Firebase:

```js
const FIREBASE_CONFIG = {
  apiKey:            "AIzaSy...",        // ← tu valor real
  authDomain:        "tu-proyecto.firebaseapp.com",
  databaseURL:       "https://tu-proyecto-default-rtdb.firebaseio.com",
  projectId:         "tu-proyecto",
  storageBucket:     "tu-proyecto.appspot.com",
  messagingSenderId: "123456789",
  appId:             "1:123456789:web:..."
};
```

Guarda el archivo, haz commit y push. La app se conectará a Firebase automáticamente.

### Paso 5 — Reglas de seguridad de la base de datos

#### Opción A — Lectura/escritura abierta (para empezar, más simple)

En Firebase Console → Realtime Database → **Reglas**, pega esto:

```json
{
  "rules": {
    ".read": true,
    ".write": true
  }
}
```

> ⚠️ **Riesgo:** cualquier persona que encuentre tu URL de base de datos puede leer y escribir datos. Suficiente para uso familiar privado, pero no recomendado si compartes el link públicamente de forma masiva.

#### Opción B — Proteger con una clave secreta (recomendado)

Agrega en `index.html`, justo después de `FIREBASE_CONFIG`, una clave de acceso:

```js
const ACCESS_KEY = "familia2024"; // pon la que quieras
```

Y modifica las reglas en Firebase a:

```json
{
  "rules": {
    ".read":  "auth == null && root.child('accessKey').val() === 'familia2024'",
    ".write": "auth == null && root.child('accessKey').val() === 'familia2024'"
  }
}
```

> Para una protección real en el futuro, activa Firebase Authentication (correo/contraseña o Google) y cambia las reglas para requerir `auth != null`.

---

## 💡 Plan gratuito de Firebase (Spark)

El plan **Spark (gratis)** de Firebase es más que suficiente para este uso:

| Límite | Plan Spark | Uso esperado |
|--------|-----------|-------------|
| Almacenamiento | 1 GB | < 1 MB para cientos de personas |
| Descargas por mes | 10 GB | < 50 MB para uso familiar |
| Conexiones simultáneas | 100 | Más que suficiente |
| Costo | **$0** | — |

No necesitas tarjeta de crédito para el plan Spark.

---

## 📋 Cómo usar la aplicación

| Acción | Cómo |
|--------|------|
| **Ver el árbol** | Abre el link en cualquier navegador |
| **Agregar familiar** | Botón **"+ Agregar familiar"** arriba a la derecha |
| **Editar / Eliminar** | Haz clic en la tarjeta de la persona |
| **Exportar PDF** | Botón **📄 PDF** — genera un PDF del árbol completo |
| **Respaldo JSON** | Botón **💾 JSON** — descarga todos los datos |
| **Restaurar respaldo** | Botón **📂 Importar** — carga un archivo JSON guardado |

---

## 💾 Hacer respaldos

Firebase es persistente, pero es bueno tener respaldos manuales:

1. Haz clic en **💾 JSON** para descargar un archivo con todos los datos.
2. Guárdalo en Google Drive o en tu computador.
3. Si alguna vez necesitas restaurar, usa **📂 Importar**.

También puedes exportar directamente desde Firebase Console → Realtime Database → ⋮ → **Exportar JSON**.

---

## 🛠️ Actualizar el código

```bash
git add index.html
git commit -m "descripción del cambio"
git push origin main
```

GitHub Pages se actualiza automáticamente en ~1 minuto.

---

## 📁 Estructura del repositorio

```
arbol-genealogico-gudino/
├── index.html    ← toda la aplicación (HTML + CSS + JS)
└── README.md     ← este archivo
```

---

## 🤝 Compartir con la familia

Envía este link por WhatsApp:

```
https://Uzcaabra.github.io/arbol-genealogico-gudino/
```

Se abre directo en el teléfono, sin instalar nada. Los cambios que haga cualquier familiar aparecen en tiempo real para todos los demás (una vez configurado Firebase).
