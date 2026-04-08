# CONTEXT.md — Guía de Contexto para IA

> Este archivo describe el proyecto TI3011 para que cualquier asistente de IA pueda entender su propósito, estructura, patrones de diseño y reglas que debe respetar al generar o modificar código.

---

## 1. ¿Qué es este proyecto?

Es una **plataforma de micro-aprendizaje estática** para la asignatura universitaria **TI3011 — Lógica y Resolución de Problemas** (INACAP Chile). Está construida exclusivamente con **HTML, CSS y JavaScript vanilla**, sin ningún framework ni librería externa. Cada página es completamente autónoma (autocontenida: estilos y scripts dentro del mismo archivo `.html`).

El objetivo pedagógico es que los estudiantes aprendan conceptos de lógica computacional y pseudocódigo PseInt de forma visual e interactiva, sin necesidad de instalar ningún software.

---

## 2. Estructura de Archivos y Navegación

```
TI3011/
├── index.html              → Hub raíz (listado de módulos)
├── clase1/
│   ├── clase1.html         → Hub del Módulo 1
│   ├── problematica.html
│   ├── modelo-polya.html
│   └── diagramas.html
└── clase2/
    ├── clase2.html         → Hub del Módulo 2
    ├── pseint-concepto-variable.html
    ├── pseint-variables.html
    ├── pseint-tipos.html
    ├── pseint-condicionales.html
    ├── pseint-segun.html
    ├── pseint-ciclos.html
    ├── pseint-repetir.html
    └── pseint-para.html
```

### Reglas de navegación (enlaces relativos)
- `index.html` → apunta a `clase1/clase1.html` y `clase2/clase2.html`
- `clase1/clase1.html` y `clase2/clase2.html` → back-link a `../index.html`
- Páginas dentro de `clase1/` → back-link a `clase1.html` (misma carpeta)
- Páginas dentro de `clase2/` → back-link a `clase2.html` (misma carpeta)
- **Nunca usar rutas absolutas.** Siempre usar rutas relativas.

---

## 3. Sistema de Diseño (Design System)

### 3.1 Variables CSS (`:root`)
Cada página define estas custom properties:

```css
:root {
    --bg-color: #0f172a;          /* Fondo oscuro principal */
    --card-bg: #1e293b;           /* Fondo de tarjetas/paneles */
    --panel-bg: #111827;          /* Fondo de terminal (Módulo 2) */
    --text-main: #f8fafc;         /* Texto principal */
    --text-dim: #94a3b8;          /* Texto secundario/muted */
    --accent: [color por módulo]; /* Color de acento según contexto */
    --accent-glow: [rgba];        /* Versión transparente del acento */
    --transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
    --flow-line: #475569;         /* Color de líneas en diagramas */
}

[data-theme="light"] {
    --bg-color: #f1f5f9;
    --card-bg: #ffffff;
    --text-main: #0f172a;
    --text-dim: #475569;
    /* El acento se ajusta a una versión más oscura del mismo color */
}
```

### 3.2 Paleta de colores por módulo

**Módulo 1 (`clase1/`)** — tema violeta/indigo:
- Card Indigo: `#818cf8` (light: `#4f46e5`)
- Card Rose: `#fb7185` (light: `#e11d48`)
- Card Cyan: `#22d3ee` (light: `#0891b2`)
- Card Emerald: `#34d399` (light: `#059669`)

**Módulo 2 (`clase2/`)** — tema verde/violeta/ámbar:
- Card Emerald (Variables): `#34d399` (light: `#059669`)
- Card Amber (Condicionales): `#fbbf24` (light: `#d97706`)
- Card Violet (Ciclos/Repetición): `#a78bfa` (light: `#7c3aed`)

**Hub Módulo 1** — acento base: `#a855f7`
**Hub Módulo 2** — acento base: `#10b981`

### 3.3 Tipografía

```html
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&family=Outfit:wght@400;600;700;800&display=swap" rel="stylesheet">
```

- `Inter` → cuerpo de texto (`font-family: 'Inter', sans-serif`)
- `Outfit` → headings h1, h2, h3 (`font-family: 'Outfit', sans-serif`)
- `Fira Code` → código en terminal del Módulo 2 (importar solo cuando se use)

### 3.4 Animaciones estándar

```css
@keyframes fadeInUp {
    from { opacity: 0; transform: translateY(30px); }
    to   { opacity: 1; transform: translateY(0); }
}
@keyframes fadeInDown {
    from { opacity: 0; transform: translateY(-30px); }
    to   { opacity: 1; transform: translateY(0); }
}
```

