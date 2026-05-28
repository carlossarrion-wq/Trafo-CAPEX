# 📊 Modelo de Medición y Control de Productividad

## 1. Introducción

La adopción de un modelo de desarrollo basado en agentes IA introduce una **nueva dimensión en la medición de la productividad**. Los indicadores tradicionales (líneas de código, story points por sprint) son insuficientes para capturar el valor real que aporta el ecosistema. Se necesita un modelo de medición que responda a tres preguntas clave:

1. **¿Cuánto más rápido** trabajan los equipos con el ecosistema?
2. **¿Con qué calidad** se producen los artefactos (specs, código, tests)?
3. **¿Cuál es el ROI real** de la inversión en el programa?

> El objetivo no es medir a las personas, sino medir el **impacto del ecosistema** para mejorarlo continuamente.

---

## 2. Marco de Medición: Las 4 Dimensiones

```
┌─────────────────────────────────────────────────────────────────────┐
│              MODELO DE PRODUCTIVIDAD — 4 DIMENSIONES                │
├──────────────────┬──────────────────┬──────────────┬────────────────┤
│   VELOCIDAD      │    CALIDAD       │  ADOPCIÓN    │     ROI        │
│                  │                  │              │                │
│ ¿Cuánto más      │ ¿Mejor o peor    │ ¿Están       │ ¿Vale la pena  │
│ rápido?          │ que antes?       │ usando el    │ la inversión?  │
│                  │                  │ ecosistema?  │                │
│ Lead Time        │ Defect Rate      │ Usage Rate   │ Coste/Feature  │
│ Cycle Time       │ Rework Rate      │ Spec Coverage│ Time-to-Value  │
│ Throughput       │ Test Coverage    │ MCP Usage    │ Ahorro horas   │
└──────────────────┴──────────────────┴──────────────┴────────────────┘
```

---

## 3. Dimensión 1: Velocidad de Entrega

### 3.1 KPIs de Velocidad

| KPI | Definición | Cómo medirlo | Frecuencia |
|-----|-----------|--------------|------------|
| **Lead Time** | Tiempo desde que se abre un ticket hasta que está en producción | Remedy (fecha apertura) → Git (fecha merge) → Deploy | Por ticket |
| **Cycle Time** | Tiempo desde que un developer empieza a trabajar en una tarea hasta que termina | Git (primer commit) → merge | Por tarea |
| **Throughput** | Número de features/tickets completados por sprint | Remedy + Git | Por sprint |
| **Spec-to-Code Time** | Tiempo desde spec aprobada hasta código listo para review | Fecha aprobación spec → PR abierto | Por feature |
| **Time-to-First-Commit** | Tiempo desde asignación de tarea hasta primer commit | Remedy → Git | Por tarea |
| **PR Review Time** | Tiempo medio de revisión de pull requests | Git/Azure DevOps | Por PR |

### 3.2 Cómo Establecer el Baseline

Antes de implantar el ecosistema, medir durante **4-6 semanas** los mismos KPIs en el equipo piloto. Esto da el punto de referencia contra el que comparar.

```
PROCESO DE BASELINE
────────────────────────────────────────────────────────────
Semana -6 a -1 (antes del piloto):
  1. Exportar histórico de Remedy (últimos 3 meses)
  2. Exportar histórico de Git/Azure DevOps (últimos 3 meses)
  3. Calcular medias y percentiles (P50, P75, P90) de cada KPI
  4. Documentar en el Memory Bank del equipo piloto
  5. Acordar con el equipo que estos son los valores de referencia
────────────────────────────────────────────────────────────
```

### 3.3 Objetivos de Mejora por Fase

| KPI | Baseline | Objetivo Piloto (3m) | Objetivo Expansión (12m) |
|-----|---------|---------------------|------------------------|
| Lead Time | X días | -20% | -35% |
| Cycle Time | X días | -25% | -40% |
| Throughput | X features/sprint | +20% | +35% |
| Spec-to-Code Time | X horas | -30% | -50% |
| Time-to-First-Commit | X horas | -40% | -60% |

---

## 4. Dimensión 2: Calidad del Software

### 4.1 KPIs de Calidad

