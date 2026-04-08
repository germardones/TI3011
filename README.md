# TI3011 — Lógica y Resolución de Problemas

> Plataforma de aprendizaje interactivo para la asignatura **TI3011** del programa de Ingeniería en Computación e Informática, **INACAP**.

---

## 📚 Contexto del Proyecto

Este proyecto es una **plataforma web de micro-aprendizaje** diseñada para complementar las clases presenciales de la asignatura *Lógica y Resolución de Problemas*. Cada módulo presenta los contenidos del curso de forma visual e interactiva, combinando pseudocódigo, diagramas de flujo animados y tarjetas conceptuales.

El sitio fue construido íntegramente con **HTML, CSS y JavaScript vanilla** (sin frameworks), priorizando la experiencia visual con un sistema de diseño glassmorphism en modo oscuro/claro.

---

## 🗂️ Estructura del Proyecto

```
TI3011/
│
├── index.html              # Hub principal — listado de módulos
│
├── clase1/                 # Módulo 1: Elementos de Lógica
│   ├── clase1.html             # Hub del Módulo 1
│   ├── problematica.html       # 1.1.1 — Alcance y Contexto
│   ├── modelo-polya.html       # 1.1.2 — Modelo de Polya (4 pasos)
│   └── diagramas.html          # 1.1.3 y 1.1.4 — Diagramas y Operadores
│
└── clase2/                 # Módulo 2: Entorno PseInt
    ├── clase2.html             # Hub del Módulo 2
    ├── pseint-concepto-variable.html   # ¿Qué es una Variable?
    ├── pseint-variables.html           # Declaración & Variables
    ├── pseint-tipos.html               # Tipos de Datos Primitivos
    ├── pseint-condicionales.html       # Si-Entonces-Sino (If-Else)
    ├── pseint-segun.html               # Según (Switch)
    ├── pseint-ciclos.html              # Mientras (While)
    ├── pseint-repetir.html             # Repetir Hasta (Do-While)
    └── pseint-para.html                # Para (For)
```

---

## 🧩 Módulos de Contenido

### Módulo 1 — Resolución de Problemas
Explora los fundamentos del pensamiento lógico estructurado para construir soluciones pertinentes.

| Página | Tema | Descripción |
|--------|------|-------------|
| `problematica.html` | Alcance y Contexto | Tarjetas interactivas con flip-3D sobre identificación de variables y análisis del entorno |
| `modelo-polya.html` | Modelo de Polya | Visualizador interactivo de los 4 pasos: Entender, Planificar, Ejecutar y Revisar |
| `diagramas.html` | Diagramas y Operadores | Simbología de diagramas de flujo y operadores lógicos AND, OR, NOT |

### Módulo 2 — Entorno PseInt
Profundiza en la codificación en pseudocódigo con visualización dual: código + diagrama de flujo sincronizados.

| Página | Tema | Estructura |
|--------|------|-----------|
| `pseint-concepto-variable.html` | ¿Qué es una Variable? | Concepto base — nombre, tipo y valor |
| `pseint-variables.html` | Declaración & Variables | Layout dual código/diagrama |
| `pseint-tipos.html` | Tipos de Datos Primitivos | Entero, Real, Carácter, Lógico |
| `pseint-condicionales.html` | Si-Entonces-Sino | Rombo de decisión con ramas V/F |
| `pseint-segun.html` | Según (Switch) | Casos múltiples sobre una variable |
| `pseint-ciclos.html` | Mientras (While) | Bucle con condición pre-evaluada |
| `pseint-repetir.html` | Repetir Hasta (Do-While) | Bucle con condición post-evaluada |
| `pseint-para.html` | Para (For) | Bucle con contador, paso e incremento |

---

## 🎨 Sistema de Diseño

- **Modo oscuro/claro** — persistido vía `localStorage`
- **Glassmorphism** — `backdrop-filter: blur` + transparencias
- **Animaciones** — `fadeInUp`, hover con `translateY`, transiciones cúbicas
- **Tipografía** — `Inter` (cuerpo) + `Outfit` (títulos) + `Fira Code` (terminal)
- **Color por módulo:**
  - Módulo 1: Índigo `#818cf8` · Rosa `#fb7185` · Cyan `#22d3ee`
  - Módulo 2: Esmeralda `#34d399` · Ámbar `#fbbf24` · Violeta `#a78bfa`

### Interactividad en Módulo 2
Cada página de PseInt implementa un layout dividido **50/50**:
- **Panel izquierdo:** Terminal con pseudocódigo resaltado por sintaxis. Al pasar el cursor sobre una línea, el elemento correspondiente en el diagrama se ilumina.
- **Panel derecho:** Diagrama de flujo con formas CSS puras y tooltips flotantes al hacer hover sobre cada nodo.

---

## 🛠️ Tecnologías

| Tecnología | Uso |
|-----------|-----|
| HTML5 Semántico | Estructura de todas las páginas |
| CSS3 Vanilla | Diseño completo, animaciones, modo oscuro/claro |
| JavaScript (ES6+) | Lógica de tema, interactividad código↔diagrama, tooltips |
| Google Fonts | `Inter`, `Outfit`, `Fira Code` |
| CSS Custom Properties | Sistema de tokens de diseño (colores, transiciones) |
| `localStorage` | Persistencia del tema seleccionado por el usuario |

> **Sin dependencias externas.** No se utiliza ningún framework CSS ni librería JavaScript.

---

## 🚀 Ejecución Local

Al ser un proyecto de archivos estáticos, basta con abrir `index.html` directamente en el navegador:

```bash
# Opción 1 — Abrir directamente
start index.html

# Opción 2 — Servidor local con Python
python -m http.server 3000

# Opción 3 — Extensión Live Server en VS Code
# Click derecho en index.html → "Open with Live Server"
```

---

## 👤 Autor

**Germán Mardones**  
Estudiante INACAP — Ingeniería en Computación e Informática  
📧 mardones.german@gmail.com

---

## 📝 Notas Académicas

- Asignatura: **TI3011 — Lógica y Resolución de Problemas**
- Institución: INACAP Chile
- Período: 2026

