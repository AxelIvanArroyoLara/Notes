
> Rol: **Persona 5 — Embedded/Companion Software Engineer (Team Lead / Dossier Owner recomendado)**  
> Objetivo macro: **integrar todo el pipeline** (datos → detección → mitigación → autopiloto → logs → replay → evidencia/dossier) con reproducibilidad.e

---

## 1) Esenciales (antes de Round 2): fundamentos que debes dominar sí o sí

### 1.1 Conceptos base del sistema (visión end-to-end)
Debes investigar y entender con claridad:
- **Qué entra al sistema (inputs):**
  - **GNSS**: posición/velocidad/tiempo, calidad de fix, satélites, métricas de señal (si disponibles).
  - **IMU**: acelerómetros/giroscopios (y temperatura si existe), frame/unidades, rate.
- **Qué sale del sistema (outputs):**
  - **Estado** del detector (NORMAL/SUSPECTED/CONFIRMED/RECOVERY).
  - **Acción recomendada** (ej. hold, loiter, RTL, degrade sensor, limit speed) y/o comando específico.
- **Qué se debe registrar para trazabilidad:**
  - inputs raw, features/observables, flags, estado, acción recomendada/enviada, latencias, errores.

**Resultado esperado (artefacto):**
- Un documento corto (1–2 páginas) llamado **System Overview** con:
  - entrada → procesamiento → salida
  - lista de módulos
  - quién produce/consume cada señal

---

### 1.2 Timestamps, sincronización y determinismo (replay confiable)
Debes investigar exactamente:
- Tipos de timestamp y cómo usarlos:
  - `t_sensor` (timestamp del sensor GNSS/IMU)
  - `t_ingest` (cuando llega a tu software)
  - `t_proc` (tick/tiempo interno de procesamiento)
- Estrategias de sincronización GNSS vs IMU:
  - interpolación/hold-last
  - tolerancia a jitter
  - manejo de datos faltantes
- Determinismo en pipelines:
  - orden estable de eventos/mensajes
  - fixed-step loop vs event-driven
  - seeds (si hay simulación)
  - tolerancias numéricas (floats) en comparaciones

**Resultado esperado (artefacto):**
- Especificación **Timing & Determinism Rules v0** (lista de reglas claras).

---

### 1.3 Contrato de datos (Data Contract) y versionado
Debes investigar y definir:
- Campos mínimos obligatorios para GNSS e IMU:
  - GNSS: lat/lon/alt, vel, fix_type, sat_count, hdop/vdop (si existe), cn0_mean (si existe), timestamp
  - IMU: accel_xyz, gyro_xyz, frame, unidades, timestamp
- Campos de trazabilidad:
  - `sequence_id`, `source` (sim/real), `run_id`, `config_hash`, `commit_hash`
- Cómo versionar el contrato:
  - `schema_version` + changelog breve

**Resultado esperado (artefacto):**
- Archivo `docs/data_contract_v0.md` + ejemplo de payload/log.

---

### 1.4 Métricas y KPIs (cómo medir “va bien”)
Debes investigar y fijar fórmula exacta para:
- **Latencia de detección**: `t_detect - t_attack_start` (p50/p95).
- **Falsas alarmas**:
  - FA/min en nominal
  - FA/test en escenarios
- **TPR/FNR** por clase (jam/spoof).
- **Tiempo de recuperación**: `t_recovery - t_attack_end`.
- **Chattering/oscillación**: cambios de estado por minuto.

**Resultado esperado (artefacto):**
- `docs/kpi_definition_v0.md` (con fórmulas y ejemplos).

---

## 2) Investigación “Esenciales técnicos” para tu rol (Software Embedded/Companion)

### 2.1 Arquitectura software (módulos, colas, scheduler)
Debes investigar:
- Patrones de arquitectura aplicables:
  - pipeline por etapas (Ingest → Sync → Detect → Mitigate → Output)
  - pub/sub (topics) vs colas directas
  - ring buffers para IMU alta frecuencia
- Qué colas/topics necesitas y su contrato mínimo:
  - `gnss_raw`, `imu_raw`
  - `observables/features`
  - `detector_state`
  - `recommended_action` y/o `autopilot_command`
  - `logs/events`

**Resultado esperado:**
- Diagrama (Mermaid/PlantUML) + `docs/architecture_v0.md`.

---

