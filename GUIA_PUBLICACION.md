# Guía de publicación — CRAMPS

Esta guía responde a una pregunta concreta que hiciste: **¿dónde van las pruebas y experimentos al momento de publicar?** La respuesta corta es que el código y los datos **no van dentro del PDF** — van en un repositorio enlazado. Abajo está el detalle completo.

---

## 1. Cómo se separa un paper de su evidencia

Un paper académico tiene tres capas, y cada una vive en un lugar distinto:

| Capa | Qué contiene | Dónde vive |
|------|--------------|------------|
| **El paper (PDF)** | Argumento, proposiciones, tablas resumen, figuras clave | arXiv / conferencia |
| **El suplemento** | Detalle de cada experimento, parámetros, tablas completas | Anexo del PDF o archivo aparte |
| **El código y datos** | Scripts, semillas, corpus, instrucciones para reproducir | Repositorio (GitHub/Zenodo) |

El PDF **no incluye el código**. Incluye una línea en "Experimental Details" que dice `Code: https://github.com/...`. Los revisores siguen ese link para verificar. Esto es el estándar universal en ML y sistemas complejos.

---

## 2. Qué archivo va a dónde

Tienes ahora estos archivos:

### Van a arXiv (dentro del zip)
- `cramps_paper_final.tex` → renómbralo `main.tex`
- `appendix_en.tex` — el apéndice de isomorfismos (decisión estratégica, ver §4)
- `cramps.bib` — bibliografía
- `cramps_paper_figure.png` — figura principal
- `cramps_paper_final.bbl` — bibliografía pre-compilada

### Van al repositorio de GitHub (NO al PDF)
- Todo el código en `eval/` y `core/`
- `cramps_experiments.pdf` — el suplemento de experimentos (también puede ir como "ancillary file" en arXiv)
- El corpus filtrado o el script que lo genera
- Un `README.md` con instrucciones

### Es material de divulgación (ni paper ni repo)
- El podcast en español
- La visualización interactiva
- La versión en español del paper (puede ir a arXiv como paper companion)

---

## 3. Las tres formas de incluir experimentos al publicar

Tienes tres opciones, de menor a mayor formalidad:

### Opción A — Link al repositorio (mínimo, estándar)
El PDF dice `Code: https://github.com/manolo-delabarra/cramps`. Todo el detalle vive ahí. Es lo mínimo aceptable y lo más común.

### Opción B — Ancillary files en arXiv (recomendado)
arXiv permite subir "ancillary files" junto al paper — archivos que aparecen en una carpeta al lado del PDF sin ser parte de él. Aquí subes `cramps_experiments.pdf` y opcionalmente los scripts. El lector ve "Ancillary files" en la página de arXiv y puede descargarlos. **Esta es la mejor opción para ti** porque el suplemento de experimentos queda inmediatamente accesible sin depender de GitHub.

### Opción C — Apéndice dentro del PDF (máxima formalidad)
Mueves todo el contenido de `cramps_experiments.pdf` como apéndices del paper principal. Hace el PDF más largo (sería ~19 páginas) pero todo está en un solo documento. Se usa cuando la conferencia exige que todo sea auto-contenido.

**Mi recomendación: Opción B.** El paper queda limpio en 13 páginas, y el suplemento de experimentos va como ancillary file en arXiv, visible y descargable.

---

## 4. La decisión estratégica del apéndice de isomorfismos

El apéndice que conecta CRAMPS con Gramsci, Bourdieu, dopamina y cortisol es un arma de doble filo, y dónde publiques determina si ayuda o resta:

- **Si apuntas a NeurIPS / AAMAS / ICLR (venues de ML puro):** saca el apéndice del paper principal. Mándalo como ancillary file o como paper-compañero separado. En esos venues, las analogías filosóficas restan credibilidad técnica.
- **Si apuntas a Complexity / Cognitive Systems Research / Adaptive Behavior / AI & Society:** déjalo en el cuerpo. Ahí es tu diferenciador y suma.

Tienes ambas versiones listas. La decisión es tuya y depende del venue.

---

## 5. Ruta de publicación paso a paso

### Paso 1 — Repositorio primero (esta semana)
1. Crea el repo `github.com/manolo-delabarra/cramps`
2. Sube `core/`, `eval/`, un `README.md`, y `requirements.txt`
3. Sube `cramps_experiments.pdf` a la raíz
4. Añade una licencia (MIT o CC-BY 4.0 para investigación)

### Paso 2 — arXiv (cuando el repo esté arriba)
1. Cuenta en arxiv.org (necesitas endorsement la primera vez en algunas categorías; cs.MA suele requerirlo — pídelo a un colega con papers previos o usa el sistema de endorsement automático)
2. Categoría primaria: **cs.MA** (Multiagent Systems)
3. Cross-list: **cs.LG** (Machine Learning) y opcionalmente **nlin.AO** (Adaptation and Self-Organizing Systems)
4. Sube el zip `cramps_arxiv_en.zip`
5. Sube `cramps_experiments.pdf` como **ancillary file**
6. En "Comments" pon: `13 pages, 5 figures. Code and full experimental supplement at [github URL]. Spanish companion version available.`

### Paso 3 — Versión española (opcional, mismo día)
Segunda submission, mismo cs.MA, en Comments: `Spanish translation of arXiv:XXXX.XXXXX`

### Paso 4 — Conferencia (meses después)
Con el arXiv publicado y citable, apunta a un workshop primero (NeurIPS workshops de multi-agent o fairness abren sept-dic). Un workshop es menos riesgoso que el track principal y te da feedback antes de un envío grande.

---

## 6. Checklist final antes de subir

- [ ] El repo existe y el link en el paper funciona (ya no dice `[REPOSITORY]`)
- [ ] El suplemento de experimentos compila y es legible
- [ ] Decidiste venue → decidiste si el apéndice va dentro o fuera
- [ ] El abstract reconoce el null result bajo poder limitado (ya lo hace)
- [ ] La circularidad métrica-goal está nombrada en Limitations (ya lo está)
- [ ] Todas las afirmaciones grandes tienen su caveat estadístico (ya lo tienen)
- [ ] Las semillas están documentadas para reproducibilidad (seed 42)

---

## 7. Lo que un revisor va a verificar

Cuando un revisor reciba esto, va a:

1. **Leer el abstract** → buscar si las afirmaciones son honestas. ✓ (ya reconoce el null result)
2. **Mirar las tablas** → verificar que los números cuadran entre tablas. ✓ (0.387 puro vs 0.360 heterogéneo ahora están separados explícitamente)
3. **Seguir el link al código** → intentar reproducir. Por eso el repo debe estar arriba ANTES del arXiv.
4. **Atacar la afirmación más débil** → que es el kill test sub-potenciado. Ya está blindado como "null result under limited power".
5. **Cuestionar la generalización** → ya está acotada a "preliminary, requires N∈{50,100,200}".

El paper está preparado para sobrevivir esa revisión. No porque sea perfecto, sino porque es honesto sobre dónde no es perfecto. Eso es exactamente lo que distingue un paper que sobrevive de uno que no.
