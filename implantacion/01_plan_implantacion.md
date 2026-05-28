# 🗺️ Plan de Implantación del Programa

## 1. Visión General del Plan

El programa de transformación se estructura en **2 etapas principales**. La Etapa 2 se subdivide a su vez en **3 sub-etapas** que permiten una adopción progresiva y controlada, minimizando el riesgo y maximizando el aprendizaje antes de escalar.

```
LÍNEA DE TIEMPO DEL PROGRAMA
──────────────────────────────────────────────────────────────────────────────────────────
  ETAPA 1                    ETAPA 2 — IMPLANTACIÓN
  Definición y Exploración   ─────────────────────────────────────────────────────────
                             2.1 Configuración    2.2 Uso Controlado    2.3 Uso Masivo
  
  Mes 1-3                    Mes 3-4              Mes 4-6               Mes 6-12+
  ──────────────────         ─────────────────    ──────────────────    ──────────────
  • Arquitectura             • Instalación        • Uso diario          • Prompts/
  • MCPs necesarios          • Configuración        perfiles              Workflows
  • Memory Banks               Git, MCPs,           controlados           definidos
  • Skills.md                  Memory Banks       • Seguimiento         • Medición
  • Modelo operacional       • Gobierno             diario                continua
  • Métricas y KPIs            interno            • Definición          • Autonomía
  • Roles y responsab.                              Prompts y             total
  • IA Champions                                    Workflows
  
  [████████████████]         [████████]           [████████████]        [████████████]
──────────────────────────────────────────────────────────────────────────────────────────
```

---

## 2. Etapa 1: Definición y Exploración

### 2.1 Objetivo
Definir la arquitectura de referencia, identificar todos los componentes necesarios y preparar el modelo operacional antes de comenzar la implantación.

### 2.2 Duración Estimada
**2-3 meses**

### 2.3 Actividades — Dimensión Técnica

| # | Actividad | Estado | Responsable |
|---|-----------|--------|-------------|
| T1.1 | Definición de arquitectura de referencia | ✅ Completado | Arquitecto |
| T1.2 | Identificación de MCPs necesarios por tecnología | ✅ Completado | Arquitecto |
| T1.3 | Identificación de Memory Banks necesarios | ✅ Completado | Arquitecto |
| T1.4 | Identificación y creación de repositorios Git | 🔲 Pendiente | DevOps |
| T1.5 | Identificación de skills.md necesarios por tecnología | ✅ Completado | Tech Leads |
| T1.6 | Definición del modelo operacional | ✅ Completado | Arquitecto |
| T1.7 | Definición de métricas y KPIs | ✅ Completado | Arquitecto |
| T1.8 | Definición de riesgos | ✅ Completado | Arquitecto |
| T1.9 | Definición de estándares de calidad para código generado | 🔲 Pendiente | Tech Leads |
| T1.10 | Definición de roles y responsabilidades metodológicas | 🔲 Pendiente | Arquitecto + Tech Leads |

### 2.4 Actividades — Dimensión Gestión del Cambio

| # | Actividad | Estado | Responsable |
|---|-----------|--------|-------------|
| GC1.1 | Definición de IA Champions / stakeholders por BAP | 🔲 Pendiente | Sponsor + Tech Leads |
| GC1.2 | Definición del modelo de gobierno durante etapas de adopción | 🔲 Pendiente | Arquitecto + Change Manager |

### 2.5 Entregables de la Etapa 1

| Entregable | Estado |
|------------|--------|
| **Arquitectura de Referencia** (este repositorio) | ✅ Completado |
| **Catálogo de MCPs necesarios** | ✅ Completado |
| **Estructura de Memory Banks** | ✅ Completado |
| **Skills.md por tecnología** | ✅ Completado |
| **Modelo de Productividad y KPIs** | ✅ Completado |
| **Reglas Cline v1** (`.clinerules` por tecnología) | 🔲 Pendiente |
| **Libros Blancos v1** (uno por tecnología) | 🔲 Pendiente |
| **Repositorios Git configurados** | 🔲 Pendiente |
| **Estándares de calidad para código generado** | 🔲 Pendiente |
| **Roles y responsabilidades metodológicas** | 🔲 Pendiente |
| **IA Champions identificados por BAP** | 🔲 Pendiente |
| **Modelo de gobierno de adopción** | 🔲 Pendiente |