### 2.2 Integración con autopiloto (PX4/ArduPilot)
Debes investigar exactamente (elige la ruta que aplique a tu prototipo):

#### Ruta A: Companion Computer vía **MAVLink**
- Qué mensajes usar para:
  - leer estados relevantes (GPS status, EKF status si aplica)
  - enviar setpoints/commands de mitigación
- Mecanismo de “control authority”:
  - cómo evitar pelearte con el autopiloto
  - reglas de seguridad (failsafe, rate limit de comandos)
- Qué librería usar (según stack):
  - MAVSDK, pymavlink, MAVLink C library (según lenguaje)

#### Ruta B: Integración interna en PX4 vía **uORB**
- Qué es uORB y cómo:
  - suscribirte a topics (GNSS/IMU/estados)
  - publicar comandos o estados
- Dónde vive tu módulo dentro del firmware y cómo se prueba (SITL/HITL)
- Reglas de timing dentro de PX4 (ciclos, prioridades)

**Resultado esperado:**
- Documento `docs/autopilot_adapter_v0.md` con:
  - tabla “Acción lógica → comando concreto”
  - lista de mensajes/topics usados
  - consideraciones de seguridad

---

### 2.3 Logging & Replay (tu columna vertebral del dossier)
Debes investigar:
- Formatos y cuándo convienen:
  - **CSV** (simple, para plots rápidos)
  - **ROS bag** (si ROS2 ya está en tu stack)
  - **ULog** (si PX4 logging es central)
  - formato binario propio + export (si quieres máximo determinismo)
- Qué debe incluir **sí o sí** un log reproducible:
  - `run_id`, `schema_version`, `commit_hash`, `config_hash`
  - inputs raw, outputs, eventos, latencias
  - metadata del entorno (sim/real, rates)
- Diseño de replay:
  - reinyectar inputs en el mismo orden
  - fixed tick / reproducción temporal
  - comparación con baseline (diff tolerante)

**Resultado esperado:**
- `tools/replay/` con `replay v0` funcional  
- `docs/logging_spec_v0.md` con el formato final elegido

---

### 2.4 Evidence Pack Generator (para dossier automático)
Debes investigar:
- Qué plots y tablas son “mínimo estándar” por test:
  - estado vs tiempo
  - observable principal vs tiempo (el que justifica detección)
  - acción/command vs tiempo
  - tabla de eventos (trigger, transición, acción, duración)
- Cómo estructurar evidencia por test:
  - `/evidence/tests/<TestID>/`
  - `summary.md`, `kpis.json`, `config.yaml`, `plots/*.png`, `log_link.txt`

**Resultado esperado:**
- `tools/evidence_pack/` con script 1-comando:
  - `generate_evidence_pack --test <TestID>`

---

### 2.5 CI/CD (GitHub Actions mínimo viable)
Debes investigar:
- Pipeline de CI recomendado:
  - build (core)
  - unit tests + replay smoke test
  - build dossier PDF (LaTeX o Markdown → PDF)
  - publicar artifacts (PDF + evidence packs)
- Qué tests deben correr en CI:
  - determinismo del replay sobre dataset pequeño
  - validación de schema/log (lint del contrato)
  - test de latencia (si aplica con límites razonables)

**Resultado esperado:**
- `.github/workflows/ci.yml` (compila + tests + build PDF)  
- Artifacts automáticos en cada push/tag.

---

## 3) Investigación específica Round 2 (según tu plan por semanas)

> Ventana Round 2: **Semana 1 a Semana 5** (04-abr → 08-may)

---

## Semana 1 (04-abr a 10-abr) — Simulación + dataset v0
### Tu misión (Persona 5): pipeline logging + formato estándar + replay v0

**Debes investigar exactamente:**
1) **Cómo unificar sim y real con el mismo “core log”**
   - estructura de carpetas por corrida (`run_id`)
   - metadata mínima obligatoria
2) **Qué formato estándar vas a congelar en v0**
   - define “primario” (core log) y “export” (csv/plots)
3) **Cómo medir KPIs desde logs**
   - script que lea `Test Catalogue` y produzca tabla KPI
4) **Replay determinista v0**
   - cómo reinyectar GNSS/IMU manteniendo orden y timing lógico

**Entregables que tú debes producir:**
- `logging_spec_v0.md` + `data_contract_v0.md`
- `replay v0` funcionando con dataset sim
- `kpi_report v0` (tabla latencias y falsas alarmas preliminar)

