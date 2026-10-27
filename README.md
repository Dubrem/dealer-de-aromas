# Dealer de Aromas — Fragancias que te definen

Tienda de perfumes en línea: catálogo, carrito, checkout con Mercado Pago y
panel de administración.

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

1. **Firebase.** Ya conectado al proyecto `dealer-de-aromas`: `index.html` tiene
   `FIREBASE_DB_URL` (línea ~3046) y `FIREBASE_API_KEY` (~3020). En Vercel hay que
   definir `FIREBASE_DB_URL`, que usan `api/products.js`, `api/img.js` y
   `api/webhook.js`. El acceso al panel usa Authentication (correo/contraseña).
2. **Mercado Pago.** Variable `MP_ACCESS_TOKEN` en Vercel. En
   `api/create-preference.js` ya quedan `statement_descriptor: 'DEALERAROMAS'` y
   `notification_url: https://dealer-de-aromas.vercel.app/api/webhook` — cambia el
   dominio si usas otro.
3. **Dominio.** Se usó `dealer-de-aromas.vercel.app` en meta tags, sitemap, robots
   y webhook. Reemplázalo por el dominio real.
4. **Contacto.** El WhatsApp (`525563723284`), la CLABE, el Facebook y la dirección
   de la tienda vienen del proyecto anterior; cámbialos por los del negocio.

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

## Pendientes de datos reales

- **Transferencia:** banco, titular y CLABE están como `XXXXXXXX` en el paso de
  pago del checkout (busca `data-banco`, `data-titular` y `data-clabe` en
  `index.html`). Sustitúyelos cuando haya cuenta a nombre de la tienda.
- **Mercado Pago:** oculto con `const MP_ACTIVO = false;` (~línea 2922). Ponlo en
  `true` y define `MP_ACCESS_TOKEN` en Vercel para reactivar el pago con tarjeta.
- **Entrega:** una sola opción, en mano con Reynel Martínez González
  (`const REPARTIDOR`), sin costo de envío (`SHIP_LOCAL = 0`).