### 2.6 Criterios de Salida (Definition of Done)
- ✅ Arquitectura de referencia aprobada por el Sponsor
- ✅ MCPs necesarios identificados y priorizados
- 🔲 Repositorios Git configurados y accesibles
- 🔲 IA Champions comprometidos por cada BAP
- 🔲 Modelo de gobierno aprobado
- 🔲 Estándares de calidad definidos y aprobados

---

## 3. Etapa 2: Implantación

### 3.1 Objetivo
Implantar el ecosistema de forma progresiva en los equipos piloto (uno por tecnología), siguiendo las 3 sub-etapas de adopción hasta alcanzar la autonomía total.

### 3.2 Sub-etapa 2.1: Configuración

**Objetivo**: Dejar el entorno técnico completamente operativo para cada equipo piloto.

**Duración estimada**: 3-4 semanas por equipo (en paralelo para los 4 pilotos)

#### Actividades Técnicas

| # | Actividad | Responsable |
|---|-----------|-------------|
| T2.1.1 | Instalación y configuración de Cline en los equipos de los developers | DevOps + Tech Lead |
| T2.1.2 | Configuración de accesos a repositorios Git del proyecto | DevOps |
| T2.1.3 | Configuración de MCPs necesarios (Remedy, SAP/MSFT/Mule, Vector DB) | DevOps + Arquitecto |
| T2.1.4 | Configuración de Memory Banks iniciales del proyecto | Tech Lead + Arquitecto |
| T2.1.5 | Carga inicial de conocimiento en Vector DB (documentación existente) | DevOps + Tech Lead |
| T2.1.6 | Configuración de reglas Cline (`.clinerules`) por tecnología | Tech Lead |

#### Actividades de Gestión del Cambio

| # | Actividad | Responsable |
|---|-----------|-------------|
| GC2.1.1 | Definición del gobierno y flujo de trabajo interno del equipo | Tech Lead + Arquitecto |
| GC2.1.2 | Identificación de situaciones y riesgos específicos del equipo | IA Champion + Tech Lead |
| GC2.1.3 | Kick-off del piloto con el equipo | Arquitecto + Change Manager |

**Entregables**:
- Entorno Cline operativo en todos los puestos del equipo piloto
- MCPs configurados y validados
- Memory Banks iniciales creados
- Flujo de trabajo interno documentado

---

### 3.3 Sub-etapa 2.2: Uso Controlado

**Objetivo**: Adopción guiada del ecosistema por perfiles controlados dentro del equipo, con seguimiento intensivo y definición de los Prompts y Workflows de uso.

**Duración estimada**: 6-8 semanas

#### Actividades Técnicas

| # | Actividad | Responsable |
|---|-----------|-------------|
| T2.2.1 | Utilización diaria por perfiles controlados dentro del equipo | Developers (perfiles seleccionados) |
| T2.2.2 | Seguimiento diario de uso y resultados | Tech Lead + IA Champion |
| T2.2.3 | Definición de Prompts específicos para las tareas más frecuentes del equipo | Tech Lead + Developers |
| T2.2.4 | Definición de Workflows de uso específicos por tipo de tarea | Tech Lead + Arquitecto |
| T2.2.5 | Formación de utilización al equipo completo | IA Champion + Arquitecto |
| T2.2.6 | Definición de reglas y best practices de uso del Memory Bank | Tech Lead + Arquitecto |
| T2.2.7 | Aplicación de estándares de calidad al código generado | Tech Lead |
| T2.2.8 | Medición de productividades (primera medición vs. baseline) | Tech Lead + Arquitecto |

#### Actividades de Gestión del Cambio

| # | Actividad | Responsable |
|---|-----------|-------------|
| GC2.2.1 | Identificación de situaciones y riesgos durante el uso controlado | IA Champion + Tech Lead |
| GC2.2.2 | Evaluación de impacto en el marco de trabajo actual del equipo | Change Manager |
| GC2.2.3 | Seguimiento diario durante las primeras semanas | IA Champion |
| GC2.2.4 | Líder técnico + IA Champion validan que los perfiles controlados tienen el conocimiento necesario | Tech Lead + IA Champion |

**Entregables**:
- Catálogo de Prompts específicos del equipo/proyecto
- Catálogo de Workflows de uso por tipo de tarea
- Reglas y best practices de Memory Bank documentadas
- Primera medición de productividad vs. baseline
- Informe de impacto en el marco de trabajo

---

### 3.4 Sub-etapa 2.3: Uso Masivo

