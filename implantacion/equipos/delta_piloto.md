# 🟣 Plan Piloto — Equipo Delta (Java)

## 1. Contexto del Piloto Delta

### 1.1 Descripción del Sistema
**Delta** es un sistema de desarrollo a medida basado en **Java**, con arquitectura monolítica que cubre múltiples funciones de negocio. Su naturaleza de monolito implica consideraciones específicas en cuanto a la gestión del conocimiento, el análisis de impacto de cambios y la estrategia de desarrollo con IA.

### 1.2 Stack Tecnológico del Equipo

| Tecnología | Descripción |
|------------|-------------|
| **Java** | Lenguaje principal (Java 8/11/17) |
| **Spring / Spring Boot** | Framework de aplicación (si aplica) |
| **Maven / Gradle** | Gestión de dependencias y build |
| **Base de datos relacional** | Oracle / MySQL / PostgreSQL |
| **Git** | Control de versiones |
| **Servidor de aplicaciones** | Tomcat / JBoss / WebLogic (según entorno) |

### 1.3 Consideraciones Específicas del Monolito

El carácter monolítico de Delta introduce retos particulares que el ecosistema debe abordar:

| Reto | Implicación para el Ecosistema |
|------|-------------------------------|
| **Gran base de código** | La Vector DB y el Graph DB son especialmente críticos para navegar el código |
| **Alto acoplamiento** | El análisis de impacto (Graph DB) es esencial antes de cualquier cambio |
| **Conocimiento concentrado** | Los Memory Banks son clave para capturar el conocimiento tácito del equipo |
| **Riesgo de regresión** | Los tests generados por Cline deben cubrir los flujos críticos existentes |
| **Deuda técnica acumulada** | Cline puede ayudar a identificar y documentar la deuda técnica |

### 1.4 Información del Equipo

| Campo | Valor |
|-------|-------|
| **Nombre del equipo** | [Por definir] |
| **Tech Lead** | [Por definir] |
| **Número de developers** | [Por definir] |
| **Proyectos activos** | [Por definir] |
| **Fecha de inicio del piloto** | [Por definir] |

---

## 2. Componentes del Ecosistema para Delta

### 2.1 Reglas Cline para Delta (`.clinerules/delta.md`)

```
ESTÁNDARES DELTA — RESUMEN
├── JAVA (BACKEND)
│   ├── Seguir convenciones de naming Java (camelCase, PascalCase)
│   ├── Principios SOLID y Clean Code
│   ├── Arquitectura en capas (Controller → Service → Repository/DAO)
│   ├── Manejo de excepciones con jerarquía propia
│   ├── Logging con SLF4J / Log4j2
│   ├── Javadoc en clases y métodos públicos
│   └── Tests con JUnit 5 + Mockito
│
├── MONOLITO — REGLAS ESPECÍFICAS
│   ├── SIEMPRE consultar Graph DB antes de modificar una clase
│   │   (para entender el impacto en el resto del sistema)
│   ├── SIEMPRE buscar en Vector DB código similar antes de crear nuevo
│   │   (el monolito tiende a tener duplicidades)
│   ├── Documentar en Memory Bank cualquier decisión de arquitectura
│   ├── Añadir tests de regresión para cualquier cambio en flujos críticos
│   └── Identificar y documentar dependencias circulares encontradas
│
├── BASE DE DATOS
│   ├── Usar transacciones para operaciones críticas
│   ├── Índices en campos de búsqueda frecuente
│   ├── Evitar N+1 queries
│   └── Scripts de migración versionados
│
└── TESTING
    ├── JUnit 5 para tests unitarios
    ├── Mockito para mocks
    ├── Cobertura mínima del 70% en código nuevo
    ├── Tests de integración para flujos críticos del negocio
    └── Tests de regresión obligatorios en cambios sobre código existente
```

### 2.2 Libro Blanco Delta

El Libro Blanco Delta cubre:
- Guía de desarrollo Java moderno (Clean Code, SOLID, patrones de diseño)
- Estrategia de trabajo con monolitos (cómo navegar, entender y modificar con seguridad)
- Guía de testing en Java (JUnit 5, Mockito, tests de integración)
- Patrones de refactorización segura en monolitos
- Guía de uso del Graph DB para análisis de impacto en Delta
- Estrategia de gestión de la deuda técnica con IA

### 2.3 Memory Bank Delta

