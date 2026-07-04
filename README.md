# AlejandrIA — Mapa de galaxia de conceptos de IA

Visualización 3D interactiva de 30 conceptos clave de Inteligencia Artificial,
organizados como una galaxia: cada concepto es un nodo grande con sus términos
relacionados orbitando como satélites, conectado por aristas a los conceptos afines.

## Archivos

| Archivo | Qué es |
|---|---|
| `index.html` | **La web completa, autocontenida** (~717 KB). Es el único archivo que necesitas para hostear. Funciona offline. |
| `index-src.html` | Fuente del anterior antes del empaquetado (requiere `support.js` y `data/` al lado). |
| `data/concepts-data.js` | Los datos: 30 conceptos, ~454 términos relacionados con definiciones, y las conexiones entre conceptos. Editable a mano. |
| `AlejandrIA.dc.html` | Fuente original editable en el editor de diseño (junto con `support.js`, en la raíz del proyecto). |

## Cómo hostearlo (GitHub + Cloudflare Pages)

1. Sube `index.html` a la raíz de tu repositorio.
2. Cloudflare → **Workers & Pages → Create → Pages → conecta el repo**.
   Sin build command; output directory = raíz.
3. Añade tu subdominio en **Custom domains**.

## Funcionalidades

- **Animación de bienvenida** (solo la primera visita): "Bienvenido a AlejandrIA. /
  La pequeña biblioteca de términos de IA", con botón **▶ PLAY** (las letras
  convergen en un nodo y de él florece la galaxia) y **SALTAR ≫** para ir directo.
  Se recuerda en `localStorage`; para volver a verla, abre la web con `#intro=1`.

- **Galaxia 3D** (Three.js): arrastra para rotar; rueda del ratón para alejar
  (la vista por defecto es el zoom máximo).
- **Selección**: clic en un nodo grande lo enfoca; su nombre aparece en un bocadillo
  blanco con conector, y sus términos relacionados se alinean en una columna a la
  derecha. Si no caben, un pager "+ N más → · 1/3" pagina.
- **Deselección**: clic en el fondo vacío o tecla `Esc`.
- **Conexiones resaltadas**: al seleccionar, las aristas del nodo se oscurecen
  y el resto se atenúa.
- **Hover**: los nodos crecen; los satélites muestran su nombre en un mini-bocadillo.
- **Constelaciones**: el nombre de cada categoría flota muy tenue sobre su clúster.
- **Panel lateral** (30%): definición del concepto, buscador (`/` lo enfoca),
  índice completo, navegación anterior/siguiente (también flechas ← →).
- **Idioma**: botón ES/EN (interfaz y definiciones de conceptos; las definiciones
  de los 454 términos están solo en inglés).
- **Modo oscuro**: botón con colores completamente invertidos.
- **URL compartible**: `#n=5&lang=en&dark=1` guarda nodo seleccionado, idioma y modo.
- **Estado inicial**: ningún nodo seleccionado (salvo que la URL lleve `#n=…`).
- **Responsive**: bajo 760 px la galaxia pasa arriba y el panel abajo.

## Editar los datos

`data/concepts-data.js` define `window.ALEJANDRIA_DATA`:

```js
{
  concepts: [ { id, name, cat, es, en, terms: [{ name, def }, …] }, … ],
  edges: [ [idA, idB], … ]   // conexiones entre conceptos
}
```

Tras editarlo hay que re-empaquetar `index.html` (o pedírmelo en el proyecto).
