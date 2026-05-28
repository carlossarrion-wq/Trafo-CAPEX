# 📋 Spec Driven Development (SDD) con OpenSpec

## 1. ¿Qué es Spec Driven Development?

**Spec Driven Development (SDD)** es una metodología de desarrollo de software en la que **toda implementación está precedida y guiada por una especificación formal**. A diferencia del desarrollo tradicional donde el código se escribe directamente a partir de requisitos informales, en SDD:

1. La especificación es el **artefacto primario** del desarrollo
2. El código es una **consecuencia** de la spec, no al revés
3. La spec es **validada y aprobada** antes de que comience la codificación
4. Los agentes IA generan tanto la spec como el código, con supervisión humana

### 1.1 Beneficios del SDD

| Beneficio | Descripción |
|-----------|-------------|
| **Alineación** | Negocio y tecnología acuerdan qué se va a construir antes de construirlo |
| **Calidad** | Los errores se detectan en la spec, no en producción |
| **Velocidad** | Cline genera código más preciso con una spec clara |
| **Trazabilidad** | Cada línea de código tiene su origen en una spec |
| **Reutilización** | Las specs se convierten en conocimiento reutilizable |
| **Estimación** | Las specs permiten estimaciones más precisas |

---

## 2. OpenSpec — El Estándar de Especificación

**OpenSpec** es el framework de especificación utilizado en este ecosistema. Define una estructura estándar para los diferentes tipos de especificaciones que se generan durante el ciclo de vida del desarrollo.

### 2.1 Tipos de Especificaciones OpenSpec

```
OPENSPEC — TIPOS DE ESPECIFICACIÓN
│
├── 📄 FUNCTIONAL SPEC
│   ├── Descripción del problema / necesidad de negocio
│   ├── Historias de usuario (User Stories)
│   ├── Criterios de aceptación (Gherkin / BDD)
│   ├── Flujos de negocio (Happy path + alternativas)
│   ├── Reglas de negocio
│   └── Restricciones y supuestos
│
├── 🏗️ TECHNICAL SPEC
│   ├── Diseño de la solución técnica
│   ├── Componentes y responsabilidades
│   ├── Interfaces entre componentes
│   ├── Modelo de datos
│   ├── Decisiones de arquitectura
│   └── Consideraciones de seguridad y rendimiento
│
├── 🔌 API SPEC
│   ├── Definición OpenAPI / RAML
│   ├── Endpoints y operaciones
│   ├── Modelos de request/response
│   ├── Códigos de error
│   ├── Autenticación y autorización
│   └── Ejemplos de uso
│
└── 🧪 TEST SPEC
    ├── Estrategia de testing
    ├── Casos de prueba unitarios
    ├── Casos de prueba de integración
    ├── Escenarios de aceptación (E2E)
    └── Criterios de cobertura
```

### 2.2 Estructura de una Spec OpenSpec

Cada spec sigue una estructura estándar en Markdown:

```markdown
# [TIPO] Spec: [Nombre del Feature/Componente]

## Metadata
- **ID**: SPEC-[número]
- **Tipo**: Functional | Technical | API | Test
- **Versión**: 1.0
- **Estado**: Draft | In Review | Approved | Implemented
- **Autor**: [Agente/Developer]
- **Fecha**: [fecha]
- **Ticket Origen**: [ID Remedy]
- **Proyecto**: [nombre del proyecto]

## 1. Contexto
[Descripción del contexto y motivación]

## 2. Alcance
[Qué incluye y qué no incluye esta spec]

## 3. [Contenido específico según tipo]
[Historias de usuario / Diseño técnico / API definition / Test cases]

## 4. Criterios de Aceptación
[Lista de criterios verificables]

## 5. Dependencias
[Otras specs, sistemas, componentes de los que depende]

## 6. Riesgos y Supuestos
[Riesgos identificados y supuestos realizados]

## 7. Historial de Revisiones
| Versión | Fecha | Autor | Cambios |
|---------|-------|-------|---------|
| 1.0 | [fecha] | [autor] | Versión inicial |
```

---

## 3. El Flujo SDD Completo