```
memory-bank/
├── projectbrief.md
├── productContext.md
├── systemPatterns.md      ← Especialmente importante: arquitectura del monolito
├── techContext.md
├── activeContext.md
├── progress.md
├── module_map.md          ← Mapa de módulos/paquetes del monolito y sus responsabilidades
├── critical_flows.md      ← Flujos de negocio críticos y los componentes que los implementan
├── known_issues.md        ← Deuda técnica conocida, bugs recurrentes, áreas de riesgo
└── db_schema.md           ← Esquema de base de datos (tablas, relaciones, procedimientos)
```

### 2.4 Graph DB — Especialmente Crítico para Delta

Para un monolito Java, el Graph DB es el componente más valioso del ecosistema. Permite:

```
CASOS DE USO GRAPH DB EN DELTA
────────────────────────────────────────────────────────────
  ANTES DE CUALQUIER CAMBIO:
  → graph_impact_analysis: "¿Qué clases usan este método?"
  → graph_get_dependencies: "¿De qué depende este módulo?"
  → graph_find_path: "¿Cómo llega la llamada desde el Controller hasta aquí?"

  PARA ENTENDER EL SISTEMA:
  → graph_get_neighbors: "¿Qué clases están relacionadas con este servicio?"
  → graph_query: "¿Qué módulos tienen más dependencias?" (identificar hotspots)

  PARA GESTIONAR LA DEUDA TÉCNICA:
  → graph_query: "¿Hay dependencias circulares en el paquete X?"
  → graph_query: "¿Qué clases tienen más de 10 dependencias?" (God classes)
────────────────────────────────────────────────────────────
```

---

## 3. Plan de Adopción — 3 Meses

### 3.1 Mes 1: Arranque y Adopción Básica

#### Semana 1-2: Onboarding Delta
- [ ] Formación: Introducción al Ecosistema (2h)
- [ ] Formación: Cline Básico (4h)
- [ ] Formación: Memory Banks (2h)
- [ ] Configuración de VS Code + Cline
- [ ] Configuración del MCP Remedy
- [ ] Configuración del MCP Vector DB
- [ ] **Indexación inicial del codebase Java en Vector DB** (tarea crítica para Delta)
- [ ] **Modelado inicial del grafo de dependencias en Graph DB** (tarea crítica para Delta)
- [ ] Primera sesión práctica: navegar el monolito con Cline

#### Semana 3-4: Primeros Casos Reales
- [ ] Usar Cline para entender un módulo complejo del monolito
- [ ] Usar Graph DB para analizar el impacto de un cambio real
- [ ] Crear el Memory Bank del proyecto (especialmente `module_map.md` y `critical_flows.md`)
- [ ] Usar Cline para resolver una incidencia con contexto de Remedy
- [ ] Documentar primeras impresiones y ajustes necesarios

**Hito Mes 1**: Todos los developers han usado Cline + Graph DB para analizar al menos 1 cambio real

### 3.2 Mes 2: Adopción del Flujo SDD

#### Semana 5-6: Spec Driven Development Delta
- [ ] Formación: Spec Driven Development (4h)
- [ ] Formación: Agentes OpenSpec (3h)
- [ ] Primera Functional Spec de una nueva funcionalidad
- [ ] Primera Technical Spec Java (con análisis de impacto en el monolito)
- [ ] Primera estimación con el Agente de Estimación

#### Semana 7-8: Flujo Completo
- [ ] Flujo SDD completo en un feature real (spec → código → test)
- [ ] Cline consulta Graph DB antes de cada modificación
- [ ] Cline genera tests JUnit + Mockito
- [ ] Cline genera tests de regresión para flujos afectados
- [ ] Uso activo de MCP Remedy para vincular código con tickets

**Hito Mes 2**: Al menos 2 features desarrollados con el flujo SDD completo y análisis de impacto

### 3.3 Mes 3: Consolidación y Medición

#### Semana 9-10: Autonomía Delta
- [ ] Equipo opera el flujo SDD sin soporte constante
- [ ] Memory Banks actualizados con mapa de módulos y flujos críticos
- [ ] Graph DB con modelo completo de dependencias del monolito
- [ ] Vector DB con codebase Java completo indexado

#### Semana 11-12: Medición y Cierre
- [ ] Medición de KPIs
- [ ] Encuesta de satisfacción al equipo
- [ ] Documentación de lecciones aprendidas
- [ ] Identificación del "champion" Delta para la expansión

