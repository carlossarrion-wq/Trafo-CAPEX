# 🟦 Plan Piloto — Equipo Microsoft

## 1. Contexto del Piloto Microsoft

### 1.1 Descripción del Equipo
El equipo piloto Microsoft es el primer equipo del área Microsoft en adoptar el ecosistema de desarrollo aumentado por IA. Su experiencia servirá de referencia para el resto de equipos Microsoft de la organización.

### 1.2 Stack Tecnológico del Equipo

| Tecnología | Descripción |
|------------|-------------|
| **.NET / C#** | Lenguaje y framework principal de desarrollo |
| **Azure** | Plataforma cloud (App Services, Functions, AKS, etc.) |
| **Azure DevOps** | Gestión de código, pipelines CI/CD, work items |
| **Power Platform** | Power Apps, Power Automate, Power BI (si aplica) |
| **Microsoft Graph** | APIs de Microsoft 365 |
| **SQL Server / Azure SQL** | Base de datos principal |

### 1.3 Información del Equipo

| Campo | Valor |
|-------|-------|
| **Nombre del equipo** | [Por definir] |
| **Tech Lead** | [Por definir] |
| **Número de developers** | [Por definir] |
| **Proyectos activos** | [Por definir] |
| **Fecha de inicio del piloto** | [Por definir] |

---

## 2. Componentes del Ecosistema para Microsoft

### 2.1 MCP Microsoft — Capacidades Específicas

```
MCP MICROSOFT — HERRAMIENTAS DISPONIBLES
├── Azure DevOps
│   ├── ado_get_workitem        → Obtener work item (historia, bug, tarea)
│   ├── ado_search_workitems    → Buscar work items por criterios
│   ├── ado_create_workitem     → Crear work item
│   ├── ado_get_repo            → Info de repositorio
│   ├── ado_get_file            → Leer archivo del repo
│   ├── ado_list_pipelines      → Listar pipelines CI/CD
│   └── ado_get_pipeline_run    → Resultado de ejecución de pipeline
│
└── Microsoft Graph
    ├── graph_get_user          → Info de usuario
    ├── graph_search_sharepoint → Buscar en SharePoint
    └── graph_get_teams_channel → Mensajes de canal Teams
```

### 2.2 Reglas Cline para Microsoft (`.clinerules/microsoft.md`)

```
ESTÁNDARES MICROSOFT — RESUMEN
├── NAMING CONVENTIONS (.NET)
│   ├── Clases: PascalCase (ej: OrderService)
│   ├── Métodos: PascalCase (ej: GetOrderById)
│   ├── Variables: camelCase (ej: orderId)
│   ├── Constantes: UPPER_SNAKE_CASE
│   └── Interfaces: IPascalCase (ej: IOrderRepository)
│
├── ARQUITECTURA
│   ├── Seguir Clean Architecture / Hexagonal
│   ├── Separar capas: Domain, Application, Infrastructure, API
│   ├── Usar inyección de dependencias (DI)
│   ├── Aplicar principios SOLID
│   └── Usar patrones Repository y Unit of Work
│
├── AZURE
│   ├── Usar Managed Identities (no credenciales hardcoded)
│   ├── Configuración via Azure App Configuration / Key Vault
│   ├── Logging con Application Insights
│   └── Health checks en todos los servicios
│
└── TESTING
    ├── xUnit para tests unitarios
    ├── Cobertura mínima del 80%
    ├── Tests de integración con TestContainers
    └── Mocks con Moq/NSubstitute
```

### 2.3 Libro Blanco Microsoft

El Libro Blanco Microsoft cubre:
- Guía de arquitectura .NET (Clean Architecture, CQRS, Event Sourcing)
- Patrones de desarrollo Azure (microservicios, serverless, containers)
- Guía de CI/CD con Azure DevOps
- Estándares de seguridad Azure (RBAC, Managed Identities, Key Vault)
- Guía de testing (.NET testing pyramid)
- Patrones de integración con Microsoft 365

### 2.4 Memory Bank Microsoft

```
memory-bank/
├── projectbrief.md
├── productContext.md
├── systemPatterns.md
├── techContext.md
├── activeContext.md
├── progress.md
├── azure_resources.md     ← Recursos Azure del proyecto (RGs, servicios)
├── ado_structure.md       ← Repos, pipelines, boards en Azure DevOps
└── power_platform.md      ← Componentes Power Platform (si aplica)
```

---

## 3. Plan de Adopción — 3 Meses

### 3.1 Mes 1: Arranque y Adopción Básica

#### Semana 1-2: Onboarding Microsoft
- [ ] Formación: Introducción al Ecosistema (2h)
- [ ] Formación: Cline Básico (4h)
- [ ] Formación: Memory Banks (2h)
- [ ] Configuración de VS Code + Cline en cada máquina
- [ ] Configuración del MCP Microsoft (Azure DevOps + Graph)
- [ ] Configuración del MCP Remedy
- [ ] Primera sesión práctica: explorar codebase .NET con Cline

