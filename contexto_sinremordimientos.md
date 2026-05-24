# Sin Remordimientos — Contexto definitivo del proyecto
*Última actualización: 24 mayo 2026*

---

## 1. Stack y Arquitectura actual

### Landing page
- **HTML5 + CSS custom properties + JavaScript vanilla** — sin frameworks, sin build steps
- **Fuentes Google Fonts:** `Fraunces` (display, peso 900 + italic) + `Outfit` (body, pesos 300/400/500/600)
- **Imágenes de fondo:** Unsplash CDN con Ken Burns CSS animation (`@keyframes kenBurns`)
- **Deploy:** GitHub → Vercel (hosting estático)
- **Repo:** `joinkod/sinremordimientos`

### Variables de marca (CSS)
```css
:root {
  --red:        #e51924;  /* Rojo vibrante — CTA principal, acentos */
  --pink:       #fa777c;  /* Coral suave — gradientes */
  --gold:       #d2b540;  /* Dorado — estrellas, detalles cálidos */
  --lime:       #a5bd0f;  /* Lima — frescura, checks, naturaleza */
  --teal:       #05a3a4;  /* Teal — fondos oscuros, hover, productos */
  --dark:       #012e2f;  /* Verde oscuro profundo — fondos principales */
  --dark-2:     #013d3e;
  --cream:      #fdfaf4;  /* Crema cálido — fondo general */
  --text:       #1a1a1a;
  --muted:      #6b7280;
  --white:      #ffffff;
  --light-teal: #e0f7f7;
}
```

**Gradiente de marca — SIEMPRE en este orden:**
```css
linear-gradient(100deg, #e51924, #fa777c, #d2b540, #a5bd0f, #05a3a4)
```

### JavaScript implementado (a diferencia de EMUNAH, este proyecto SÍ tiene JS)
- Scroll reveal con `IntersectionObserver` (`.reveal` → `.visible`)
- Contadores animados con easing cúbico (`data-target`, `data-decimal`, `data-suffix`)
- Barras de escasez animadas por `IntersectionObserver` (`data-width`)
- FAQ accordion (un ítem abierto a la vez)
- Barra de progreso de lectura (`#scrollProgress`)
- Nav shadow al hacer scroll (`.scrolled`)
- Scroll indicator en hero (se oculta al bajar)
- Botón "volver arriba" (`#backTop`)
- Ripple effect en `.ripple-btn`

---

## 2. Estado del desarrollo

### Correcciones CODE vs. CHAT (verificado mayo 2026 — repo `joinkod/sinremordimientos`)
| Qué decía la documentación | Realidad en el código |
|---|---|
| Archivo principal: `sinremordimientos-landing.html` | Archivo real: **`index.html`** |
| `vercel.json` en el repo | No existe (Vercel sirve `index.html` automáticamente) |
| Assets / logo SVG | No existe `assets/` — logo es CSS gradient text (`grad-text`) |

### Módulos por estado