| KPI | Definición | Cómo medirlo | Frecuencia |
|-----|-----------|--------------|------------|
| **Defect Escape Rate** | % de defectos que llegan a producción sin ser detectados antes | Incidencias producción / Total features entregados | Por sprint |
| **Defect Density** | Número de defectos por feature o por KLOC | Remedy (bugs) / features entregados | Por sprint |
| **Rework Rate** | % de código que requiere reescritura significativa tras el primer review | PRs con > 20 comentarios de cambio / total PRs | Por sprint |
| **Test Coverage** | % de código cubierto por tests automatizados | SonarQube / herramientas de cobertura por tecnología | Por release |
| **Spec Completeness Score** | Puntuación de completitud de las specs (criterios de aceptación, casos edge, etc.) | Revisión del Agente de Revisión | Por spec |
| **First-Time-Right Rate** | % de features que pasan el review sin cambios significativos | PRs aprobados sin cambios / total PRs | Por sprint |
| **Mean Time to Resolve (MTTR)** | Tiempo medio en resolver una incidencia de producción | Remedy (fecha apertura → cierre) | Por incidencia |

### 4.2 Calidad Específica del Ecosistema IA

Además de los KPIs tradicionales, medir la calidad de los artefactos generados por los agentes:

| KPI | Definición | Cómo medirlo |
|-----|-----------|--------------|
| **Spec Acceptance Rate** | % de specs generadas por agentes que el developer aprueba sin modificaciones mayores | Registro en el flujo SDD |
| **Code Acceptance Rate** | % de código generado por Cline que el developer aprueba sin cambios significativos | Revisión de PRs (ratio cambios/líneas generadas) |
| **Hallucination Rate** | % de referencias a código/APIs/tablas inexistentes en el output de Cline | Revisión manual de PRs |
| **Context Accuracy** | % de veces que Cline usa correctamente el contexto del Memory Bank | Revisión cualitativa por el Tech Lead |

---

## 5. Dimensión 3: Adopción del Ecosistema

### 5.1 KPIs de Adopción

| KPI | Definición | Cómo medirlo | Frecuencia |
|-----|-----------|--------------|------------|
| **Daily Active Users (DAU)** | Número de developers que usan Cline activamente cada día | Telemetría de Cline / VS Code | Diaria |
| **Spec Coverage** | % de features que tienen spec formal antes de codificar | Registro en el flujo SDD | Por sprint |
| **Memory Bank Update Rate** | % de sesiones en las que se actualiza el Memory Bank | Commits en carpeta memory-bank/ | Por semana |
| **MCP Usage Rate** | % de tareas en las que se usa al menos 1 MCP server | Logs de MCP servers | Por semana |
| **SDD Compliance Rate** | % de features que siguen el flujo SDD completo | Auditoría del proceso | Por sprint |
| **Knowledge Reuse Rate** | % de specs que reutilizan patrones del Vector DB | Registro en el flujo SDD | Por sprint |

### 5.2 Mapa de Adopción por Developer

Para cada developer del equipo, trazar su curva de adopción:

```
CURVA DE ADOPCIÓN INDIVIDUAL
────────────────────────────────────────────────────────────
  NIVEL 1: EXPLORADOR (Semanas 1-2)
  └─ Usa Cline para tareas simples (entender código, buscar info)
  
  NIVEL 2: PRACTICANTE (Semanas 3-6)
  └─ Usa Cline para desarrollo guiado, con supervisión constante
  
  NIVEL 3: COMPETENTE (Semanas 7-10)
  └─ Usa el flujo SDD completo, usa MCP servers activamente
  
  NIVEL 4: EXPERTO (Semanas 11+)
  └─ Autónomo, contribuye a mejorar reglas y Memory Banks
  
  NIVEL 5: CHAMPION (Post-piloto)
  └─ Forma a otros, propone mejoras al ecosistema
────────────────────────────────────────────────────────────
```

### 5.3 NPS del Ecosistema

Encuesta trimestral a los developers con una única pregunta:

> *"En una escala del 0 al 10, ¿recomendarías el uso de este ecosistema de desarrollo a un compañero?"*

| Puntuación | Clasificación |
|-----------|---------------|
| 9-10 | Promotor |
| 7-8 | Pasivo |
| 0-6 | Detractor |

**NPS = % Promotores - % Detractores**

Objetivo: NPS > 40 al final del piloto, > 60 tras la expansión.

---

## 6. Dimensión 4: ROI del Programa

### 6.1 Modelo de Cálculo del ROI