---

## 4. KPIs del Piloto Delta

| KPI | Baseline | Objetivo Mes 1 | Objetivo Mes 2 | Objetivo Mes 3 |
|-----|---------|---------------|---------------|---------------|
| % developers usando Cline | 0% | > 80% | > 90% | > 95% |
| % cambios con análisis de impacto previo (Graph DB) | 0% | > 50% | > 80% | > 95% |
| % features con spec previa | 0% | 20% | 60% | > 80% |
| Tiempo en entender un módulo desconocido | [baseline] | -30% | -50% | -60% |
| Tiempo en resolver incidencias | [baseline] | -10% | -25% | -40% |
| Cobertura de tests en código nuevo | [baseline] | +10% | +20% | +30% |
| NPS del equipo | — | — | — | > 40 |

---

## 5. Casos de Uso Prioritarios para el Piloto Delta

### Caso 1: Modificación de Funcionalidad Existente en el Monolito
```
Escenario: Modificar la lógica de cálculo de un proceso de negocio crítico
──────────────────────────────────────────────────────────────────────────
1. Developer consulta MCP Remedy → obtiene detalle del ticket
2. Graph DB → Cline analiza el impacto: qué clases usan el método a modificar
3. Vector DB → Cline busca implementaciones similares en el codebase
4. Agentes OpenSpec generan Technical Spec con el análisis de impacto incluido
5. Cline implementa el cambio con mínimo impacto en el resto del sistema
6. Cline genera tests de regresión para todos los flujos afectados
7. Developer revisa y valida
8. Memory Bank actualizado con la decisión técnica
```

### Caso 2: Resolución de Incidencia en Producción
```
Escenario: NullPointerException en un flujo de negocio crítico
──────────────────────────────────────────────────────────────────────────
1. MCP Remedy → Cline obtiene el stack trace y descripción del error
2. Vector DB → Cline busca la clase y método donde ocurre el error
3. Graph DB → Cline entiende el contexto: quién llama a este método
4. Cline analiza el código y propone el fix
5. Cline genera test de regresión que reproduce el bug
6. Developer valida el fix y el test
7. MCP Remedy → worklog actualizado
```

### Caso 3: Comprensión de un Módulo Desconocido
```
Escenario: Developer nuevo necesita entender el módulo de facturación
──────────────────────────────────────────────────────────────────────────
1. Memory Bank → Cline lee el module_map.md y critical_flows.md
2. Graph DB → Cline genera el mapa de dependencias del módulo
3. Vector DB → Cline busca las clases principales del módulo
4. Cline genera un resumen del módulo: responsabilidades, flujos, dependencias
5. Cline genera un diagrama de la arquitectura del módulo
6. Developer tiene contexto completo en minutos en lugar de días
```

### Caso 4: Identificación y Documentación de Deuda Técnica
```
Escenario: Auditoría de calidad del código del monolito
──────────────────────────────────────────────────────────────────────────
1. Graph DB → Cline identifica clases con más de 10 dependencias (God classes)
2. Graph DB → Cline detecta dependencias circulares entre paquetes
3. Vector DB → Cline busca código duplicado en el codebase
4. Cline genera informe de deuda técnica con priorización
5. Memory Bank → known_issues.md actualizado con los hallazgos
6. Tech Lead usa el informe para planificar la refactorización
```

---

## 6. Riesgos Específicos del Piloto Delta

| Riesgo | Probabilidad | Impacto | Mitigación |
|--------|-------------|---------|------------|
| Tamaño del codebase dificulta la indexación en Vector DB | Alta | Medio | Indexación incremental por módulos, empezar por los más activos |
| Modelado del grafo de dependencias complejo en un monolito | Alta | Alto | Dedicar semana 1 completa al modelado inicial del grafo |
| Cline genera código que rompe otras partes del monolito | Media | Alto | Regla obligatoria: consultar Graph DB antes de cualquier cambio |
| Resistencia por complejidad percibida del ecosistema | Media | Medio | Mostrar valor rápido con el caso de uso de comprensión de módulos |
| Deuda técnica tan elevada que dificulta el trabajo de Cline | Media | Medio | Documentar la deuda en Memory Bank, trabajar módulo a módulo |
| Falta de tests existentes dificulta la validación de cambios | Alta | Alto | Priorizar la generación de tests de regresión desde el inicio |