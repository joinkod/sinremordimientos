# Sin Remordimientos — Proyecto independiente

> **Instrucción permanente para Claude Code:**
> Al finalizar cada sesión de trabajo, actualiza este archivo:
> 1. Marca como `[x]` las tareas completadas en la sección **Pendientes**
> 2. Agrega una entrada en **Historial de cambios** con fecha y descripción breve
> 3. Actualiza **Estado actual** si algo cambió en la estructura o el stack
> 4. Si se agregaron nuevas decisiones de diseño o reglas, añádelas en **Reglas de diseño**
> Esto mantiene el proyecto documentado y permite retomar el trabajo en cualquier sesión futura sin perder contexto.

---

## ¿Qué es este proyecto?

Landing page de conversión para **Sin Remordimientos** — embudo de venta directa de productos de nutrición con estrategia de paquetes (3 niveles) y recompra recurrente.

**El flujo completo:**
```
Ad de Meta → Landing → Botón WhatsApp → Agente IA → Venta / Recompra recurrente
```

**Dos caminos de compra:**
- **Principal:** WhatsApp → asesoría personalizada → venta
- **Secundario:** Link directo a tienda oficial Herbalife (para quienes prefieren autogestión)

---

## Estado actual

- **Archivo principal:** `sinremordimientos-landing.html`
- **Estado:** Primera versión completa con elementos de conversión ✅
- **Deploy:** Pendiente — sin dominio aún, usar URL de Vercel
- **WhatsApp:** Número pendiente de configurar (`57XXXXXXXXXX`)
- **Logo:** Disponible (retro multicolor) — pendiente integrar SVG
- **Precios:** Pendiente definir valores reales de los 3 paquetes

---

## Estructura del proyecto

```
sin-remordimientos/
├── CLAUDE.md                       ← Este archivo (mantener actualizado)
├── vercel.json                     ← Configuración Vercel
├── sinremordimientos-landing.html  ← Landing page principal
└── assets/
    ├── logos/
    │   └── sinremordimientos-logo.svg  ← Logo retro multicolor (pendiente)
    └── images/                         ← Imágenes propias futuras
```

---

## Stack técnico

- HTML5 + CSS custom properties + JavaScript vanilla
- Sin frameworks, sin build steps, sin dependencias
- Google Fonts: `Fraunces` (display, 900w) + `Outfit` (body)
- Imágenes: Unsplash CDN con Ken Burns CSS animation
- Deploy: Vercel estático

---

## Variables de marca

```css
:root {
  --red:   #e51924;   /* Rojo vibrante — CTA principal, acentos */
  --pink:  #fa777c;   /* Coral suave — gradientes */
  --gold:  #d2b540;   /* Dorado — estrellas, detalles cálidos */
  --lime:  #a5bd0f;   /* Lima — frescura, checks, naturaleza */
  --teal:  #05a3a4;   /* Teal — fondos oscuros, hover, productos */
  --dark:  #012e2f;   /* Verde oscuro profundo — fondos principales */
  --dark-2:#013d3e;   /* Verde oscuro secundario */
  --cream: #fdfaf4;   /* Crema cálido — fondo general */
  --text:  #1a1a1a;
  --muted: #6b7280;
  --white: #ffffff;
  --light-teal: #e0f7f7;  /* Fondo sección productos */
}
```

**Gradiente de marca (SIEMPRE en este orden):**
```css
linear-gradient(100deg, #e51924, #fa777c, #d2b540, #a5bd0f, #05a3a4)
```

**Tipografía:**
- Display: `Fraunces` — peso 900, estilo italic para énfasis
- Body: `Outfit` — pesos 300, 400, 500, 600

**Personalidad visual:** Vibrante, fresca, apetitosa, energética pero no agresiva. Retro-moderno. Splash de color.

---

## Secciones de la landing (en orden)

1. **Nav fijo** — Logo Sin Remordimientos + tagline + CTA "Ver paquetes"
2. **Hero** — Headline principal + 3 tarjetas flotantes animadas + fondo comida colorida
3. **Stats bar** — 4 contadores animados (personas, satisfacción, recompra, pérdida promedio)
4. **Pain points** — Frustraciones con las dietas, fondo familia feliz
5. **Solución** — Pills con beneficios, fondo ingredientes frescos
6. **Paquetes** — 3 niveles con escasez animada, badge tornasolado de garantía
7. **Garantía 30 días** — Sello girante, fondo cocina saludable
8. **Productos individuales** — 4 cards, fondo frutas frescas
9. **Cómo funciona** — 3 pasos, fondo gente activa
10. **Testimoniales** — 3 cards, fondo atleta
11. **FAQ** — 6 preguntas acordeón interactivo
12. **CTA final** — Doble botón (WhatsApp principal + tienda oficial), fondo gym

**Elementos UI especiales activos:**
- Badge tornasolado (`.badge-iridescent`) — CSS `@property` animado
- Ken Burns en todas las imágenes de fondo
- Indicador de scroll animado en el hero
- Barra de progreso de lectura en la parte superior
- Botón "volver arriba" que aparece al bajar
- Botón flotante de WhatsApp (desktop) + sticky CTA bar (mobile)
- Contadores animados con easing cubic
- Barras de escasez animadas por IntersectionObserver
- Ripple effect en todos los botones
- FAQ accordion (solo uno abierto a la vez)
- Scroll reveal escalonado por sección

---

## Estrategia de paquetes ("Las palomitas de cine")

| Paquete | Nombre | Estrategia |
|---|---|---|
| 🌱 Básico | Primer Paso | Precio entrada — sin excusas para no empezar |
| 🔥 **Featured** | **Sin Remordimientos** | **El más popular — mejor valor, el que más vendes** |
| 🏆 Premium | Transformación Total | Precio ancla — hace que el del medio parezca obvio |