```
ROI = (Beneficios obtenidos - Costes del programa) / Costes del programa × 100
```

#### Costes del Programa

| Categoría | Componentes |
|-----------|-------------|
| **Licencias y herramientas** | Cline (Claude API), Aurora RDS, Graph DB, MCP servers |
| **Desarrollo de componentes** | Horas de desarrollo de MCP servers, reglas, libros blancos |
| **Formación** | Horas de formación × coste/hora de los developers |
| **Soporte durante pilotos** | Horas del Arquitecto y Change Manager |
| **Infraestructura** | AWS (Aurora, compute para MCP servers) |

#### Beneficios Cuantificables

| Beneficio | Cómo cuantificar |
|-----------|-----------------|
| **Ahorro en tiempo de desarrollo** | (Horas ahorradas por feature) × (coste/hora) × (nº features/año) |
| **Reducción de defectos** | (Defectos evitados) × (coste medio de resolución de un defecto) |
| **Reducción de rework** | (Horas de rework evitadas) × (coste/hora) |
| **Aceleración del onboarding** | (Días ahorrados en onboarding) × (coste/día) × (nº nuevos developers/año) |
| **Reducción de tiempo en búsqueda de información** | (Horas/semana ahorradas) × (coste/hora) × (nº developers) × 52 |

### 6.2 Plantilla de Cálculo ROI

```
EJEMPLO DE CÁLCULO (equipo de 10 developers, 1 año)
────────────────────────────────────────────────────────────
COSTES ANUALES:
  Licencias Claude API:          ~12.000 €/año
  Aurora RDS + infraestructura:   ~6.000 €/año
  Desarrollo MCP servers (1 vez): ~40.000 € (amortizado 3 años = 13.333 €/año)
  Formación (1 vez):              ~15.000 € (amortizado 3 años = 5.000 €/año)
  ─────────────────────────────────────────────────────────
  TOTAL COSTES:                  ~36.333 €/año

BENEFICIOS ANUALES (estimados con mejoras conservadoras):
  Ahorro tiempo desarrollo (20% mejora, 10 devs, 1.600h/año, 60€/h):
    10 × 1.600 × 0.20 × 60 = 192.000 €/año
  Reducción defectos (30% menos, 50 defectos/año, 2.000€/defecto):
    50 × 0.30 × 2.000 = 30.000 €/año
  Reducción rework (40% menos, 200h/año, 60€/h):
    200 × 0.40 × 60 = 4.800 €/año
  ─────────────────────────────────────────────────────────
  TOTAL BENEFICIOS:             ~226.800 €/año

ROI = (226.800 - 36.333) / 36.333 × 100 = 524%
────────────────────────────────────────────────────────────
```

> ⚠️ Este es un ejemplo ilustrativo. Los valores reales se calcularán con el baseline de cada equipo piloto.

---

## 7. Sistema de Reporting

### 7.1 Dashboard de Productividad

Se propone un dashboard con 3 niveles de visibilidad:

#### Nivel 1: Dashboard Operativo (para Tech Leads — semanal)

```
┌─────────────────────────────────────────────────────────────┐
│              DASHBOARD SEMANAL — EQUIPO [X]                  │
├──────────────────┬──────────────────┬───────────────────────┤
│  VELOCIDAD       │  CALIDAD         │  ADOPCIÓN             │
│                  │                  │                       │
│  Lead Time: Xd   │  Defects: X      │  DAU: X/Y devs        │
│  Throughput: X   │  Rework: X%      │  Spec Coverage: X%    │
│  vs baseline: ↑↓ │  Coverage: X%    │  MCP Usage: X%        │
└──────────────────┴──────────────────┴───────────────────────┘
```

#### Nivel 2: Dashboard de Programa (para Arquitecto — mensual)

- Comparativa entre los 4 equipos piloto
- Evolución de KPIs desde el inicio del piloto
- Alertas de equipos con adopción baja
- Estado de los componentes del ecosistema

#### Nivel 3: Dashboard Ejecutivo (para Sponsor — trimestral)

- ROI acumulado del programa
- Comparativa antes/después por tecnología
- Proyección de beneficios al escalar
- Riesgos y plan de mitigación

### 7.2 Fuentes de Datos para el Dashboard