#### Semana 3-4: Primeros Casos Reales Microsoft
- [ ] Usar Cline para entender un servicio .NET complejo existente
- [ ] Usar MCP Azure DevOps para obtener contexto de work items
- [ ] Crear el Memory Bank del primer proyecto piloto
- [ ] Usar Cline para resolver un bug con contexto de ADO + Remedy
- [ ] Documentar primeras impresiones y ajustes necesarios

**Hito Mes 1**: Todos los developers han usado Cline en al menos 3 tareas reales

### 3.2 Mes 2: Adopción del Flujo SDD

#### Semana 5-6: Spec Driven Development Microsoft
- [ ] Formación: Spec Driven Development (4h)
- [ ] Formación: Agentes OpenSpec (3h)
- [ ] Primera Functional Spec generada con agentes OpenSpec
- [ ] Primera Technical Spec .NET (con patrones Clean Architecture)
- [ ] Primera API Spec (OpenAPI 3.0) generada por el Agente de API Spec
- [ ] Primera estimación con el Agente de Estimación

#### Semana 7-8: Flujo Completo con MCP
- [ ] Flujo SDD completo en un feature real (spec → código → test)
- [ ] Uso activo de MCP Azure DevOps durante el desarrollo
- [ ] Uso activo de MCP Remedy para vincular código con tickets
- [ ] Primeros tests xUnit generados por Cline
- [ ] Actualización del Memory Bank con decisiones del sprint

**Hito Mes 2**: Al menos 2 features desarrollados con el flujo SDD completo

### 3.3 Mes 3: Consolidación y Medición

#### Semana 9-10: Autonomía Microsoft
- [ ] Equipo opera el flujo SDD sin soporte constante
- [ ] Memory Banks actualizados y enriquecidos
- [ ] Vector DB con documentación .NET/Azure del proyecto indexada
- [ ] Graph DB con relaciones de servicios y dependencias modeladas

#### Semana 11-12: Medición y Cierre del Piloto
- [ ] Medición de KPIs
- [ ] Encuesta de satisfacción al equipo
- [ ] Documentación de lecciones aprendidas
- [ ] Presentación de resultados al Sponsor
- [ ] Identificación del "champion" Microsoft para la expansión

---

## 4. KPIs del Piloto Microsoft

| KPI | Baseline | Objetivo Mes 1 | Objetivo Mes 2 | Objetivo Mes 3 |
|-----|---------|---------------|---------------|---------------|
| % developers usando Cline | 0% | > 80% | > 90% | > 95% |
| % features con spec previa | 0% | 20% | 60% | > 80% |
| Tiempo medio en code review | [baseline] | -10% | -25% | -35% |
| Tiempo medio en resolver bugs | [baseline] | -10% | -25% | -40% |
| Cobertura de tests unitarios | [baseline] | +5% | +15% | +25% |
| NPS del equipo | — | — | — | > 40 |

---

## 5. Casos de Uso Prioritarios para el Piloto Microsoft

### Caso 1: Nuevo Endpoint REST en .NET
```
Escenario: Añadir endpoint de búsqueda avanzada a una API existente
─────────────────────────────────────────────────────────────────────
1. Developer obtiene la historia de usuario de ADO (MCP Azure DevOps)
2. Agente de Conceptualización analiza la necesidad
3. Agentes OpenSpec generan Functional + Technical + API Spec
   (API Spec en OpenAPI 3.0, siguiendo estándares del proyecto)
4. Cline implementa el endpoint siguiendo Clean Architecture
   (Controller → Application → Domain → Infrastructure)
5. Cline genera tests xUnit con mocks
6. Developer revisa, hace merge, pipeline CI/CD se ejecuta
7. MCP Azure DevOps → work item actualizado automáticamente
```

### Caso 2: Diagnóstico de Fallo en Azure
```
Escenario: Servicio Azure Function fallando en producción
─────────────────────────────────────────────────────────────────────
1. Developer consulta MCP Remedy → obtiene detalle del incidente
2. MCP Azure DevOps → verifica si hay pipeline fallido reciente
3. Cline analiza el código de la Function afectada
4. Graph DB → Cline entiende dependencias del servicio
5. Vector DB → Cline busca incidencias similares resueltas
6. Cline propone el fix con tests
7. Developer valida, merge y despliegue
8. MCP Remedy → worklog actualizado
```

---

## 6. Riesgos Específicos del Piloto Microsoft

| Riesgo | Probabilidad | Impacto | Mitigación |
|--------|-------------|---------|------------|
| Permisos insuficientes en Azure DevOps | Media | Alto | Configurar Service Principal con permisos adecuados |
| Variedad de proyectos .NET (versiones, frameworks) | Alta | Medio | Reglas Cline adaptables, Libro Blanco con múltiples versiones |
| Resistencia si ya usan GitHub Copilot | Media | Medio | Mostrar valor diferencial de Cline (MCP, Memory Banks, SDD) |
| Complejidad de arquitecturas Azure existentes | Media | Medio | Modelar en Graph DB desde el inicio |