**Objetivo**: Extensión del uso al equipo completo con los Prompts y Workflows ya definidos y validados, alcanzando la autonomía total bajo el flujo de trabajo establecido.

**Duración estimada**: 4-6 semanas (por equipo), luego expansión al resto

#### Actividades Técnicas

| # | Actividad | Responsable |
|---|-----------|-------------|
| T2.3.1 | Utilización de Prompts/Workflows definidos y adaptados al proyecto por todo el equipo | Todos los developers |
| T2.3.2 | Medición continua de utilización y productividades | Tech Lead + Arquitecto |
| T2.3.3 | Autonomía total del equipo bajo el flujo de trabajo definido | Equipo |
| T2.3.4 | Actualización continua de Memory Banks y Vector DB | Todos los developers |
| T2.3.5 | Refinamiento de Prompts y Workflows basado en el uso real | Tech Lead + IA Champion |

#### Actividades de Gestión del Cambio

| # | Actividad | Responsable |
|---|-----------|-------------|
| GC2.3.1 | Establecimiento del proceso de OnBoarding para uso masivo (nuevos developers) | IA Champion + Tech Lead |
| GC2.3.2 | Líder técnico + IA Champions validan que todo el equipo tiene el conocimiento necesario | Tech Lead + IA Champion |
| GC2.3.3 | Seguimiento diario durante las primeras fechas de uso masivo | IA Champion |
| GC2.3.4 | Transición al modelo de soporte autónomo (comunidad de práctica) | Arquitecto + IA Champions |

**Entregables**:
- Equipo completo operativo con el ecosistema
- Proceso de OnBoarding documentado y validado
- Medición continua de productividad activa
- Equipo autónomo bajo el flujo de trabajo definido

---

## 4. IA Champions — Rol y Responsabilidades

### 4.1 ¿Qué es un IA Champion?
El **IA Champion** es el referente de adopción del ecosistema dentro de cada equipo/BAP. Es el puente entre el equipo técnico y el programa de transformación.

### 4.2 Perfil del IA Champion

| Atributo | Descripción |
|----------|-------------|
| **Perfil técnico** | Developer senior o Tech Lead con interés en IA |
| **Motivación** | Convencido del valor del ecosistema, dispuesto a ser embajador |
| **Dedicación** | 20-30% de su tiempo durante las fases de adopción |
| **Alcance** | Un IA Champion por equipo/BAP |

### 4.3 Responsabilidades del IA Champion

**Durante la Etapa 1:**
- Participar en la definición del modelo de gobierno
- Identificar los casos de uso más relevantes para su equipo

**Durante la Sub-etapa 2.1 (Configuración):**
- Apoyar la configuración técnica del entorno
- Identificar riesgos específicos del equipo

**Durante la Sub-etapa 2.2 (Uso Controlado):**
- Ser el primer usuario del ecosistema en el equipo
- Documentar Prompts y Workflows efectivos
- Dar soporte diario al equipo
- Reportar al Arquitecto los bloqueos y ajustes necesarios

**Durante la Sub-etapa 2.3 (Uso Masivo):**
- Formar al resto del equipo
- Gestionar el OnBoarding de nuevos developers
- Mantener y evolucionar los Prompts y Workflows
- Participar en la comunidad de práctica

### 4.4 IA Champions por BAP

| BAP / Tecnología | IA Champion | Estado |
|-----------------|-------------|--------|
| **SAP** | [Por definir] | 🔲 Pendiente |
| **Microsoft** | [Por definir] | 🔲 Pendiente |
| **MuleSoft** | [Por definir] | 🔲 Pendiente |
| **Darwin (React+PHP)** | [Por definir] | 🔲 Pendiente |

---

## 5. Catálogo de Prompts y Workflows

### 5.1 ¿Qué son los Prompts y Workflows de uso?

- **Prompts**: Instrucciones optimizadas para las tareas más frecuentes del equipo. Ejemplo: "Prompt para analizar una incidencia SAP", "Prompt para generar una spec funcional".
- **Workflows**: Secuencias de pasos definidas para tipos de tarea recurrentes. Ejemplo: "Workflow para resolver un bug", "Workflow para desarrollar un nuevo endpoint".

### 5.2 Proceso de Definición (Sub-etapa 2.2)