| Fuente | Datos que aporta | Integración |
|--------|-----------------|-------------|
| **BMC Remedy** | Lead Time, MTTR, Defect Rate | API Remedy → Dashboard |
| **Git / Azure DevOps** | Cycle Time, Throughput, PR metrics | API Git → Dashboard |
| **Cline Telemetría** | DAU, sesiones, herramientas usadas | Logs Cline → Dashboard |
| **MCP Server Logs** | MCP Usage Rate, herramientas más usadas | Logs MCP → Dashboard |
| **SonarQube / ATC** | Test Coverage, Code Quality | API SonarQube → Dashboard |
| **Encuestas** | NPS, satisfacción cualitativa | Forms → Dashboard |

---

## 8. Proceso de Revisión y Mejora Continua

### 8.1 Cadencia de Revisión

| Cadencia | Reunión | Participantes | Agenda |
|----------|---------|---------------|--------|
| **Semanal** | Stand-up de adopción (30 min) | Tech Lead + Arquitecto | KPIs de la semana, bloqueos, ajustes rápidos |
| **Quincenal** | Revisión de productividad (1h) | Tech Lead + equipo | Análisis de tendencias, feedback del equipo |
| **Mensual** | Revisión de programa (2h) | Arquitecto + Tech Leads | Comparativa entre equipos, ajustes al ecosistema |
| **Trimestral** | Revisión ejecutiva (1h) | Sponsor + Arquitecto | ROI, decisiones estratégicas, plan de expansión |

### 8.2 Proceso de Ajuste Basado en Datos

```
CICLO DE MEJORA CONTINUA
────────────────────────────────────────────────────────────
  1. MEDIR
     └─ Recopilar KPIs según la cadencia definida

  2. ANALIZAR
     └─ Identificar tendencias, anomalías y oportunidades

  3. DIAGNOSTICAR
     └─ Entender la causa raíz de los problemas detectados
        ¿Es un problema de adopción? ¿De calidad del ecosistema?
        ¿De formación? ¿De proceso?

  4. ACTUAR
     └─ Ajustar el componente correspondiente:
        • Adopción baja → más formación, soporte intensivo
        • Calidad baja de specs → mejorar agentes OpenSpec
        • Código con muchos errores → ajustar reglas Cline
        • MCP poco usado → mejorar UX del MCP server

  5. VALIDAR
     └─ Verificar que el ajuste tuvo el efecto esperado
────────────────────────────────────────────────────────────
```

---

## 9. Consideraciones Éticas y de Gestión del Cambio

### 9.1 Principios de Medición

> ⚠️ **Importante**: Las métricas de productividad deben usarse para **mejorar el ecosistema**, no para evaluar o comparar a los desarrolladores individualmente.

| Principio | Descripción |
|-----------|-------------|
| **Transparencia** | Los developers conocen qué se mide y por qué |
| **Agregación** | Los datos se reportan a nivel de equipo, no individual |
| **Mejora, no control** | El objetivo es identificar dónde el ecosistema falla, no quién falla |
| **Participación** | Los developers contribuyen a definir y revisar las métricas |
| **Contexto** | Los KPIs siempre se interpretan con contexto (complejidad del proyecto, etc.) |

### 9.2 Comunicación al Equipo

Al inicio del piloto, comunicar claramente:
- **Qué** se va a medir y **por qué**
- **Cómo** se van a usar los datos (mejora del ecosistema, no evaluación personal)
- **Quién** tiene acceso a los datos
- **Cómo** pueden los developers dar feedback sobre las métricas

---

## 10. Checklist de Implementación del Modelo de Productividad

### Antes del Piloto
- [ ] Extraer baseline de los últimos 3 meses (Remedy + Git)
- [ ] Calcular y documentar valores de referencia por KPI
- [ ] Configurar las fuentes de datos para el dashboard
- [ ] Comunicar el modelo de medición al equipo
- [ ] Acordar los objetivos de mejora con el Tech Lead

### Durante el Piloto
- [ ] Revisar KPIs semanalmente en el stand-up de adopción
- [ ] Registrar incidencias y ajustes en el diario del piloto
- [ ] Realizar encuesta NPS al final del mes 1 y mes 3
- [ ] Documentar casos de éxito y fracaso con datos

### Al Finalizar el Piloto
- [ ] Calcular el ROI real del piloto
- [ ] Comparar KPIs finales vs baseline
- [ ] Presentar resultados al Sponsor con recomendaciones
- [ ] Actualizar el modelo de medición para la fase de expansión