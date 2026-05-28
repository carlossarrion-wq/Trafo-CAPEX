# 🤖 Catálogo de Agentes Especializados

## 1. Visión General del Ecosistema de Agentes

El ecosistema cuenta con una suite de agentes IA especializados que cubren todo el ciclo de vida del desarrollo. Cada agente tiene un rol específico, herramientas propias y produce artefactos concretos.

```
CICLO DE VIDA Y AGENTES
────────────────────────────────────────────────────────────────────────
  NECESIDAD     SPEC          ESTIMACIÓN    REVISIÓN      CÓDIGO
  DE NEGOCIO    FORMAL        Y PLAN        Y CHALLENGE   Y TESTS
      │             │              │              │            │
      ▼             ▼              ▼              ▼            ▼
  [Agente de]  [Agentes      [Agente de    [Agente de   [CLINE +
  [Concept.]   [OpenSpec]    [Estimación]  [Revisión]   [Agente
                                                        [Testing]
────────────────────────────────────────────────────────────────────────
```

---

## 2. Agente de Conceptualización

### 2.1 Propósito
Transforma **necesidades de negocio informales** en **Concept Briefs estructurados** que sirven de base para la generación de specs formales.

### 2.2 Perfil del Agente

| Atributo | Valor |
|----------|-------|
| **Nombre** | Conceptualization Agent |
| **Rol** | Analista de Negocio / Arquitecto de Solución |
| **Fase** | Pre-Spec |
| **Input** | Descripción informal, ticket Remedy, conversación con el developer |
| **Output** | Concept Brief estructurado |

### 2.3 Capacidades
- Comprensión de lenguaje natural de negocio
- Identificación de requisitos implícitos
- Detección de ambigüedades y contradicciones
- Consulta de Memory Banks para contexto histórico
- Consulta de Vector DB para soluciones similares previas
- Consulta de Graph DB para entender impacto en el sistema

### 2.4 Plantilla de Concept Brief

```markdown
# Concept Brief: [Nombre]

## 1. Problema / Necesidad
[Descripción clara del problema que se quiere resolver]

## 2. Contexto de Negocio
[Por qué es importante, qué proceso afecta, quiénes son los usuarios]

## 3. Solución Propuesta
[Descripción de alto nivel de la solución]

## 4. Alcance
### En alcance:
- [Item 1]
### Fuera de alcance:
- [Item 1]

## 5. Restricciones y Supuestos
- [Restricción/Supuesto 1]

## 6. Dependencias
- [Sistema/Componente del que depende]

## 7. Criterios de Éxito
- [Criterio verificable 1]

## 8. Riesgos Identificados
| Riesgo | Probabilidad | Impacto | Mitigación |
|--------|-------------|---------|------------|

## 9. Preguntas Abiertas
- [Pregunta que necesita respuesta antes de continuar]
```

### 2.5 Skill Especializado por Tecnología
El agente adapta su análisis según la tecnología:
- **SAP**: Conoce los módulos SAP, procesos de negocio estándar, restricciones de customizing
- **Microsoft**: Conoce el ecosistema Azure, Power Platform, patrones de integración
- **MuleSoft**: Conoce los patrones de integración, API-led connectivity
- **Darwin**: Conoce la arquitectura React/PHP, patrones de UX, APIs REST

---

## 3. Agentes OpenSpec

### 3.1 Propósito
Suite de agentes que generan **especificaciones formales** a partir del Concept Brief aprobado. Cada agente se especializa en un tipo de spec.

### 3.2 Agente de Spec Funcional

| Atributo | Valor |
|----------|-------|
| **Nombre** | Functional Spec Agent |
| **Rol** | Analista Funcional / Product Owner técnico |
| **Input** | Concept Brief aprobado |
| **Output** | Functional Spec (historias de usuario, criterios de aceptación, flujos) |

**Capacidades:**
- Generación de User Stories en formato estándar (Como... Quiero... Para...)
- Definición de criterios de aceptación en formato Gherkin (Given/When/Then)
- Modelado de flujos de negocio (happy path + alternativas + errores)
- Identificación de reglas de negocio
- Detección de casos edge y excepciones

**Ejemplo de output:**
```gherkin
Feature: Creación de pedido de compra en SAP

  Scenario: Creación exitosa de pedido
    Given el usuario tiene rol de comprador
    And existe un proveedor activo con código "PROV001"
    When el usuario crea un pedido con 3 posiciones
    Then el pedido se crea con estado "Abierto"
    And se genera un número de pedido único
    And se envía notificación al proveedor
```

### 3.3 Agente de Spec Técnica