```
┌─────────────────────────────────────────────────────────────────────────┐
│                        FLUJO SPEC DRIVEN DEVELOPMENT                     │
└─────────────────────────────────────────────────────────────────────────┘

  ENTRADA: Necesidad de negocio / Ticket Remedy / Historia de usuario
     │
     ▼
┌────────────────────────────────────────────────────────────────────────┐
│  FASE 1: CONCEPTUALIZACIÓN                                              │
│                                                                        │
│  Agente: Agente de Conceptualización                                   │
│  Input:  Descripción informal de la necesidad                          │
│  Output: Concept Brief estructurado                                    │
│                                                                        │
│  • Clarifica el problema                                               │
│  • Define el alcance inicial                                           │
│  • Identifica restricciones y dependencias                             │
│  • Propone enfoque de solución                                         │
│  • Consulta Memory Banks y Vector DB para contexto                     │
└────────────────────────────────────────────────────────────────────────┘
     │
     ▼ [Developer revisa y aprueba el Concept Brief]
     │
┌────────────────────────────────────────────────────────────────────────┐
│  FASE 2: ESPECIFICACIÓN                                                 │
│                                                                        │
│  Agentes: Suite OpenSpec                                               │
│  Input:   Concept Brief aprobado                                       │
│  Output:  Functional Spec + Technical Spec + API Spec (si aplica)     │
│                                                                        │
│  • Agente Functional Spec: genera historias de usuario y criterios    │
│  • Agente Technical Spec: diseña la solución técnica                  │
│  • Agente API Spec: define contratos de API (si aplica)               │
│  • Todos consultan Memory Banks + Vector DB para consistencia         │
└────────────────────────────────────────────────────────────────────────┘
     │
     ▼ [Developer revisa las specs]
     │
┌────────────────────────────────────────────────────────────────────────┐
│  FASE 3: ESTIMACIÓN                                                     │
│                                                                        │
│  Agente: Agente de Estimación                                          │
│  Input:  Specs completas                                               │
│  Output: Estimación detallada con rangos de confianza                 │
│                                                                        │
│  • Descompone la spec en tareas estimables                            │
│  • Aplica datos históricos del proyecto (Memory Banks)                │
│  • Identifica riesgos que afectan a la estimación                     │
│  • Genera estimación por componente y total                           │
└────────────────────────────────────────────────────────────────────────┘
     │
     ▼
┌────────────────────────────────────────────────────────────────────────┐
│  FASE 4: REVISIÓN / CHALLENGE                                           │
│                                                                        │
│  Agente: Agente de Revisión                                            │
│  Input:  Specs + Estimación                                            │
│  Output: Informe de revisión con observaciones y preguntas            │
│                                                                        │
│  • Verifica completitud y consistencia de las specs                   │
│  • Cuestiona supuestos y decisiones técnicas                          │
│  • Valida la estimación contra la complejidad                         │
│  • Identifica riesgos no contemplados                                 │
│  • Sugiere mejoras y alternativas                                     │
└────────────────────────────────────────────────────────────────────────┘
     │
     ▼ [Developer resuelve observaciones y aprueba specs]
     │
┌────────────────────────────────────────────────────────────────────────┐
│  FASE 5: CODIFICACIÓN                                                   │
│                                                                        │
│  Agente: CLINE                                                         │
│  Input:  Specs aprobadas + Memory Banks + Vector DB + Skills + Reglas │
│  Output: Código implementado                                           │
│                                                                        │
│  • Lee y comprende las specs aprobadas                                │
│  • Consulta Memory Banks para contexto del proyecto                   │
│  • Consulta Vector DB para patrones y código existente                │
│  • Consulta Graph DB para entender dependencias                       │
│  • Usa MCP servers para acceder a sistemas externos                   │
│  • Aplica Skills de tecnología y Reglas Cline                         │
│  • Genera código, tests y documentación                               │
└────────────────────────────────────────────────────────────────────────┘
     │
     ▼ [Developer revisa el código]
     │
┌────────────────────────────────────────────────────────────────────────┐
│  FASE 6: VALIDACIÓN                                                     │
│                                                                        │
│  Agente: Agente de Testing                                             │
│  Input:  Test Spec + Código implementado                               │
│  Output: Reporte de testing + Cobertura                               │
│                                                                        │
│  • Genera casos de prueba basados en la Test Spec                     │
│  • Ejecuta tests y verifica cobertura                                 │
│  • Valida que el código cumple los criterios de aceptación            │
│  • Genera reporte de resultados                                       │
└────────────────────────────────────────────────────────────────────────┘
     │
     ▼ [Developer aprueba y hace merge]
     │
┌────────────────────────────────────────────────────────────────────────┐
│  CIERRE: ACTUALIZACIÓN DEL CONOCIMIENTO                                 │
│                                                                        │
│  • Memory Banks se actualiza con nuevas decisiones y patrones         │
│  • Vector DB indexa el nuevo código y specs                           │
│  • Graph DB actualiza las relaciones del nuevo componente             │
│  • Ticket Remedy se cierra con worklog                                │
└────────────────────────────────────────────────────────────────────────┘
```

---

## 4. Artefactos del Flujo SDD

| Artefacto | Generado por | Aprobado por | Almacenado en |
|-----------|-------------|--------------|---------------|
| **Concept Brief** | Agente Conceptualización | Developer | Memory Banks |
| **Functional Spec** | Agente OpenSpec | Developer / PO | Repositorio Git |
| **Technical Spec** | Agente OpenSpec | Tech Lead | Repositorio Git |
| **API Spec** | Agente OpenSpec | Arquitecto | Repositorio Git |
| **Estimación** | Agente Estimación | Tech Lead | Memory Banks |
| **Informe de Revisión** | Agente Revisión | Developer | Memory Banks |
| **Código** | CLINE | Developer | Repositorio Git |
| **Tests** | Agente Testing / CLINE | Developer | Repositorio Git |
| **Documentación** | CLINE | Developer | Memory Banks + Vector DB |

---

## 5. Integración con Herramientas Existentes

### 5.1 Con Remedy (ITSM)
- Cada spec tiene un **ticket Remedy de origen**
- El MCP Remedy permite obtener el contexto del ticket directamente
- Al completar el desarrollo, se actualiza el ticket automáticamente

### 5.2 Con Git
- Las specs se versionan en el mismo repositorio que el código
- Los commits referencian el ID de la spec (`SPEC-001: Implementa...`)
- Las specs aprobadas se marcan con un tag en Git

### 5.3 Con CI/CD
- Los tests generados por el Agente de Testing se integran en el pipeline
- El pipeline verifica que el código cumple la spec antes de hacer merge
- Los resultados de testing se reportan en el ticket Remedy

---

## 6. Métricas del Proceso SDD

| Métrica | Descripción | Objetivo |
|---------|-------------|---------|
| **Spec Coverage** | % de features con spec aprobada antes de codificar | 100% |
| **Spec Quality Score** | Puntuación de completitud y claridad de las specs | > 80% |
| **Estimation Accuracy** | Desviación entre estimación y tiempo real | < 20% |
| **Defect Escape Rate** | % de defectos no detectados en la fase de spec | < 10% |
| **Spec-to-Code Time** | Tiempo desde spec aprobada hasta código listo | Baseline + mejora |
| **Rework Rate** | % de código que requiere reescritura por spec incorrecta | < 5% |