```
PROCESO DE DEFINICIÓN DE PROMPTS Y WORKFLOWS
────────────────────────────────────────────────────────────
1. IDENTIFICAR las tareas más frecuentes del equipo
   (análisis de tickets Remedy de los últimos 3 meses)

2. EXPERIMENTAR con diferentes prompts para cada tarea
   (IA Champion + 1-2 developers durante uso controlado)

3. VALIDAR la efectividad de cada prompt/workflow
   (medir calidad del output y tiempo empleado)

4. DOCUMENTAR en el repositorio del equipo
   (carpeta prompts/ y workflows/ en el proyecto)

5. COMPARTIR con el equipo en la fase de uso masivo
   (formación + documentación accesible)

6. REFINAR continuamente basándose en el uso real
────────────────────────────────────────────────────────────
```

### 5.3 Estructura de un Prompt Documentado

```markdown
# Prompt: [Nombre descriptivo]

## Contexto de uso
[Cuándo usar este prompt, para qué tipo de tarea]

## Prompt
[Texto del prompt, con variables entre corchetes]

## Ejemplo de uso
[Ejemplo concreto con input y output esperado]

## Notas
[Limitaciones, variantes, consejos de uso]
```

---

## 6. Modelo de Gobierno durante la Adopción

### 6.1 Estructura de Gobierno

```
MODELO DE GOBIERNO — ADOPCIÓN
────────────────────────────────────────────────────────────
  NIVEL ESTRATÉGICO (Sponsor)
  └─ Decisiones de inversión, priorización, escalado

  NIVEL PROGRAMA (Arquitecto + Change Manager)
  └─ Coordinación entre equipos, ajustes de arquitectura,
     resolución de bloqueos cross-equipo

  NIVEL EQUIPO (Tech Lead + IA Champion)
  └─ Adopción diaria, Prompts/Workflows, formación,
     medición de productividad del equipo

  NIVEL DEVELOPER (Todos)
  └─ Uso del ecosistema, feedback, actualización de
     Memory Banks
────────────────────────────────────────────────────────────
```

### 6.2 Proceso de Escalado de Problemas

| Tipo de Problema | Responsable de Resolución | Tiempo Máximo |
|-----------------|--------------------------|---------------|
| Técnico (configuración/uso) | IA Champion | 24h |
| Técnico (arquitectura/MCP) | Arquitecto | 48h |
| Proceso (flujo de trabajo) | Tech Lead + Arquitecto | 24h |
| Adopción (resistencia) | Change Manager + IA Champion | 1 semana |
| Estratégico | Sponsor | 1 semana |

---

## 7. Métricas del Programa

### 7.1 KPIs de Adopción

| KPI | Descripción | Objetivo Sub-etapa 2.2 | Objetivo Sub-etapa 2.3 |
|-----|-------------|----------------------|----------------------|
| **Adoption Rate** | % de developers usando Cline activamente | > 50% (perfiles controlados) | > 90% (todo el equipo) |
| **Spec Coverage** | % de features con spec antes de codificar | > 50% | > 90% |
| **Daily Active Usage** | Horas/día de uso de Cline por developer | > 1h | > 3h |
| **MCP Usage** | % de tareas que usan al menos 1 MCP server | > 30% | > 70% |
| **Prompts Defined** | Nº de Prompts documentados y validados | > 5 | > 15 |
| **Workflows Defined** | Nº de Workflows documentados y validados | > 3 | > 8 |

### 7.2 KPIs de Impacto

Ver documento completo: [Modelo de Productividad](../roadmap/01_modelo_productividad.md)

---

## 8. Riesgos del Programa

| # | Riesgo | Probabilidad | Impacto | Mitigación |
|---|--------|-------------|---------|------------|
| R1 | Resistencia al cambio de los equipos | Media | Alto | IA Champions activos, change management, mostrar valor rápido |
| R2 | Complejidad de integración con sistemas legacy | Alta | Alto | Prototipado temprano de MCPs críticos en Etapa 1 |
| R3 | Calidad insuficiente de los Memory Banks | Media | Alto | Formación específica, best practices documentadas en 2.2 |
| R4 | Prompts y Workflows de baja calidad | Media | Medio | Proceso de validación en 2.2 antes de escalar en 2.3 |
| R5 | IA Champions sin tiempo suficiente | Alta | Alto | Acuerdo explícito de dedicación (20-30%) con los managers |
| R6 | Curva de aprendizaje más larga de lo esperado | Media | Medio | Soporte intensivo en 2.1 y 2.2, ajuste del plan |
| R7 | Falta de tiempo de los equipos para el piloto | Alta | Alto | Acuerdo explícito de capacidad con los managers |