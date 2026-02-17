# DECISIONES.md — Frontend (Cuenta de Ventas / Tienda)

## 1) Alcance del Front

**Incluye:** Home/Hero, listado de productos con paginación, detalle de producto, carrito/checkout, perfil y estados de órdenes, y pantalla de error (producto no encontrado).  
**Evidencia:** “Productos / Perfil / Pagar”, “Paginación”, “Comprar”, “Total / Finalizar”, “El producto que estás buscando no se encontró”.  
Referencia del prototipo: Actividad de aprendizaje.pdf. :contentReference[oaicite:3]{index=3} :contentReference[oaicite:4]{index=4} :contentReference[oaicite:5]{index=5} :contentReference[oaicite:6]{index=6}

---

## 2) Arquitectura UI (componentes reutilizables)

**Decisión:** usar un _Design System_ + librería de componentes.

- Design tokens: colores, tipografías, espaciado.
- Componentes base: Button, Input, Card, Modal/Drawer, Table/List, Badge, Pagination, Navbar.
  **Por qué:** consistencia visual, reuso y menos errores al escalar vistas (productos, perfil, checkout).  
  **Principios/patrones:** Atomic Design / Component-driven UI.

---

## 3) Navegación y estructura (IA)

**Decisión:** navegación superior con menú (hamburguesa en móvil) + rutas principales:

- `/` (home con hero + CTA + producto destacado)
- `/productos` (listado + paginación)
- `/producto/:id` (detalle + comprar)
- `/perfil` (puntos, órdenes por estado)
- `/pagar` o `/checkout` (total + finalizar)
- `/404` o estado “no encontrado” (error)
  **Evidencia:** “Logo + menú”, “Call to action / HERO IMG / Producto destacado”, “Paginación”, “Perfil”, “Pagar”, “Finalizar”. :contentReference[oaicite:7]{index=7} :contentReference[oaicite:8]{index=8} :contentReference[oaicite:9]{index=9} :contentReference[oaicite:10]{index=10}  
  **Patrones:** Router + Layout shell.

---

## 4) Accesibilidad (WCAG 2.2 AA)

**Decisiones clave:**

1. **Teclado primero:** todo operable con Tab/Shift+Tab/Enter/Esc (menú, paginación, formularios, finalizar compra).
2. **Focus visible:** estilo de enfoque consistente en botones, inputs y links (no se elimina `outline`).
3. **Skip link:** “Saltar al contenido” al inicio para evitar tabular todo el menú.
4. **Landmarks ARIA:** `header`, `nav`, `main`, `footer` para lectores de pantalla.
5. **Mensajes de error claros:** en formularios (cantidad, pago) se muestran mensajes junto al campo y se anuncian con `aria-live`.
6. **Imágenes:** `alt` descriptivo (producto, hero, perfil); si es decorativa -> `alt=""`.
   **Por qué:** asegurar navegación por teclado y compatibilidad con lector de pantalla, cumpliendo AA.

---

## 5) Tipografía y legibilidad

**Decisión:** base mínima **16px**, escalable (rem), y jerarquía clara:

- H1 (título de vista), H2 (secciones), texto base, ayudas.
  **Por qué:** lectura cómoda en móvil y accesibilidad (zoom sin romper layout).  
  **Principios:** legibilidad / jerarquía visual.

---

## 6) Colores y contraste

**Decisión:** paleta con contraste AA (mín. 4.5:1 en texto normal).  
**Cómo se valida:** Stark (Figma) / DevTools contrast checker.  
**Evidencia:** el prototipo usa fondos claros y texto oscuro + mensajes en rojo (error). :contentReference[oaicite:11]{index=11}  
**Nota:** errores no dependen solo del color; se acompaña con texto/ícono.

---

## 7) Espaciado y layout

**Decisión:** sistema de espaciado en múltiplos de **8px** (8/16/24/32).
**Por qué:** consistencia entre cards de productos, formularios y botones (CTA/Comprar/Finalizar).  
**Patrones:** grid + cards.

---

## 8) Estados de interacción (Figma Prototype)

**Decisión:** cada componente crítico tendrá estados:

- Button: default/hover/focus/disabled/loading
- Input: default/focus/error/disabled
- Paginación: activo/inactivo/focus
- Cards producto: hover/focus
  **Por qué:** el flujo “comprar → pagar → finalizar” necesita feedback claro. :contentReference[oaicite:12]{index=12} :contentReference[oaicite:13]{index=13}

---

## 9) Manejo de errores y vacíos

**Decisión:** pantalla dedicada para “producto no encontrado” con acción “Volver”.  
**Evidencia:** “El producto que estas buscando no se entro / Volver / IMG Error”. :contentReference[oaicite:14]{index=14}  
**Por qué:** reduce frustración y guía al usuario.

---

## 10) Rendimiento (conexión lenta)

**Decisión:** optimizar carga en móvil:

- Lazy loading de imágenes
- Paginación en listado
- Skeletons (loading)
- Cache básico de datos en cliente
  **Evidencia:** existe “Paginación” y lista de productos en grid. :contentReference[oaicite:15]{index=15}  
  **Por qué:** mejora UX en datos móviles.

---

## 11) Criterios de aceptación (resumen)

- Se puede comprar y finalizar sin mouse (teclado).
- Lector de pantalla entiende estructura (landmarks + labels).
- Contraste AA en textos.
- Estados visibles (focus/error/loading).
- Paginación accesible y navegable.