- Usar `animation: fadeInUp 0.8s cubic-bezier(0.4, 0, 0.2, 1) forwards` en containers.
- Hover en tarjetas: `transform: translateY(-10px)` + `box-shadow` con `--accent-glow`.
- Hover en back-link: `transform: translateX(-5px)`.

---

## 4. Patrones de Componentes

### 4.1 Toggle de Tema (presente en TODAS las páginas)

```html
<button id="themeToggle">☀️ Modo Claro</button>

<script>
    const toggleBtn = document.getElementById('themeToggle');
    const root = document.documentElement;
    if (localStorage.getItem('theme') === 'light') {
        root.setAttribute('data-theme', 'light');
        toggleBtn.innerHTML = '🌙 Modo Oscuro';
    }
    toggleBtn.addEventListener('click', () => {
        if (root.getAttribute('data-theme') === 'light') {
            root.removeAttribute('data-theme');
            localStorage.setItem('theme', 'dark');
            toggleBtn.innerHTML = '☀️ Modo Claro';
        } else {
            root.setAttribute('data-theme', 'light');
            localStorage.setItem('theme', 'light');
            toggleBtn.innerHTML = '🌙 Modo Oscuro';
        }
    });
</script>
```

> **Regla:** Toda página nueva DEBE incluir este bloque exacto. El botón puede tener clase `.theme-btn` o `id="themeToggle"`, pero siempre estilizado como pill redondeado.

### 4.2 Back-link estándar

```html
<!-- Dentro de clase1/ o clase2/ → hacia el hub de módulo -->
<a href="clase2.html" class="back-link">← Volver a Módulo 2</a>

<!-- En hub de módulo → hacia index -->
<a href="../index.html" class="back-link">
    <svg>...</svg> Hub Principal
</a>
```

### 4.3 Tarjetas de Hub (`.content-card`)

Patrón de tarjeta usado en `clase1.html` y `clase2.html`:

```html
<a href="pagina.html" class="content-card card-violet">
    <div>
        <span class="card-tag">Etiqueta</span>
        <h2 style="color: var(--accent);">Título</h2>
        <p>Descripción...</p>
    </div>
    <div class="card-action">Aprender <span>&rarr;</span></div>
</a>
```

Clases de color disponibles: `.card-emerald`, `.card-amber`, `.card-violet`, `.card-indigo`, `.card-rose`, `.card-cyan`.

### 4.4 Layout dual del Módulo 2 (código + diagrama)

Todas las páginas `pseint-*.html` usan este layout split 50/50:

```
┌─────────────────────┬─────────────────────┐
│   .term-panel       │   .diagram-panel    │
│   (pseudocódigo)    │   (diagrama flujo)  │
│                     │                     │
│   .terminal         │   .flowchart        │
│   > código PseInt   │   > shapes CSS      │
│   > hover resalta   │   > hover tooltip   │
└─────────────────────┴─────────────────────┘
```

CSS base:
```css
.workspace {
    display: grid;
    grid-template-columns: 1fr 1fr;
    flex-grow: 1;
    min-height: calc(100vh - 60px);
}
@media (max-width: 900px) {
    .workspace { grid-template-columns: 1fr; }
}
```

### 4.5 Formas del diagrama de flujo (CSS puro)

```css
/* Terminal (inicio/fin) — pastilla redondeada */
.shape-terminal { width: 180px; background: #64748b; border-radius: 30px; min-height: 40px; }

/* Proceso — rectángulo */
.shape-process  { width: max-content; padding: 10px 25px; background: #eab308; border-radius: 4px; }

/* Decisión — rombo con clip-path */
.shape-decision { width: 180px; height: 90px; background: #c678dd;
                  clip-path: polygon(50% 0%, 100% 50%, 50% 100%, 0% 50%); }

/* IO/Entrada-Salida — paralelogramo con skew */
.shape-io       { width: max-content; background: #10b981; transform: skew(-20deg); padding: 5px 35px; }
.shape-io span  { transform: skew(20deg); display: block; } /* Contra-rotar el texto */
```

**Estado `highlight` (al hacer hover en código):**
```css
.shape.highlight {
    transform: scale(1.1);
    box-shadow: 0 0 25px var(--accent);
    filter: brightness(1.2);
    z-index: 10;
}
```

### 4.6 Sistema de sincronización código↔diagrama

