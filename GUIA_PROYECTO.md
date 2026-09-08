# Guía del proyecto FitForLife

Sitio web de presentación para el smartwatch FitForLife. La aplicación muestra sus características, especificaciones técnicas, galería de acabados y puntos de venta oficiales.

Está construida con React, Vite, React Router y CSS Modules.

## 1. Requisitos previos

Antes de comenzar, instala:

- Node.js 20 o una versión compatible con Vite 8.
- pnpm.
- Git, si vas a clonar el repositorio.

Comprueba las instalaciones:

```bash
node --version
pnpm --version
git --version
```

Si pnpm no está disponible, puedes habilitarlo mediante Corepack:

```bash
corepack enable
corepack prepare pnpm@latest --activate
```

## 2. Obtener el proyecto

Clona el repositorio y entra en su carpeta:

```bash
git clone <URL_DEL_REPOSITORIO>
cd FitforLife
```

Si ya tienes la carpeta abierta en VS Code, comienza directamente con la instalación de dependencias.

## 3. Instalar dependencias

Desde la raíz del proyecto, donde está `package.json`, ejecuta:

```bash
pnpm install
```

Este comando usa `pnpm-lock.yaml` para instalar versiones reproducibles.

## 4. Ejecutar en desarrollo

Inicia el servidor local:

```bash
pnpm dev
```

Vite mostrará una URL similar a `http://localhost:5173/`. Abre esa dirección en el navegador. El modo de desarrollo incluye HMR, por lo que los cambios se reflejan sin reiniciar manualmente la aplicación.

Para detener el servidor, presiona `Ctrl + C` en la terminal.

## 5. Recorrido de la aplicación

La aplicación usa `BrowserRouter` y un layout compartido. Las rutas disponibles son:

| Ruta | Vista | Función |
| --- | --- | --- |
| `/` | Inicio | Presenta el producto, modelos, beneficios, contador y formulario de suscripción. |
| `/DS3` | Información del producto | Muestra la ficha técnica organizada por categorías. |
| `/Galeria` | Galería | Filtra acabados y abre el detalle de cada imagen en un modal. |
| `/Ubicacion` | Ubicación | Lista tiendas, horarios, teléfonos y formulario de disponibilidad. |
| `/Footer` | Footer | Vista independiente del componente de pie de página. |

Las rutas desconocidas redirigen automáticamente a `/`.

## 6. Estructura del proyecto

```text
FitforLife/
├── public/                         # Archivos públicos servidos sin procesamiento
├── src/
│   ├── assets/                     # Imágenes usadas por la aplicación
│   ├── components/
│   │   ├── Layout/                 # Layout general con Navbar, Outlet y Footer
│   │   ├── Footer/                 # Footer reutilizable
│   │   └── Navbar/                 # Navegación principal
│   ├── pages/
│   │   ├── Home/                   # Página de inicio
│   │   ├── ProductInfo/            # Información técnica
│   │   ├── Gallery/                # Galería y modal
│   │   ├── Location/               # Tiendas y formulario de consulta
│   │   └── Footer/                 # Página independiente del footer
│   ├── routes/AppRoutes.jsx        # BrowserRouter y definición de rutas
│   ├── App.jsx                     # Punto de entrada de la interfaz
│   ├── main.jsx                    # Montaje de React en #root
│   ├── App.css                     # Estilos globales de App
│   └── index.css                   # Reset y estilos base
├── index.html                      # Documento HTML inicial
├── package.json                    # Dependencias y scripts
├── pnpm-lock.yaml                  # Versiones bloqueadas
└── vite.config.js                  # Configuración de Vite
```

Cada página tiene un archivo `.jsx` y su correspondiente `.module.css`. Los estilos locales se importan como `styles`, evitando colisiones entre componentes.

## 7. Cómo añadir una nueva página

1. Crea una carpeta dentro de `src/pages/`, por ejemplo `src/pages/Contacto/`.
2. Añade `Contacto.jsx` y `Contacto.module.css`.
3. Implementa el componente y exporta su función principal.
4. Importa el componente en `src/routes/AppRoutes.jsx`.
5. Registra una nueva ruta dentro de la ruta padre de `MainLayout`.
6. Añade un enlace en el Navbar o Footer si la página debe aparecer en la navegación.
7. Ejecuta `pnpm lint` y prueba la URL con `pnpm dev`.

Ejemplo de registro de ruta:

```jsx
import Contacto from '../pages/Contacto/Contacto.jsx'

<Route path="Contacto" element={<Contacto />} />
```

## 8. Cómo modificar contenido

- El contenido de la página de inicio está en `src/pages/Home/Home.jsx`.
- Las especificaciones técnicas están en `src/pages/ProductInfo/ProductInfo.jsx`.
- Los elementos y filtros de la galería están en `src/pages/Gallery/Gallery.jsx`.
- Las tiendas y sus datos están en `src/pages/Location/Location.jsx`.
- La imagen principal del producto se importa desde `src/assets/ElproductoP.png`.

Para cambiar la apariencia, edita el CSS Module de la página o componente correspondiente. Conserva la importación `styles` y los nombres de clase usados en el JSX.

## 9. Scripts disponibles

| Comando | Uso |
| --- | --- |
| `pnpm dev` | Inicia el servidor de desarrollo con Vite. |
| `pnpm lint` | Revisa el código con ESLint. |
| `pnpm build` | Genera la versión optimizada en `dist/`. |
| `pnpm preview` | Sirve localmente la carpeta `dist/` para revisar la compilación. |

Flujo recomendado antes de entregar cambios:

```bash
pnpm lint
pnpm build
pnpm preview
```

## 10. Generar y revisar producción

1. Ejecuta `pnpm lint` para detectar errores de estilo o código.
2. Ejecuta `pnpm build` para crear `dist/`.
3. Ejecuta `pnpm preview` y revisa las rutas principales.
4. Comprueba navegación, filtros, modales, formularios y diseño responsive.
5. Antes de publicar, verifica que los recursos de `src/assets/` estén incluidos en la compilación.

La carpeta `dist/` es un artefacto generado; no se edita manualmente.

## 11. Solución de problemas frecuentes

### El comando `pnpm` no existe

Instala Node.js, habilita Corepack y vuelve a ejecutar `pnpm install`.

### Faltan módulos después de cambiar de rama

Actualiza las dependencias desde la raíz:

```bash
pnpm install
```

### El puerto de Vite está ocupado

Vite intentará usar otro puerto disponible. Usa la URL que aparezca en la terminal.

### Una ruta no se muestra

Comprueba el `path` y el `import` en `src/routes/AppRoutes.jsx`. Recuerda que las rutas actuales distinguen mayúsculas y minúsculas, por ejemplo `/Galeria` y `/Ubicacion`.

### Una imagen no aparece

Confirma que el archivo exista en `src/assets/` y que la ruta relativa del import parta desde el archivo `.jsx` que la usa.

## 12. Estado actual de validación

La validación se ejecuta con `corepack pnpm` cuando pnpm no está disponible directamente en el PATH. En el estado actual del repositorio:

- `pnpm lint` falla porque `src/pages/Footer/Footer.jsx` importa `React` sin utilizarlo.
- `pnpm build` falla porque `src/components/Layout/MainLayout.jsx` importa `../Navbar/Navbar.jsx`, pero esa carpeta o archivo no está presente en `src/components/`.

Estos errores deben corregirse antes de publicar una compilación de producción. La sección de comandos anterior describe el flujo esperado una vez resueltos.

## 13. Tecnologías principales

- React 19
- Vite 8
- React Router DOM 7
- Lucide React para iconos
- ESLint 10
- CSS Modules