#### Landing page (`index.html` — en repo GitHub)
| Módulo | Estado real |
|---|---|
| Archivo HTML en repo | ✅ Existe como `index.html` |
| Deploy en Vercel | ⚠️ Repo existe en GitHub — verificar si hay proyecto Vercel activo |
| Nav fijo + scroll shadow | ✅ Implementado con JS |
| Barra de progreso de lectura | ✅ Implementado |
| Hero (headline + 3 tarjetas flotantes + Ken Burns) | ✅ Implementado |
| Scroll indicator animado en hero | ✅ Implementado |
| Stats bar (4 contadores) | ✅ Implementado — **números placeholder, actualizar con reales** |
| Pain points (5 items) | ✅ Implementado |
| Solución (pills con beneficios) | ✅ Implementado |
| Paquetes (3 niveles + escasez animada) | ✅ Implementado — **disponibilidades placeholder** |
| Badge tornasolado (CSS `@property`) | ✅ Implementado |
| Garantía 30 días (sello girante) | ✅ Implementado |
| Productos individuales (4 cards) | ✅ Implementado |
| Cómo funciona (3 pasos) | ✅ Implementado |
| Testimoniales (3 cards) | ✅ Implementado — **placeholders** |
| FAQ (6 preguntas, accordion) | ✅ Implementado |
| CTA final (doble botón) | ✅ Implementado |
| Botón flotante WhatsApp (desktop) | ✅ Implementado |
| Sticky CTA bar (mobile, ≤900px) | ✅ Implementado |
| Botón volver arriba | ✅ Implementado |
| Ripple en botones | ✅ Implementado |
| Responsive (≤900px y ≤480px) | ✅ Implementado con media queries |
| Número WhatsApp real | ❌ Sigue como `57XXXXXXXXXX` en todos los botones |
| Link tienda oficial Herbalife | ❌ `href="#"` — placeholder |
| Precios reales de los 3 paquetes | ❌ No aparecen precios en el HTML |
| Logo SVG retro multicolor | ❌ No existe — el nav usa texto con `grad-text` |
| Testimoniales reales | ❌ Placeholders (Valentina M./Cali, Andrés T./Medellín, Carolina R./Bogotá) |
| Stats reales | ❌ Placeholders (1247 personas, 4.9★, 98%, -8kg) |
| Pixel de Meta | ❌ No implementado |

---

## 3. Decisiones clave de diseño y negocio

### Funnel completo
```
Ad de Meta → Landing → Botón WhatsApp → Agente IA (n8n + Claude) → Venta → Recompra mensual
```
- **Dos caminos de compra:** WhatsApp (principal, asesoría personalizada) + tienda oficial Herbalife (secundario, autogestión)
- **Objetivo estratégico:** primer cliente → consumidor recurrente → recompra mes a mes

### Estrategia de paquetes ("Las palomitas de cine")
| Nivel | Nombre | Rol estratégico |
|---|---|---|
| 🌱 Básico | **Primer Paso** | Precio entrada — sin excusas para no empezar |
| 🔥 Featured | **Sin Remordimientos** | El más popular — mejor valor, el que más vendes |
| 🏆 Premium | **Transformación Total** | Precio ancla — hace que el del medio parezca obvio |

**Regla:** El paquete featured siempre lleva badge "⭐ Más popular" y está elevado con `transform: translateY(-14px)`.

### Reglas de diseño — NO romper
1. **Gradiente de marca** — siempre rojo → rosa → dorado → lima → teal. Nunca en otro orden
2. **Badge tornasolado** — `.badge-iridescent` usa CSS `@property --shine-angle`. No modificar la lógica de animación
3. **Ken Burns** — todas las imágenes de fondo llevan `animation: kenBurns`
4. **Overlays** — siempre un overlay de color sobre la imagen antes del texto
5. **Botones primarios** — gradiente `var(--red)` a `#c8141e`, nunca color plano
6. **Ripple** — todos los botones de acción llevan clase `.ripple-btn`
7. **Paquete featured** — siempre `transform: translateY(-14px)` para elevarlo
8. **Mobile** — el botón flotante WhatsApp se oculta y aparece la sticky bar inferior (≤900px)
9. **Herbalife** — puede mencionarse en comentarios internos de código, NUNCA en texto visible al usuario
10. **Scarcity** — los números de disponibilidad deben actualizarse mensualmente para ser creíbles

### Decisiones de arquitectura
- **Vanilla HTML/JS** — mismo criterio que EMUNAH: sin dependencias, deploy directo
- **Imágenes Unsplash CDN** — sin necesidad de `assets/` propios hasta tener fotos reales
- **Nav logo en CSS** — `grad-text` class en lugar de SVG hasta tener el logo retro listo
- **Un solo número WhatsApp** compartido con EMUNAH — el agente distingue el funnel por el mensaje pre-cargado

