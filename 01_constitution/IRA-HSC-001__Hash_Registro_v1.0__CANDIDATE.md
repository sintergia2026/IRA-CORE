---
Document ID: IRA-HSC-001
Version: 1.0
Status: CANDIDATE
Authority: SINTERGIA™
Date: 2026-02-15
---

# IRA-HSC-001
## HASH & STRUCTURAL CONTROL IRA™ v1.0
### Edición Institucional — CONSTITUCIONAL — CANDIDATE

Estado: CANDIDATE

---

## I. Naturaleza del Documento

IRA-HSC-001 define el mecanismo constitucional de:

- Generación de hash estructural (SHA-256)
- Normalización canónica estricta de datos para hashing
- Registro de integridad (persistencia mínima obligatoria)
- Verificación pública basada exclusivamente en registro persistido
- Prohibición absoluta de recalculo por fuentes no autorizadas

Este documento controla la cadena de verificabilidad del estándar IRA™.

El hash estructural:

- No es firma humana.
- No es validación manual.
- Es prueba determinística de integridad del resultado emitido bajo una versión específica del estándar.

---

## II. Principio Rector

1. Solo Backend Institucional puede generar:
   - `evaluation_id`
   - `ts_utc`
   - `hash_sha256`

2. El `hash_sha256` se calcula únicamente desde un payload canónico definido en este documento.

3. El sistema de verificación:
   - No recalcula resultados.
   - No ejecuta el motor.
   - No reconstruye el payload.
   - Solo consulta registros persistidos.

---

## III. Alcance y Aplicación

IRA-HSC-001 aplica a:

- Evaluaciones `OFFICIAL` (obligatorio)
- Evaluaciones `EXPLORATORY`
- Generación de PDF institucional
- Endpoints `/verify`

Reglas:

- En `OFFICIAL`, `hash_sha256` es obligatorio.
- En `OFFICIAL`, `expires_at_utc` es obligatorio y no puede ser NULL.
- En `EXPLORATORY`, `expires_at_utc` también es obligatorio.
- No se permite el uso de NULL en `expires_at_utc` en v1.0.
- En EXPLORATORY, hash_sha256 puede ser generado o no según política operativa vigente, 
pero no es requisito constitucional obligatorio.

### Determinación de `expires_at_utc`

En evaluaciones `OFFICIAL`:
- `expires_at_utc` se determina exclusivamente por las reglas de vigencia (TTL) definidas en IRA-MTR-001.

En evaluaciones `EXPLORATORY`:
- `expires_at_utc = ts_utc + 30 días exactos`
- Este valor representa caducidad operativa del resultado exploratorio.
- No constituye certificación ni estatus constitucional.

---

## IV. Algoritmo y Estándar Criptográfico

Algoritmo:

- SHA-256

Salida:

- Representación hexadecimal en minúsculas (64 caracteres exactos)

Reglas:

- Prohibido utilizar algoritmos alternativos.
- Prohibido utilizar Base64 para la salida oficial.
- Solo representación hexadecimal en minúsculas es válida.

---

## V. Payload Canónico de Hash (HSC-PAYLOAD v1.0)

El hash se calcula sobre un único string canónico denominado `HSC_PAYLOAD_STRING`.

### V.1 Campos Incluidos (Orden Estricto e Inmutable)

1. `evaluation_id`
2. `mode`
3. `version_id`
4. `ts_utc`
5. `sci_internal`
6. `tier`
7. `state`
8. `expires_at_utc`
9. `D1`
10. `D2`
11. `D3`
12. `D4`
13. `D5`
14. `D6`
15. `D7`
16. `D8`

Reglas:

- El orden es inmutable.
- Prohibido agregar campos en v1.0.
- Prohibido eliminar campos en v1.0.
- Prohibido alterar mayúsculas/minúsculas.
- Prohibido normalizar después de construcción.

---

### V.2 Normalización de Formato por Campo

**evaluation_id**
- String exacto emitido por backend.
- Case-sensitive.

**mode**
- `OFFICIAL` o `EXPLORATORY` (uppercase exacto).
- Case-sensitive.

**version_id**
- Ejemplo: `1.0`
- String exacto.
- Case-sensitive.

**ts_utc**
- ISO 8601 UTC estricto con `Z`
- Sin milisegundos
- Sin zona horaria distinta
- Case-sensitive

**expires_at_utc**
- ISO 8601 UTC con `Z`
- Obligatorio en todos los modos
- No puede ser NULL
- Case-sensitive

