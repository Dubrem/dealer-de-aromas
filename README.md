# ESENCIA — Fragancias que te definen

Tienda de perfumes. Misma infraestructura que DUBREM (`~/bella-esencia`), con el
catálogo, los textos y las categorías adaptados a perfumería.

## Qué incluye

- `index.html` — toda la tienda en un solo archivo: catálogo, carrito, checkout,
  cuentas de cliente, panel de administración, reseñas y búsqueda con Fuse.js.
- `api/products.js` — reenvía `productMeta` de Firebase (catálogo sin fotos).
- `api/img.js` — sirve las fotos base64 guardadas en Firebase como imágenes cacheables.
- `api/create-preference.js` — crea la preferencia de pago de Mercado Pago.
- `api/webhook.js` — confirma el pago aprobado y marca el pedido en Firebase.
- `sw.js` — service worker (caché de la página y de las fotos).
- `vercel.json`, `robots.txt`, `sitemap.xml`.

## Antes de publicar

1. **Firebase Realtime Database.** Crea una base nueva y pon su URL en:
   - `index.html` → `const FIREBASE_DB_URL` (línea ~3046)
   - variable de entorno `FIREBASE_DB_URL` en Vercel (la usan `api/products.js`,
     `api/img.js` y `api/webhook.js`).
   Hoy apunta al placeholder `https://esencia-perfumes-default-rtdb.firebaseio.com`,
   que todavía no existe: hasta que la crees, el catálogo se ve vacío.
2. **Mercado Pago.** Variable `MP_ACCESS_TOKEN` en Vercel. En
   `api/create-preference.js` ya quedan `statement_descriptor: 'ESENCIA'` y
   `notification_url: https://esencia-perfumes.vercel.app/api/webhook` — cambia el
   dominio si usas otro.
3. **Dominio.** Se usó `esencia-perfumes.vercel.app` en meta tags, sitemap, robots
   y webhook. Reemplázalo por el dominio real.
4. **Contacto.** El WhatsApp (`525563723284`) y el Facebook siguen siendo los de
   DUBREM; cámbialos si la perfumería usa otros.

## Catálogo

Secciones: Mujer, Hombre, Unisex, Árabes, Nicho, Sets y Estuches, Miniaturas,
Línea Corporal, Aromas de Hogar, Ofertas. Las sub-categorías son familias
olfativas y tipos de producto (Eau de Parfum, Oud, Attar, Body Mist, Decants…).

Las tallas de ropa se convirtieron en **presentaciones**: Decant 5 ml, Decant
10 ml, 30, 50, 60, 75, 100, 125, 200 ml y Única.

## Correr en local

```bash
npx serve -p 4321 .
```

Las funciones de `api/` solo corren en Vercel (`vercel dev` si quieres probarlas).