| Atributo | Valor |
|----------|-------|
| **Nombre** | Technical Spec Agent |
| **Rol** | Arquitecto de Solución / Tech Lead |
| **Input** | Functional Spec aprobada + contexto técnico del proyecto |
| **Output** | Technical Spec (diseño, componentes, interfaces, modelo de datos) |

**Capacidades:**
- Diseño de la solución técnica
- Definición de componentes y sus responsabilidades
- Diseño de interfaces entre componentes
- Modelado de datos (entidades, atributos, relaciones)
- Identificación de patrones de diseño aplicables
- Consideraciones de seguridad, rendimiento y escalabilidad
- Consulta de Memory Banks para decisiones de arquitectura previas
- Consulta de Graph DB para entender el impacto en el sistema existente

### 3.4 Agente de Spec de API

| Atributo | Valor |
|----------|-------|
| **Nombre** | API Spec Agent |
| **Rol** | API Designer |
| **Input** | Technical Spec + estándares de API del proyecto |
| **Output** | OpenAPI 3.0 / RAML spec completa |

**Capacidades:**
- Generación de specs OpenAPI 3.0 o RAML
- Diseño de endpoints RESTful siguiendo best practices
- Definición de modelos de datos (schemas)
- Especificación de autenticación y autorización
- Generación de ejemplos de request/response
- Definición de códigos de error y mensajes

### 3.5 Agente de Spec de Testing

| Atributo | Valor |
|----------|-------|
| **Nombre** | Test Spec Agent |
| **Rol** | QA Engineer / Test Architect |
| **Input** | Functional Spec + Technical Spec |
| **Output** | Test Spec (estrategia, casos de prueba, criterios de cobertura) |

**Capacidades:**
- Definición de estrategia de testing (unitario, integración, E2E)
- Generación de casos de prueba a partir de criterios de aceptación
- Identificación de casos edge y negativos
- Definición de datos de prueba
- Criterios de cobertura de código

---

## 4. Agente de Estimación

### 4.1 Propósito
Genera **estimaciones de esfuerzo** precisas y fundamentadas a partir de las specs aprobadas, utilizando datos históricos del proyecto.

### 4.2 Perfil del Agente

| Atributo | Valor |
|----------|-------|
| **Nombre** | Estimation Agent |
| **Rol** | Project Manager / Tech Lead |
| **Input** | Functional Spec + Technical Spec |
| **Output** | Estimación detallada con rangos de confianza |

### 4.3 Metodología de Estimación

```
PROCESO DE ESTIMACIÓN
─────────────────────────────────────────────────────────────
1. DESCOMPOSICIÓN
   └─ Divide la spec en tareas atómicas estimables

2. ESTIMACIÓN BASE
   └─ Estima cada tarea en horas/story points

3. AJUSTE POR COMPLEJIDAD
   └─ Aplica factores de complejidad técnica

4. AJUSTE POR RIESGO
   └─ Añade buffer por riesgos identificados

5. AJUSTE HISTÓRICO
   └─ Calibra con datos de proyectos similares (Memory Banks)

6. RANGO DE CONFIANZA
   └─ Genera estimación optimista / probable / pesimista
─────────────────────────────────────────────────────────────
```

### 4.4 Plantilla de Estimación

```markdown
# Estimación: [Nombre del Feature]

## Resumen
| Escenario | Horas | Story Points |
|-----------|-------|-------------|
| Optimista | X h   | X SP        |
| Probable  | X h   | X SP        |
| Pesimista | X h   | X SP        |

## Desglose por Tarea
| Tarea | Complejidad | Horas | Notas |
|-------|-------------|-------|-------|
| [Tarea 1] | Alta/Media/Baja | X h | [notas] |

## Supuestos
- [Supuesto que afecta a la estimación]

## Riesgos que Afectan la Estimación
| Riesgo | Impacto en horas | Probabilidad |
|--------|-----------------|-------------|

## Datos Históricos Utilizados
- [Referencia a proyecto/feature similar]
```

---

## 5. Agente de Revisión / Challenge

### 5.1 Propósito
Actúa como **revisor crítico** de specs y estimaciones, identificando problemas, inconsistencias y oportunidades de mejora antes de que comience el desarrollo.

### 5.2 Perfil del Agente

| Atributo | Valor |
|----------|-------|
| **Nombre** | Review & Challenge Agent |
| **Rol** | Arquitecto Senior / Revisor de Calidad |
| **Input** | Specs completas + Estimación |
| **Output** | Informe de revisión con observaciones categorizadas |

### 5.3 Dimensiones de Revisión