### Contexto del negocio
- **Quién:** Davo — diseñador gráfico, branding, Join Media Co. / JOINKOD (alianza con KODIAK / Renzo Muñoz)
- **Marca:** Sin Remordimientos — nombre de clubes de nutrición anteriores, con historia y reconocimiento previo
- **Filosofía:** "Vivir sano sin que sea una tortura. Nutrición que sabe bien y funciona."
- **Estrategia clave:** Primer cliente → consumidor recurrente → recompra mes a mes
- **Logo:** Tipografía retro, letras grandes con gradiente rojo → verde multicolor (pendiente integrar SVG)

---

## 4. Siguiente paso inmediato

### Paso 1 — Confirmar deploy en Vercel
Verificar si `sinremordimientos` tiene proyecto activo en Vercel:
- Entrar a vercel.com → revisar si aparece como proyecto
- Si no: `npx vercel` desde la carpeta `sinremordimientos/`
- `index.html` como raíz funciona sin `vercel.json`

### Paso 2 — Datos reales que desbloquean el lanzamiento
Con el número WhatsApp aprobado por Meta, actualizar en `index.html`:

| Placeholder | Reemplazar con |
|---|---|
| `57XXXXXXXXXX` (aparece 9 veces) | Número real de WhatsApp Business |
| `href="#"` del botón tienda | URL real de tienda oficial Herbalife |
| Precios de los 3 paquetes | Valores reales en COP |
| Stats bar (1247, 4.9, 98%, -8kg) | Números reales del negocio |
| Testimoniales placeholder | Casos reales (nombre, ciudad, resultado) |
| Disponibilidad en barras de escasez | Cupos reales del mes actual |

### Pendientes críticos (bloquean lanzamiento)
- [ ] Aprobación Meta WhatsApp Business → token permanente
- [ ] Número WhatsApp real reemplazado en todos los botones (9 ocurrencias)
- [ ] Precios reales de los 3 paquetes
- [ ] Link tienda oficial Herbalife en botón secundario
- [ ] Deploy confirmado en Vercel

### Pendientes importantes (mejoran conversión)
- [ ] Logo SVG retro multicolor en el nav
- [ ] Testimoniales reales (nombre, ciudad, resultado concreto)
- [ ] Stats reales en la stats bar
- [ ] Actualizar números de escasez mensualmente
- [ ] Pixel de Meta para tracking

### Futuro (cuando haya tracción)
- [ ] Dominio propio (`sinremordimientos.co` o `sinremordimientos.com`)
- [ ] Google Analytics / Tag Manager
- [ ] Fotos reales de productos y resultados (reemplazar Unsplash)
- [ ] Sección antes/después con casos reales
- [ ] Página de "gracias" post-conversión
- [ ] Flujo "Agente Sin Remordimientos" en n8n (comparte infraestructura con EMUNAH)
- [ ] Sistema de recompra automática (recordatorio día 25)
- [ ] Landing solo para productos individuales (sin paquetes)

---

## Deploy en Vercel (referencia)
```bash
# Primera vez
npx vercel
# Project name → sinremordimientos / Directory → ./ / Override → N

# Actualización
npx vercel --prod
```
No se necesita `vercel.json` — Vercel sirve `index.html` como raíz por defecto.

---

## Historial de cambios

| Fecha | Descripción |
|---|---|
| Mayo 2025 | Versión inicial — hero, pain, solución, paquetes, productos, pasos, testimoniales, CTA |
| Mayo 2025 | Paleta aplicada: #e51924, #fa777c, #d2b540, #a5bd0f, #05a3a4 |
| Mayo 2025 | Imágenes Unsplash con Ken Burns + overlays en todas las secciones |
| Mayo 2025 | JS completo: scroll reveal, contadores, escasez, FAQ, progress bar, ripple |
| Mayo 2025 | Badge tornasolado (CSS @property), sello girante de garantía |
| Mayo 2025 | Botón flotante WhatsApp (desktop) + sticky CTA bar (mobile) |
| Mayo 2026 | Fusión CLAUDE.md → contexto_sinremordimientos.md. Código verificado: archivo es index.html, JS completo, datos pendientes de reemplazar |