---

## Semana 2 (11-abr a 17-abr) — Instrumentación real (banco)
### Tu misión: integrar lecturas reales en el módulo (drivers/parsers)

**Debes investigar exactamente:**
1) **Drivers/parsers del hardware real**
   - protocolo (serial/USB/CAN), rate, mensajes disponibles
2) **Sincronización de clocks**
   - cómo estimar offset GNSS vs IMU
   - detección de drift/jitter
3) **Verificación de coherencia temporal**
   - checks automáticos: rate promedio, missing %, jitter histograma

**Entregables que tú debes producir:**
- módulo de ingestión real que emite el Data Contract v0
- log nominal 10–15 min con timestamps coherentes
- reporte automático de calidad de datos (sanity report)

---

## Semana 3 (18-abr a 24-abr) — Detección robusta + mitigación integrada
### Tu misión: estados + acciones autopiloto integradas

**Debes investigar exactamente:**
1) **Diseño FSM (NORMAL/SUSPECTED/CONFIRMED/RECOVERY)**
   - persistencia por ventanas
   - timers (cooldown/recovery)
   - condiciones de salida/entrada (sin oscillación)
2) **Mapeo de acciones a autopiloto**
   - qué comando exacto aplica a cada acción lógica
   - rate limits y seguridad (no saturar)
3) **Log de decisiones**
   - registrar “por qué” (flags/observables) para el dossier

**Entregables que tú debes producir:**
- FSM implementada + log de transiciones
- autopilot adapter con acciones mínimas (banco o SITL)
- tabla “Amenaza → Observable → Detector → Acción” lista para dossier (en conjunto)

---

## Semana 4 (25-abr a 01-may) — Validación controlada y evidencia
### Tu misión: Evidence Pack por test (repetible)

**Debes investigar exactamente:**
1) **Estructura estándar de evidencia por TestID**
2) **Plots obligatorios y tablas de eventos**
3) **Reproducibilidad**
   - `config_hash`, `commit_hash`, `run_manifest`
   - rerun idéntico → resultados consistentes

**Entregables que tú debes producir:**
- `generate_evidence_pack` (1 comando) por test
- carpeta `/evidence/tests/` ordenada y completa
- export de gráficas/tablas que alimentan el dossier

---

## Semana 5 (02-may a 08-may) — Cierre: dossier + demo
### Tu misión: narrativa final + CI/CD + coherencia

**Debes investigar exactamente:**
1) **Cómo asegurar trazabilidad completa**
   - cada afirmación del dossier apunta a un Evidence Pack
2) **CI/CD final**
   - build PDF + tests + artifacts
3) **Guion de demo**
   - escenario → detección → acción → recuperación
   - qué logs/plots mostrar y en qué orden

**Entregables finales que tú lideras:**
- Dossier v1.0 (PDF) + anexo de evidencia (carpetas)
- demo/video (estructura y assets)
- lista de riesgos, límites del prototipo y mitigaciones

---

## 4) Lista exacta de cosas que debes “investigar” (checklist)
### Autopiloto
- [ ] MAVLink: mensajes de telemetría y de comando para mitigación
- [ ] uORB PX4: topics de GNSS/IMU/estado y publicación de comandos (si aplica)
- [ ] Autoridad de control + failsafes + rate limits

### Arquitectura/Determinismo
- [ ] Diseño de colas/topics y backpressure
- [ ] fixed-step vs event-driven
- [ ] sincronización GNSS/IMU (offset, jitter, drift)
- [ ] reglas para replay determinista

### Logging/Replay/Evidencia
- [ ] formato principal de log + export
- [ ] schema versioning + metadata obligatoria
- [ ] replay tool (reinject + compare)
- [ ] evidence pack generator (plots/tablas/summary)

### CI/CD
- [ ] build + unit tests
- [ ] replay smoke test en dataset “golden”
- [ ] build PDF del dossier
- [ ] artifacts (PDF + evidence)

---

## 5) Artefactos obligatorios (para que Round 2 no se descontrole)
- **Decision Log**: qué/por qué/cuándo/quién
- **Risk Register**: probabilidad/impacto/mitigación/owner
- **Test Catalogue**:
  - `TestID`, setup, config_hash, expected, observed, link evidencia
- **Run Manifest** por corrida:
  - `run_id`, commit_hash, schema_version, config_hash, fecha, sim/real

---