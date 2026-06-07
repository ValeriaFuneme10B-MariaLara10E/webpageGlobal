# Plan de desarrollo — Página web C8 + C9

## Criterios de diseño del plan

- Una sola página `index.html` con dos modos integrados
- Cada etapa produce código funcional y verificable en navegador
- Se construye en capas: estructura → lógica → visualización → datos
- Ninguna etapa bloquea la siguiente si el usuario no tiene GitHub aún

---

## Etapa 1 — Esqueleto HTML + CSS base

**Qué se construye:** estructura de la página completa sin lógica aún.

- Layout de dos modos (tabs o secciones): Simulación / Modelado de datos
- Panel de controles (inputs) para cada distribución en C8
- Área de canvas para la gráfica
- Sección "AI development record" visible con placeholder de links
- Estilos CSS: colores, tipografía, responsividad básica

**Verificación:** la página carga en el navegador, los tabs cambian de vista, todos los inputs están presentes y la sección AI es visible.

---

## Etapa 2 — Motor de distribuciones (C8 — lógica JS)

**Qué se construye:** funciones matemáticas para las 5 distribuciones.

- PDF de cada distribución: Uniforme, Triangular, Lineal, Por partes, Normal
- CDF (probabilidad acumulada) para cada distribución
- Cálculo de P(X<x), P(X>x), P(x₁<X<x₂) para cada una
- Funciones independientes, sin depender aún del canvas

**Verificación:** llamadas de prueba en consola del navegador devuelven valores numéricos correctos para cada distribución.

---

## Etapa 3 — Visualización Canvas (C8 — gráfica + sombreado)

**Qué se construye:** renderizado de las PDFs en canvas y conexión con inputs.

- Dibujo de la curva PDF en canvas para cada distribución
- Sombreado del área según región seleccionada (izquierda / derecha / entre)
- Actualización automática al cambiar parámetros o bounds
- Display del valor numérico de probabilidad en pantalla

**Verificación:** RS-01, RS-02 y RS-03 cumplen criterios de aceptación. **C8 completo.**

---

## Etapa 4 — Carga y procesamiento CSV (C9 — datos)

**Qué se construye:** módulo de ingesta de datos.

- Input de tipo file que acepta CSV
- Parser CSV en JS vanilla (sin librerías)
- Extracción de la columna numérica automáticamente
- Cálculo de estadísticas básicas: n, min, max, μ, σ
- Display de estadísticas en pantalla tras carga

**Verificación:** los 3 datasets se cargan correctamente y muestran estadísticas correctas (valores ya conocidos del paso anterior).

---

## Etapa 5 — Histograma (C9 — visualización de datos)

**Qué se construye:** histograma de los datos cargados en canvas.

- Cálculo automático de bins (número de intervalos)
- Dibujo del histograma en canvas
- Escala vertical en densidad (no frecuencia) para que sea comparable con la PDF

**Verificación:** los 3 datasets producen histogramas visualmente coherentes con la distribución conocida de los datos.

---

## Etapa 6 — Ajuste de modelos y superposición (C9 — modelado)

**Qué se construye:** estimación de parámetros + PDF superpuesta sobre histograma.

- Estimación de parámetros para los 5 modelos desde los datos cargados
- Display de parámetros estimados en pantalla
- Dibujo de la PDF ajustada sobre el histograma en el mismo canvas
- Texto de interpretación automática del ajuste

**Verificación:** RM-01, RM-02 y RM-03 cumplen criterios de aceptación. **C9 completo.**

---

## Etapa 7 — Integración final y pulido

**Qué se construye:** conexión entre modos y detalles finales.

- Links definitivos en sección "AI development record"
- Revisión de casos borde (parámetros inválidos, CSV mal formado)
- Mensajes de error amigables al usuario
- Revisión de checklist completo de C8 y C9

**Verificación:** checklist completo de la guía sin ítems pendientes.

---

## Resumen de etapas

| Etapa | Qué produce | Criterio cubierto |
|---|---|---|
| 1 | Esqueleto HTML + CSS | RG-01, RG-02 (estructura) |
| 2 | Motor de distribuciones JS | RS-01, RS-03 (lógica) |
| 3 | Canvas + interactividad | RS-02, RS-03 (visual) — **C8 listo** |
| 4 | Parser CSV + estadísticas | RM-01 |
| 5 | Histograma en densidad | RM-03 (parcial) |
| 6 | Ajuste de modelos + superposición | RM-02, RM-03 — **C9 listo** |
| 7 | Integración + pulido | RG-02 definitivo, checklist |