```html
<!-- En el código: data-target apunta al id del shape -->
<span class="code-line" data-target="shape-id">Pseudocódigo</span>

<!-- En el diagrama: id coincide con data-target -->
<div id="shape-id" class="shape shape-process" data-tooltip="Explicación">...</div>
```

```javascript
document.querySelectorAll('.code-line').forEach(line => {
    line.addEventListener('mouseenter', function () {
        const el = document.getElementById(this.getAttribute('data-target'));
        if (el) el.classList.add('highlight');
    });
    line.addEventListener('mouseleave', function () {
        const el = document.getElementById(this.getAttribute('data-target'));
        if (el) el.classList.remove('highlight');
    });
});
```

### 4.7 Tooltip flotante en diagramas

```javascript
const tooltip = document.createElement('div');
tooltip.className = 'tooltip-box';
document.body.appendChild(tooltip);

document.querySelectorAll('.shape[data-tooltip]').forEach(shape => {
    shape.addEventListener('mouseenter', function (e) {
        tooltip.textContent = this.getAttribute('data-tooltip');
        tooltip.style.opacity = '1';
        tooltip.style.left = e.pageX + 'px';
        tooltip.style.top = (e.pageY - 15) + 'px';
        tooltip.style.transform = 'translate(-50%, -100%)';
    });
    shape.addEventListener('mousemove', e => {
        tooltip.style.left = e.pageX + 'px';
        tooltip.style.top = (e.pageY - 15) + 'px';
    });
    shape.addEventListener('mouseleave', () => { tooltip.style.opacity = '0'; });
});
```

---

## 5. Sintaxis PseInt de Referencia

Las páginas del Módulo 2 modelan exactamente esta sintaxis:

```
Algoritmo NombreAlgoritmo
  Definir variable Como Tipo;  // Tipos: Entero, Real, Caracter, Logico
  variable <- valor;           // Asignación
  Leer variable;                // Entrada
  Escribir "texto" , variable; // Salida

  Si condicion Entonces         // Condicional
    ...
  SiNo
    ...
  FinSi

  Segun variable Hacer          // Switch
    valor1: ...
    valor2: ...
    De Otro Modo: ...
  FinSegun

  Mientras condicion Hacer      // While (pre-condición)
    ...
  FinMientras

  Repetir                       // Do-While (post-condición)
    ...
  Hasta Que condicion

  Para i <- inicio Hasta fin Con Paso incremento Hacer  // For
    ...
  FinPara
FinAlgoritmo
```

---

## 6. Reglas y Restricciones para la IA

### ✅ Siempre hacer
- Cada página HTML es **autocontenida** (CSS y JS dentro del mismo archivo, en `<style>` y `<script>`).
- Aplicar el toggle de tema con `localStorage` en **todas** las páginas nuevas.
- Usar rutas **relativas** para todos los `href` y assets.
- Mantener la **responsividad**: breakpoint principal en `max-width: 900px`.
- Al agregar una página nueva de PseInt, agregarla también como tarjeta en `clase2/clase2.html`.
- Al agregar cualquier módulo nuevo, agregarlo como tarjeta en `index.html`.
- Respetar el esquema de colores existente: no introducir colores genéricos (plain red, blue, green).

### ❌ Nunca hacer
- No usar frameworks CSS (Tailwind, Bootstrap, etc.).
- No usar librerías JavaScript externas (jQuery, React, etc.).
- No usar rutas absolutas en `href` o `src`.
- No crear archivos CSS o JS separados — todo va inline en el HTML.
- No romper la sincronización `data-target` / `id` entre código y diagrama.
- No eliminar el atributo `[data-theme="light"]` de los estilos — es necesario para el modo claro.

---

## 7. Cómo Agregar una Nueva Página de PseInt

1. Copiar la estructura de cualquier `pseint-*.html` existente como base.
2. Reemplazar el pseudocódigo en el `.terminal-body` añadiendo los `data-target` correctos.
3. Construir el diagrama de flujo en `.diagram-panel` usando las clases de shapes.
4. Agregar los `id` en los shapes que coincidan con los `data-target` del código.
5. Añadir `data-tooltip` en cada shape con su explicación pedagógica.
6. Registrar la nueva página como `.content-card` en `clase2/clase2.html`.
7. Actualizar el `README.md` con la nueva página.

---

## 8. Autor y Contexto Académico

- **Autor:** Germán Mardones (`mardones.german@gmail.com`)
- **Institución:** INACAP Chile
- **Carrera:** Ingeniería en Computación e Informática
- **Asignatura:** TI3011 — Lógica y Resolución de Problemas
- **Año:** 2026