**sci_internal**
- Siempre con exactamente dos (2) decimales
- Separador decimal: punto `.`
- Fixed-point obligatorio
- Prohibido notación científica
- Prohibido truncamiento posterior al formateo
- Prohibido usar `sci_public_trunc`
- El valor persistido es definitivo para hashing
- No se permite doble redondeo posterior

**tier**
- `I|II|III|IV|V` (uppercase romano exacto)
- Case-sensitive

**state**
- `ACTIVE|WARNING|INACTIVE|DOWNGRADED|PERMANENT`
- Uppercase exacto
- Case-sensitive

**D1–D8**
- Siempre con exactamente dos (2) decimales
- Separador decimal: punto `.`
- Fixed-point obligatorio
- Prohibido notación científica
- Prohibido normalización posterior

---

### V.3 Separador y Construcción

Separador oficial:

- Pipe `|`

Reglas de construcción:

- Sin espacios
- Sin saltos de línea
- Prohibido CRLF o cualquier carácter de salto de línea.
- Codificación UTF-8 sin BOM
- Prohibido usar JSON como payload en v1.0
- Prohibido agregar whitespace inicial o final
- Prohibido aplicar trim automático posterior

Construcción exacta:

HSC_PAYLOAD_STRING =
evaluation_id|mode|version_id|ts_utc|sci_internal|tier|state|expires_at_utc|D1|D2|D3|D4|D5|D6|D7|D8

El hash oficial se calcula como:

hash_sha256 = SHA256(utf8(HSC_PAYLOAD_STRING))

---

## VI. Procedimiento de Generación

1. Backend genera:
   - `evaluation_id`
   - `ts_utc`

2. Backend ejecuta IRA-MTR-001 y obtiene:
   - D1–D8 (2 decimales exactos)
   - SCI_int (2 decimales exactos)
   - Tier
   - State
   - expires_at_utc (según TTL o regla exploratoria)

3. Backend construye `HSC_PAYLOAD_STRING`.

4. Backend calcula:
   - `hash_sha256 = SHA256(utf8(HSC_PAYLOAD_STRING))`

5. Backend persiste registro completo.

6. Solo después se emite:
   - PDF institucional
   - Endpoint de verificación

---

## VII. Persistencia Obligatoria

Antes de emisión pública debe existir registro persistido con:

- evaluation_id
- ts_utc
- version_id
- mode
- sci_internal
- sci_public_trunc
- tier
- state
- expires_at_utc
- hash_sha256 (obligatorio en OFFICIAL)
- D1–D8 (internos exactos)

Reglas adicionales:

- Persistencia precede emisión pública.
- En evaluaciones `OFFICIAL`, `hash_sha256` debe ser UNIQUE en base de datos.
- No pueden existir dos evaluaciones `OFFICIAL` con el mismo hash.

---

## VIII. Verificación Pública (VERIFY)

Endpoints Permitidos:

- `/verify/{evaluation_id}`
- `/verify?hash=...`

VERIFY:

- No recalcula
- No ejecuta el motor
- No reconstruye el payload
- Solo consulta base de datos

Salida pública permitida:

- Tier
- State (según política)
- Timestamp UTC
- Version
- Vigencia
- SCI_pub
- SCI_int (si política OFFICIAL lo permite)

---

## IX. Inmutabilidad y Prohibiciones

Prohibido:

- Generar hash desde frontend
- Recalcular hash en VERIFY
- Alterar campos canónicos post-emisión
- Cambiar orden del payload
- Modificar precisión decimal
- Aplicar normalización automática
- Cambiar reglas sin nueva versión del documento

Si cambia cualquier campo del payload:

→ El hash cambia  
→ El registro pierde consistencia  

---

## X. Seguridad Mínima

Obligatorio:

- Hashing server-side
- Logs de generación
- Rate limiting en `/verify`
- No exponer payload completo públicamente
- No incluir PII en payload canónico

Recomendado:

- `created_ip_hash`
- `user_agent_hash`

(No forman parte del payload en v1.0)

---

## XI. Control de Versión

IRA-HSC-001 pertenece a IRA™ v1.0 Constitucional.

Estado actual: CANDIDATE.

Para pasar a LOCKED requiere:

- Validación cruzada con IRA-MTR-001
- Validación con modelo de base de datos
- Confirmación de implementación backend
- Registro institucional de cierre

No existe edición retroactiva.

---

## XII. Declaración Constitucional

IRA-HSC-001 queda declarado como el estándar oficial de Hash & Structural Control del sistema IRA™ v1.0.

Emitido por:

Julio César Moya  
Founder & Systems Architect  
SINTERGIA™

Fecha oficial de emisión: 15 de febrero de 2026  
Status: CANDIDATE  
Versión: 1.0