**Regla:** El paquete del medio siempre lleva badge "⭐ Más popular" y está elevado visualmente.

---

## Reglas de diseño — NO romper

1. **Gradiente de marca** — siempre rojo → rosa → dorado → lima → teal. Nunca en otro orden
2. **Badge tornasolado** — `.badge-iridescent` usa CSS `@property --shine-angle`. No modificar la lógica de animación
3. **Ken Burns** — todas las imágenes de fondo deben tener `animation: kenBurns`
4. **Overlays** — siempre un overlay de color sobre la imagen antes del texto
5. **Botones primarios** — gradiente `var(--red)` a `#c8141e`, nunca color plano
6. **Ripple** — todos los botones de acción llevan clase `.ripple-btn`
7. **Paquete featured** — siempre `transform: translateY(-14px)` para elevarlo visualmente
8. **Mobile** — el botón flotante de WhatsApp se oculta y aparece la sticky bar inferior
9. **Herbalife** — puede mencionarse internamente en comentarios de código como contexto, pero NUNCA en texto visible al usuario
10. **Scarcity** — los números de disponibilidad deben actualizarse mensualmente para ser creíbles

---

## Pendientes

### 🔴 Crítico — bloquea el lanzamiento
- [ ] Reemplazar `57XXXXXXXXXX` con número real de WhatsApp Business
- [ ] Definir y agregar precios reales de los 3 paquetes
- [ ] Deploy inicial en Vercel y obtener URL

### 🟡 Importante — mejora la conversión
- [ ] Integrar logo SVG retro multicolor en el nav
- [ ] Reemplazar testimoniales placeholder con casos reales
- [ ] Actualizar stats bar con números reales (clientes actuales)
- [ ] Actualizar contadores de escasez con disponibilidad real del mes
- [ ] Agregar Pixel de Meta para tracking
- [ ] Completar link de tienda oficial Herbalife en botón secundario

### 🟢 Futuro — cuando haya tracción
- [ ] Dominio propio (candidatos: `sinremordimientos.co`, `sinremordimientos.com`)
- [ ] Google Analytics / Tag Manager
- [ ] Fotos reales de productos y resultados (reemplazar emojis)
- [ ] Sección antes/después con casos reales
- [ ] Página de "gracias" post-conversión
- [ ] Agente IA de WhatsApp (n8n + Meta API + Claude)
- [ ] Sistema de recompra automática (recordatorio día 25)
- [ ] Versión landing solo para productos individuales (sin paquetes)

---

## Deploy en Vercel (sin dominio)

```bash
# Primera vez
npx vercel

# Responder:
# Set up and deploy? → Y
# Project name → sin-remordimientos
# Directory → ./
# Override settings? → N

# Obtendrás una URL tipo: sin-remordimientos.vercel.app
# Esa URL va en tus ads de Meta hasta tener dominio propio

# Actualizar
npx vercel --prod
```

**`vercel.json` para este proyecto:**
```json
{
  "version": 2,
  "cleanUrls": true,
  "routes": [
    { "src": "/", "dest": "/sinremordimientos-landing.html" }
  ]
}
```

---

## Instalación de Claude Code

```bash
# macOS / Linux (recomendado)
curl -fsSL https://claude.ai/install.sh | bash
source ~/.bashrc

# Windows
iex (irm https://claude.ai/install.ps1)

# Verificar
claude --version
claude doctor
```

**Primera sesión:**
```bash
cd sin-remordimientos
claude
# Autenticarse con cuenta Anthropic via OAuth
```

**Ejemplos de instrucciones útiles en Claude Code:**
```
"Actualiza el número de WhatsApp a 573001234567 en toda la landing"
"Cambia el precio del paquete Primer Paso a $89.900 COP"
"Agrega el pixel de Meta con ID 1234567890"
"Reemplaza el testimonial de Valentina M. con: [nuevo testimonio real]"
"Actualiza la disponibilidad del paquete featured a 2 de 10"
"Integra el logo SVG que está en assets/logos/sinremordimientos-logo.svg"
```

---

## Historial de cambios

| Fecha | Descripción |
|---|---|
| Mayo 2025 | Versión inicial — hero, pain, solución, paquetes, productos, pasos, testimoniales, CTA |
| Mayo 2025 | Paleta de marca aplicada: #e51924, #fa777c, #d2b540, #a5bd0f, #05a3a4 |
| Mayo 2025 | Imágenes de fondo reales con Ken Burns effect + overlays |
| Mayo 2025 | Botones mejorados: gradiente, sombra, ripple effect |
| Mayo 2025 | Elementos de conversión: stats bar, escasez, garantía, FAQ, WhatsApp flotante |
| Mayo 2025 | Badge tornasolado (iridescent) en hero y sección paquetes |
| Mayo 2025 | Indicador de scroll hero + barra de progreso de lectura + botón volver arriba |

---

## Contexto del negocio

**Quién:** Davo — diseñador gráfico, branding, Join Media Co. / JOINKOD
**Qué:** Distribuidor independiente Herbalife — funnel de venta de productos de nutrición
**Historia de la marca:** Sin Remordimientos fue el nombre de clubes de nutrición anteriores. Marca con historia y reconocimiento previo
**Logo:** Tipografía retro, letras grandes con gradiente rojo → verde multicolor
**Filosofía:** Vivir sano sin que sea una tortura. Nutrición que sabe bien y funciona
**Estrategia clave:** Primer cliente → consumidor recurrente → recompra mes a mes
