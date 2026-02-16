---
Document ID: IRA-MTR-001
Version: 1.0
Status: LOCKED
Authority: SINTERGIA™
Date: 2026-02-15
---

# IRA-MTR-001  
## MOTOR DETERMINÍSTICO IRA™ v1.0  
### Edición Institucional — CONSTITUCIONAL — LOCKED

Estado: LOCKED

---

## I. Naturaleza del Documento

IRA-MTR-001 define el motor matemático oficial y determinístico del estándar IRA™ v1.0.

Este documento constituye la autoridad computacional de:

- Cálculo estructural
- Clasificación (Tier)
- Asignación de estado
- Vigencia automática
- Reglas de derivación

El motor:

- Opera exclusivamente mediante reglas matemáticas.
- No admite intervención humana en cálculo, clasificación, interpretación ni asignación de estado.
- Produce salidas reproducibles: misma entrada → misma salida bajo misma versión.

---

## II. Variables de Entrada (D1–D8)

El motor recibe exactamente ocho (8) dimensiones estructurales:

D1 — Gobernanza y Autoridad  
D2 — Integridad Operativa  
D3 — Evidencia y Control  
D4 — Riesgo y Dependencia  
D5 — Coherencia Estructural  
D6 — Arquitectura de Información  
D7 — Densidad de Capacidad  
D8 — Elasticidad Estructural  

### Reglas

- Escala continua: 0.00 – 5.00
- Precisión interna obligatoria: dos (2) decimales
- No se admiten valores fuera del rango

---

## III. Escala y Precisión

Escala estructural:

0.00 – 5.00 (5.00 asintótico teórico)

Precisión interna obligatoria:

- Dos (2) decimales para todo cálculo interno.

Visual público permitido:

- Truncamiento a un (1) decimal.
- Prohibido redondeo.

El valor interno exacto (SCI_int) debe permanecer almacenado.

---

## IV. Fórmula Oficial (SCI™)

SCI™ = (D1 + D2 + D3 + D4 + D5 + D6 + D7 + D8) / 8

Ponderación:

- Igualitaria en versión 1.0.
- No admite ponderaciones sectoriales en esta versión.

---

## V. Regla de Truncamiento Público

Definiciones:

- SCI_int = valor interno con dos (2) decimales.
- SCI_pub = truncamiento de SCI_int a un (1) decimal.

Ejemplos:

- 3.29 → 3.2  
- 3.20 → 3.2  
- 3.99 → 3.9  

Regla:

- Se prohíbe redondeo.
- Solo truncamiento.

---

## VI. Sistema de Clasificación (Tier I–V)

Clasificación basada en SCI_int:

Tier I   — SCI < 2.50  
Tier II  — 2.50 ≤ SCI < 3.25  
Tier III — 3.25 ≤ SCI < 3.75  
Tier IV  — 3.75 ≤ SCI < 4.25  
Tier V   — SCI ≥ 4.25  

### Requisitos adicionales Tier IV

- Ninguna dimensión < 3.00

### Requisitos adicionales Tier V

- Todas las dimensiones ≥ 3.50  
- D6 ≥ 4.00  
- D8 ≥ 4.00  

La clasificación es automática.

Regla de Equivalencia WARNING

Toda evaluación clasificada como Tier I implica automáticamente estado WARNING.

No puede existir Tier I con estado ACTIVE.

La condición WARNING se determina exclusivamente por:

SCI_int < 2.50

No admite interpretación adicional.

---

## VII. Estados Estructurales

El motor asigna estado automáticamente.

ACTIVE  
Clasificación vigente dentro de parámetros.

WARNING  
SCI_int < 2.50

INACTIVE  
Caducidad sin reevaluación.

DOWNGRADED  
Se asigna automáticamente cuando, en una reevaluación OFFICIAL válida, el Tier resultante es inferior al Tier previamente vigente.


---

### PERMANENT — Estabilidad Constitucional Sostenida

Aplicable exclusivamente a evaluaciones `OFFICIAL`.

No aplica a `EXPLORATORY`.

#### Condiciones de Activación

PERMANENT se asigna automáticamente cuando:

1. Existen tres (3) reevaluaciones consecutivas en modo OFFICIAL.
2. Ninguna reevaluación produce descenso de Tier.
3.	En las tres evaluaciones consecutivas:
	•	SCI_int ≥ 4.00
	•	Clasificación mínima: Tier IV

4. Ocurren dentro de 24 meses desde la primera.
5. Todas bajo la misma versión constitucional.

#### Condiciones Técnicas

- Cálculo automático.
- Basado en historial persistido.
- Sin intervención humana.
- Sin override institucional.

#### Pérdida del Estado

Se pierde automáticamente si:

- Hay descenso de Tier.
- SCI_int < 4.00
- Expira vigencia sin reevaluación.

No existe período de gracia.

Vigencia bajo PERMANENT

La asignación del estado PERMANENT:
	•	No altera la vigencia (TTL) definida por Tier.
	•	No extiende plazo de certificación.
	•	No modifica reglas de caducidad.

La vigencia continúa rigiéndose por la sección VIII.

PERMANENT constituye un estado estructural superior a ACTIVE, pero no modifica la clasificación Tier.

---

## VIII. Vigencia (TTL)

Tier I   — 3 meses  
Tier II  — 4 meses  
Tier III — 6 meses  
Tier IV  — 12 meses  
Tier V   — 18 meses  

Al vencimiento:

- Al vencimiento de vigencia en evaluaciones OFFICIAL, el estado pasa automáticamente a INACTIVE.
- No existe extensión manual.

---

## IX. Radar Estructural (Derivado)

Representación gráfica orientativa sin impacto en cálculo.

E1 — D1  
E2 — D2  
E3 — D3  
E4 — promedio(D4, D8)  
E5 — D6  
E6 — promedio(D5, D7)  

Reglas:

- Derivado exclusivamente del cálculo interno.
- No altera SCI.
- No altera Tier.
- No altera Estado.

---

## X. Priority Signals™ (Top 3)

Algoritmo:

1. Ordenar dimensiones por menor valor.
2. Seleccionar tres (3) más bajas.
3. Resolver empates según prioridad fija:

D4 > D6 > D3 > D7 > D2 > D8 > D5 > D1

Salida:

- Determinística.
- No personalizada.

---

## XI. Determinismo Computacional

El motor:

- Opera bajo cálculo automático.
- No permite edición manual.
- No admite modificación parcial.
- No admite interpretación humana.

La reevaluación completa es el único mecanismo de actualización.

---

## XII. Control de Versión

IRA-MTR-001 pertenece a IRA™ v1.0 Constitucional — LOCKED.

Toda modificación requiere:

- Nueva versión numerada.
- Documento formal.
- Registro institucional.
- Preservación histórica.

No existe edición retroactiva.

La generación de hash estructural se regula bajo IRA-HSC-001.

---

## XIII. Declaración Constitucional

IRA-MTR-001 queda declarado como el Motor Determinístico oficial del estándar IRA™ v1.0.

Emitido por:

Julio César Moya  
Founder & Systems Architect  
SINTERGIA™

Fecha oficial de emisión: 15 de febrero de 2026  
Status: LOCKED  
Versión: 1.0