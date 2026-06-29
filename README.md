# 🛒 La Despensa — Manual de instalación

PWA de lista de la compra compartida en tiempo real.
React 18 UMD + Firebase Realtime Database + GitHub Pages.

---

## Archivos del proyecto

```
Despensa/
├── index.html          ← App completa (EDITAR: pegar config Firebase)
├── sw.js               ← Service Worker (caché PWA)
├── manifest.json       ← Config PWA (nombre, iconos, colores)
├── icons/
│   ├── icon-192.png    ← Icono PWA pequeño
│   └── icon-512.png    ← Icono PWA grande
└── README.md           ← Este archivo
```

---

## PASO 1 — Crear proyecto Firebase

1. Ve a https://console.firebase.google.com
2. **Añadir proyecto** → Nombre: `Despensa`
   - Desactiva Google Analytics → **Crear proyecto**
3. Menú lateral → **Build → Realtime Database → Crear base de datos**
   - Región: **europe-west1 (Bélgica)**
   - Modo: **Iniciar en modo de prueba**
4. Menú lateral → **Configuración del proyecto** (⚙️) → pestaña **General**
   - Scroll abajo → sección **Tus apps** → clic en `</>` (Web)
   - Nombre de app: `Despensa` → **Registrar app**
   - Copia el bloque `firebaseConfig` que aparece

---

## PASO 2 — Pegar la config en index.html

Abre `index.html` y busca esta sección (está cerca del principio del script):

```javascript
const FB_CFG = {
  apiKey:            "YOUR_API_KEY",
  authDomain:        "YOUR_PROJECT_ID.firebaseapp.com",
  databaseURL:       "https://YOUR_PROJECT_ID-default-rtdb.europe-west1.firebasedatabase.app",
  projectId:         "YOUR_PROJECT_ID",
  storageBucket:     "YOUR_PROJECT_ID.appspot.com",
  messagingSenderId: "YOUR_SENDER_ID",
  appId:             "YOUR_APP_ID"
};
```

Reemplaza cada `"YOUR_..."` con los valores reales de tu Firebase.

---

## PASO 3 — Reglas de seguridad Firebase (recomendado)

En Firebase Console → Realtime Database → **Reglas**, pega esto:

```json
{
  "rules": {
    "market": {
      ".read": true,
      ".write": true
    }
  }
}
```

> Suficiente para uso familiar. Si en el futuro quieres más seguridad, añade autenticación.

---

## PASO 4 — Crear repo en GitHub

1. Ve a https://github.com/raucarc81 → **New repository**
2. Nombre: `Despensa`
3. Visibilidad: **Public** (necesario para GitHub Pages gratuito)
4. **Create repository** (sin README ni nada extra)

---

## PASO 5 — Subir los archivos

En el repo recién creado, sube **todos** estos archivos respetando la estructura:

```
index.html
sw.js
manifest.json
icons/icon-192.png
icons/icon-512.png
```

Para subir la carpeta `icons/` con sus imágenes:
- En GitHub → **Add file → Upload files**
- Arrastra la carpeta `icons/` completa (o los dos PNG dentro)

---

## PASO 6 — Activar GitHub Pages

1. En el repo → **Settings → Pages**
2. Source: **Deploy from a branch**
3. Branch: **main** → carpeta: **/ (root)**
4. **Save**

En 1-2 minutos la app estará en:
**https://raucarc81.github.io/Despensa/**

---

## PASO 7 — Instalar como PWA en el móvil

### Android (Chrome):
- Abre la URL en Chrome
- Menú (⋮) → **Añadir a pantalla de inicio**
- O espera el banner automático de instalación

### iPhone (Safari):
- Abre la URL en Safari
- Botón compartir → **Añadir a pantalla de inicio**

---

## Cómo funciona la app

### Inventario
- **Categorías** (tabs horizontales): Comida, Despensa, Bebidas...
- **Subcategorías** (acordeón): toca para expandir/colapsar
- **Productos**: nombre + supermercado + controles cantidad `[−][N][+]`
- Si la cantidad llega al **mínimo configurado** → el producto **va al carrito automáticamente** 🛒
- También puedes añadir al carrito manualmente con el menú `⋮`

### Carrito
- Vista **Todo** o **Por tienda**
- **✓ Completar**: introduce las unidades que has comprado → actualiza el stock y sale del carrito
- **✕ Quitar**: saca el producto del carrito sin comprarlo

### Sincronización
- Cualquier cambio se sincroniza en **tiempo real** entre todos los dispositivos
- Si tu mujer añade algo al carrito, recibes un **toast de aviso** en la app 🔔

### Añadir contenido
- **＋** al final de los tabs de categorías → nueva categoría
- **+ Nueva subcategoría** al final de cada categoría
- **+ Añadir producto** al final de cada subcategoría abierta

---

## Datos de primera carga

La primera vez que se abre la app, se carga automáticamente en Firebase:

**Comida:** Carnes, Pescados, Verduras, Huevos, Embutidos, Lechugas, Frutas, Frutos secos, Leche, Yogures, Quesos, Pan, Masa de pizza, Tortitas, Chocolate, Mantequilla, Mermelada

**Despensa:** Latas de conserva, Arroces, Legumbres, Pastas, Aceites, Salsas

**Bebidas:** Refrescos, Zumos, Vinos, Cervezas, Ron, Ginebra, Whisky, Licores

**Limpieza y Baños:** Papel absorbente, Papel higiénico, Bastoncillos oídos, Cremas, Toallitas desmaquillantes, Toallitas húmedas, Clínex, Pañales normales, Pañales de agua

**Guarrerías:** Patatas, Cortezas, Encurtidos, Saladitos

**Barbacoa:** Pastillas para encender, Cerillas largas, Carbón

**Botiquín:** Alcohol, Agua oxigenada, Yodo, Cristalmina, Tiritas, Esparadrapo, Vendas, Algodón, Compresas para heridas

---

## Notas técnicas

- SW cache: `despensa-v1` → bumpar a `v2` cada vez que se actualice `index.html`
- Siempre subir `index.html` + `sw.js` juntos
- Firebase databaseURL en Europa termina en `.europe-west1.firebasedatabase.app`
- Si la imagen de fondo no carga (Unsplash), muestra un gradiente oscuro verde — funciona igual

---

## URLs útiles

- App: https://raucarc81.github.io/Despensa/
- Firebase Console: https://console.firebase.google.com
- Repo GitHub: https://github.com/raucarc81/Despensa