| Dimensión | Qué verifica |
|-----------|-------------|
| **Completitud** | ¿Están todos los casos cubiertos? ¿Faltan escenarios? |
| **Consistencia** | ¿Son coherentes la spec funcional y la técnica? |
| **Claridad** | ¿Son los criterios de aceptación verificables y sin ambigüedad? |
| **Viabilidad** | ¿Es técnicamente viable la solución propuesta? |
| **Estimación** | ¿Es la estimación coherente con la complejidad? |
| **Riesgos** | ¿Se han identificado todos los riesgos relevantes? |
| **Estándares** | ¿Cumple con los estándares y patrones del proyecto? |
| **Seguridad** | ¿Se han considerado los aspectos de seguridad? |

### 5.4 Categorías de Observaciones

```
🔴 BLOQUEANTE   → Debe resolverse antes de continuar
🟡 IMPORTANTE   → Debe resolverse, puede continuar con cautela
🟢 SUGERENCIA   → Mejora recomendada, no bloquea
❓ PREGUNTA     → Necesita aclaración del developer/PO
```

---

## 6. CLINE — Agente de Codificación

### 6.1 Propósito
**Implementa el código** a partir de las specs aprobadas, utilizando todo el contexto disponible (Memory Banks, Vector DB, Graph DB, Skills, Reglas).

### 6.2 Modo de Operación con SDD

```
CLINE EN MODO SDD
─────────────────────────────────────────────────────────────
1. LEE las specs aprobadas (Functional + Technical + API)
2. CARGA el contexto del proyecto (Memory Banks)
3. CONSULTA código similar (Vector DB)
4. VERIFICA dependencias (Graph DB)
5. APLICA skills de tecnología y reglas Cline
6. GENERA el código siguiendo la spec
7. GENERA tests basados en la Test Spec
8. GENERA documentación inline
9. ACTUALIZA Memory Banks con nuevas decisiones
─────────────────────────────────────────────────────────────
```

### 6.3 Skills por Tecnología

Ver documento [Componentes Core](../arquitectura/03_componentes_core.md) para el detalle de cada skill.

---

## 7. Agente de Testing

### 7.1 Propósito
Genera y ejecuta **casos de prueba** basados en la Test Spec, verificando que el código implementado cumple los criterios de aceptación.

### 7.2 Perfil del Agente

| Atributo | Valor |
|----------|-------|
| **Nombre** | Testing Agent |
| **Rol** | QA Engineer / Test Automation Engineer |
| **Input** | Test Spec + Código implementado |
| **Output** | Tests ejecutables + Reporte de cobertura |

### 7.3 Tipos de Tests Generados

| Tipo | Framework (SAP) | Framework (MSFT) | Framework (Mule) | Framework (Darwin) |
|------|----------------|-----------------|-----------------|-------------------|
| **Unitario** | ABAP Unit | xUnit / NUnit | MUnit | Jest / PHPUnit |
| **Integración** | ABAP Unit + RFC | Integration Tests | MUnit + HTTP | Cypress / PHPUnit |
| **E2E** | CBTA / Selenium | Playwright | Postman/Newman | Cypress |
| **API** | — | REST Assured | MUnit | Supertest |

---

## 8. Orquestación de Agentes

### 8.1 Flujo de Orquestación

Los agentes no operan de forma aislada; se orquestan en un flujo coordinado:

```
ORQUESTACIÓN
─────────────────────────────────────────────────────────────
• Los agentes se invocan secuencialmente según el flujo SDD
• El output de cada agente es el input del siguiente
• El developer actúa como punto de control entre fases
• Los agentes comparten el mismo contexto (Memory Banks)
• Cline puede invocar agentes auxiliares durante la codificación
─────────────────────────────────────────────────────────────
```

### 8.2 Comunicación entre Agentes
- Los artefactos se almacenan en el repositorio Git del proyecto
- Los agentes leen los artefactos de fases anteriores como contexto
- El Memory Bank actúa como memoria compartida entre agentes
- Los MCP servers son accesibles por todos los agentes

### 8.3 Intervención Humana
El developer interviene en los siguientes puntos de control:

| Punto de Control | Decisión |
|-----------------|----------|
| Tras Concept Brief | Aprobar / Rechazar / Modificar |
| Tras Specs | Aprobar / Rechazar / Iterar |
| Tras Estimación | Aprobar / Ajustar alcance |
| Tras Revisión | Resolver observaciones / Aprobar |
| Tras Código | Code review / Aprobar merge |
| Tras Testing | Aprobar resultados / Solicitar fixes |