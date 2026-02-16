---
Document ID: IRA-IIGF-001
Version: 1.0
Status: CANDIDATE
Authority: SINTERGIA™
Date: 2026-02-15
---

# IRA-IIGF-001
## IMPLEMENTATION & INSTITUTIONAL GOVERNANCE FRAMEWORK IRA™ v1.0
### Edición Institucional — CONSTITUCIONAL — CANDIDATE

Estado: CANDIDATE

---

## I. Naturaleza del Documentogit add 01_constitution/IRA-IIGF-001__Implementacion_Gobernanza_v1.0__CANDIDATE.md

IRA-IIGF-001 define el marco constitucional de implementación y gobernanza institucional del estándar IRA™ v1.0.

Este documento establece:

- Reglas de implementación obligatoria (backend, storage, verificación).
- Reglas de gobernanza institucional del estándar (cierre, control, compatibilidad).
- Reglas de publicación, auditoría y verificación externa.
- Reglas de integridad operativa entre documentos constitucionales.
- Reglas de no-intervención humana en resultados.

Este documento es subordinado a IRA-CON-001 y debe ser consistente con:

- IRA-FRW-001  
- IRA-MTR-001  
- IRA-HSC-001  

En caso de conflicto interpretativo, prevalece la jerarquía definida en IRA-CON-001.

---

## II. Principios de Implementación

1. La implementación debe cumplir estrictamente la jerarquía constitucional (IRA-CON-001).
2. Ningún componente puede introducir lógica fuera de IRA-MTR-001 para cálculo de resultado.
3. La verificación pública solo consulta registros persistidos y nunca recalcula.
4. La emisión pública (PDF/VERIFY) exige persistencia previa completa del registro.
5. Toda ejecución debe ser determinística bajo `version_id`.
6. Toda emisión debe ser trazable a una versión constitucional específica del estándar.

---

## III. Componentes Institucionales Mínimos

Obligatorio en v1.0:

- Backend Institucional (única autoridad de ejecución y emisión).
- Motor Determinístico (IRA-MTR-001) como única fuente de cálculo.
- Registro Persistido (DB) con campos mínimos definidos en IRA-HSC-001.
- Hash & Structural Control (IRA-HSC-001) para integridad verificable.
- Endpoint VERIFY (solo consulta de registros persistidos).

Prohibido:

- Ejecutar motor desde frontend.
- Recalcular resultado en VERIFY.
- Overrides manuales de tier/state/SCI en modo OFFICIAL.
- Emisión pública sin registro previamente persistido.

---

## IV. Reglas de Persistencia y Emisión

Regla de orden (inmutable y obligatoria):

1) Ejecutar motor (IRA-MTR-001)  
2) Construir payload canónico (IRA-HSC-001)  
3) Calcular hash SHA-256 (server-side)  
4) Persistir registro completo  
5) Emitir PDF / habilitar VERIFY  

La secuencia anterior no puede alterarse.

Cualquier emisión sin persistencia previa constituye violación constitucional del estándar. La violación del orden invalida la emisión institucional bajo v1.0.

---

## V. Modos de Ejecución

### V.1 OFFICIAL

- Requiere persistencia completa.
- Requiere `hash_sha256` obligatorio.
- Requiere `expires_at_utc` obligatorio. Debe cumplir igualmente con las reglas estructurales definidas en IRA-HSC-001.
- Requiere `version_id` explícito.
- Prohibido emitir OFFICIAL sin registro verificable.
- El resultado OFFICIAL solo puede derivarse del backend institucional.

### V.2 EXPLORATORY

- Requiere persistencia (mínimo obligatorio v1.0).
- `expires_at_utc` obligatorio (ts_utc + 30 días exactos). Debe cumplir igualmente con las reglas estructurales definidas en IRA-HSC-001.
- No constituye certificación constitucional.
- Las políticas de emisión pública pueden restringirse.
- No puede presentarse como resultado oficial del estándar.

---

## VI. Gobernanza Institucional del Estándar

### VI.1 Control de Cambios

- Cambios constitucionales solo por nueva versión numerada.
- Versiones anteriores permanecen preservadas.
- Prohibida edición retroactiva de documentos LOCKED.
- Toda nueva versión debe mantener trazabilidad documental explícita.

### VI.2 Criterios de Cierre (LOCKED)

IRA-IIGF-001 solo puede pasar a LOCKED cuando exista evidencia verificable de:

- Implementación backend confirmada.
- Validación cruzada con IRA-MTR-001 (cálculo) y IRA-HSC-001 (hash/payload).
- Validación de esquema DB vs campos obligatorios.
- Prueba de VERIFY (consulta-only) confirmada.
- Confirmación de no-recalculo en endpoint público.

---

## VII. Auditoría y Evidencia de Cumplimiento

La implementación debe poder demostrar:

- `version_id` incluido en todo registro emitido.
- `evaluation_id` trazable y único.
- hash_sha256 verificable contra el registro persistido.
- Ausencia de recálculo en VERIFY.
- Registros inmutables post-emisión.
- Consistencia estructural entre payload persistido y hash calculado.

Recomendado:

- Logs de ejecución.
- Logs de generación de hash.
- Rate limiting en VERIFY.
- Monitoreo de integridad de registros persistidos.

---

## VIII. Publicación y Verificación Externa

VERIFY permite:

- Validar existencia del registro emitido.
- Validar integridad mediante hash (cuando aplique).
- Consultar estado, tier, timestamps, versión y vigencia según política pública.
- Confirmar trazabilidad institucional del resultado emitido.

VERIFY no permite:

- Recalcular resultados.
- Reconstruir payload.
- Ejecutar motor.
- Alterar registros persistidos.

---

## IX. Declaración Constitucional

IRA-IIGF-001 queda declarado como el marco oficial de implementación y gobernanza institucional del estándar IRA™ v1.0.

Este documento establece los límites técnicos y jurídicos de ejecución, emisión y verificación del sistema IRA™ bajo la jerarquía constitucional vigente.

Emitido por:

Julio César Moya  
Founder & Systems Architect  
SINTERGIA™

Fecha oficial de emisión: 15 de febrero de 2026  
Status: CANDIDATE  
Versión: 1.0