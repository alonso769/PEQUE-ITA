# Estudio Pequeñita: showroom inmobiliario interactivo

## Cómo abrirlo en Visual Studio Code

1. Descomprime el .zip en una carpeta, por ejemplo `Documentos/estudio-pequenita`.
2. Abre VS Code y ve a **Archivo → Abrir carpeta**. Elige esa carpeta.
3. Instala la extensión **Live Server**, de Ritwick Dey. Está en el ícono de cuadritos de la barra izquierda.
4. Haz clic derecho sobre `index.html` y elige **"Open with Live Server"**. Se abrirá en tu navegador.

> Importante: no abras `index.html` con doble clic. El navegador bloquea el visor 360° cuando
> la página se abre como archivo suelto, así que necesitas Live Server o publicarla en internet.

## Estructura

```
index.html          → toda la página (diseño, textos y lógica)
lib/pannellum.js    → visor 360° (no tocar)
lib/pannellum.css   → estilos del visor 360° (no tocar)
img/                → todas las imágenes
   fachada.jpg, planta.jpg
   sala-a.jpg, sala-b.jpg, cocina.jpg, dormitorio.jpg   (renders)
   360-sala-a.jpg, 360-sala-b.jpg, 360-dorm.jpg         (panorámicas)
```

## Qué cambiar (todo está en index.html, dentro de <script>)

Busca estas secciones con Ctrl+F:

| Quieres cambiar… | Busca | Qué editar |
|---|---|---|
| Número de WhatsApp | `whatsapp:` | `"51999999999"` → tu número con código de país, sin + ni espacios |
| Nombre, dormitorios, baños o m² de cada tipo | `const TIPOS` | los valores de `A` y `B` |
| Imágenes de cada tipo | `renders:` y `tour:` | la ruta de cada imagen |
| Pisos | `PISO_MIN` / `PISO_MAX` | el número del primer y del último piso |
| Precios base | `const base` | 112000 (Tipo A) y 71500 (Tipo B) |
| Estado de los departamentos | `2. DATOS DE PRUEBA` | ver abajo |

### Poner estados reales (vendido, reservado, disponible)

Ahora los estados se generan al azar para la demo. Para fijarlos a mano, agrega esto justo
antes de la línea `const pisoStats`:

```js
const ESTADOS_REALES = {
  "A-03": "vendido",
  "B-03": "reservado",
  "C-03": "disponible",
  // ...uno por línea
};
Object.entries(ESTADOS_REALES).forEach(([code, est]) => { if (DEPAS[code]) DEPAS[code].estado = est; });
```

## Cambiar una imagen

Reemplaza el archivo dentro de `img/` por otro **con el mismo nombre**. Si cambias la fachada
o la planta por otra distinta, hay que volver a marcar las coordenadas en `FRANJAS` (pisos)
y `UNIDADES` (departamentos).

## Publicarlo en internet gratis

1. Crea una cuenta en **netlify.com**.
2. Ve a **Sites** y arrastra la carpeta completa a la zona que dice "Drag and drop".
3. En segundos tendrás un enlace público. Luego puedes conectar tu propio dominio.
