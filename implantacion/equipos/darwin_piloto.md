# 🟢 Plan Piloto — Equipo Darwin (React + PHP)

## 1. Contexto del Piloto Darwin

### 1.1 Stack Tecnológico

| Tecnología | Descripción |
|------------|-------------|
| **React** | Framework frontend (hooks, context, Redux) |
| **PHP** | Backend (Laravel / Symfony) |
| **REST APIs** | Comunicación frontend-backend |
| **MySQL / PostgreSQL** | Base de datos relacional |
| **Git** | Control de versiones |
| **Docker** | Contenedores para desarrollo y despliegue |

### 1.2 Información del Equipo

| Campo | Valor |
|-------|-------|
| **Nombre del equipo** | [Por definir] |
| **Tech Lead** | [Por definir] |
| **Número de developers** | [Por definir] |
| **Proyectos activos** | [Por definir] |
| **Fecha de inicio del piloto** | [Por definir] |

---

## 2. Componentes del Ecosistema para Darwin

### 2.1 Reglas Cline para Darwin (`.clinerules/darwin.md`)

```
ESTÁNDARES DARWIN — RESUMEN
├── REACT (FRONTEND)
│   ├── Functional components + hooks (no class components)
│   ├── Custom hooks para lógica reutilizable
│   ├── Context API / Redux para estado global
│   ├── Componentes pequeños con responsabilidad única
│   ├── Props tipadas con TypeScript o PropTypes
│   └── Tests con Jest + React Testing Library
│
├── PHP (BACKEND)
│   ├── PSR-12 coding standards
│   ├── Arquitectura en capas (Controller → Service → Repository)
│   ├── Inyección de dependencias
│   ├── Validación de inputs en Controller
│   ├── Manejo de excepciones centralizado
│   └── Tests con PHPUnit
│
├── API REST
│   ├── Convenciones REST (recursos, verbos HTTP)
│   ├── Versionar APIs (/api/v1/...)
│   ├── Respuestas JSON consistentes (data, error, meta)
│   ├── Autenticación con JWT / OAuth
│   └── Documentar con OpenAPI 3.0
│
└── BASE DE DATOS
    ├── Migraciones para cambios de esquema
    ├── Índices en campos de búsqueda frecuente
    ├── Evitar N+1 queries (eager loading)
    └── Transacciones para operaciones críticas
```

### 2.2 Memory Bank Darwin

```
memory-bank/
├── projectbrief.md
├── productContext.md
├── systemPatterns.md
├── techContext.md
├── activeContext.md
├── progress.md
├── component_library.md   ← Componentes React reutilizables
├── api_contracts.md       ← Contratos de API (endpoints, modelos)
└── db_schema.md           ← Esquema de base de datos
```

---

## 3. Plan de Adopción — 3 Meses

### 3.1 Mes 1: Arranque y Adopción Básica

#### Semana 1-2: Onboarding Darwin
- [ ] Formación: Introducción al Ecosistema (2h)
- [ ] Formación: Cline Básico (4h)
- [ ] Formación: Memory Banks (2h)
- [ ] Configuración de VS Code + Cline
- [ ] Configuración del MCP Remedy y MCP Vector DB
- [ ] Primera sesión práctica: explorar codebase React + PHP con Cline

#### Semana 3-4: Primeros Casos Reales
- [ ] Usar Cline para entender un componente React complejo existente
- [ ] Usar Cline para entender un servicio PHP complejo existente
- [ ] Crear el Memory Bank del primer proyecto piloto
- [ ] Usar Cline para resolver un bug con contexto de Remedy

**Hito Mes 1**: Todos los developers han usado Cline en al menos 3 tareas reales

### 3.2 Mes 2: Adopción del Flujo SDD

#### Semana 5-6: Spec Driven Development
- [ ] Formación: Spec Driven Development (4h)
- [ ] Formación: Agentes OpenSpec (3h)
- [ ] Primera Functional Spec de una nueva funcionalidad
- [ ] Primera Technical Spec (componentes React + endpoints PHP)
- [ ] Primera API Spec (OpenAPI 3.0)

#### Semana 7-8: Flujo Completo
- [ ] Flujo SDD completo en un feature real (spec → código → test)
- [ ] Cline genera componente React siguiendo las reglas Darwin
- [ ] Cline genera endpoint PHP con tests PHPUnit
- [ ] Uso activo de MCP Remedy para vincular código con tickets

**Hito Mes 2**: Al menos 2 features desarrollados con el flujo SDD completo

### 3.3 Mes 3: Consolidación y Medición

#### Semana 9-10: Autonomía
- [ ] Equipo opera el flujo SDD sin soporte constante
- [ ] Memory Banks actualizados con componentes y contratos de API
- [ ] Vector DB con codebase React + PHP indexado

#### Semana 11-12: Medición y Cierre
- [ ] Medición de KPIs
- [ ] Encuesta de satisfacción al equipo
- [ ] Documentación de lecciones aprendidas
- [ ] Identificación del "champion" Darwin para la expansión

---

## 4. KPIs del Piloto Darwin

| KPI | Baseline | Objetivo Mes 1 | Objetivo Mes 2 | Objetivo Mes 3 |
|-----|---------|---------------|---------------|---------------|
| % developers usando Cline | 0% | > 80% | > 90% | > 95% |
| % features con spec previa | 0% | 20% | 60% | > 80% |
| Tiempo en desarrollar componente React | [baseline] | -10% | -30% | -45% |
| Tiempo en desarrollar endpoint PHP | [baseline] | -10% | -30% | -45% |
| Cobertura de tests (Jest + PHPUnit) | [baseline] | +5% | +15% | +25% |
| NPS del equipo | — | — | — | > 40 |

---

## 5. Casos de Uso Prioritarios

### Caso 1: Nuevo Feature Full-Stack (React + PHP)
```
Escenario: Nueva pantalla de gestión con filtros avanzados
──────────────────────────────────────────────────────────
1. Agentes OpenSpec generan Functional + Technical + API Spec
2. Cline implementa el componente React (hooks, estado, llamadas API)
3. Cline implementa el endpoint PHP (Controller → Service → Repository)
4. Cline genera tests Jest para el componente
5. Cline genera tests PHPUnit para el endpoint
6. Developer revisa y hace merge
7. Memory Bank actualizado con nuevos patrones
```

### Caso 2: Resolución de Bug
```
Escenario: Error en formulario de registro de usuarios
──────────────────────────────────────────────────────────
1. MCP Remedy → Cline obtiene detalle del ticket
2. Cline analiza el componente React afectado
3. Cline analiza el endpoint PHP relacionado
4. Graph DB → Cline entiende dependencias del componente
5. Cline propone el fix con tests de regresión
6. Developer valida y hace merge
7. MCP Remedy → worklog actualizado
```

### Caso 3: Refactorización de Componente Legacy
```
Escenario: Migrar class component a functional component con hooks
──────────────────────────────────────────────────────────────────
1. Cline analiza el class component existente
2. Agente de Conceptualización documenta la funcionalidad actual
3. Cline refactoriza a functional component con hooks
   (siguiendo reglas Darwin)
4. Cline genera tests Jest equivalentes
5. Developer valida equivalencia funcional
```

---

## 6. Riesgos Específicos del Piloto Darwin

| Riesgo | Probabilidad | Impacto | Mitigación |
|--------|-------------|---------|------------|
| Variedad de versiones PHP y React en proyectos | Alta | Medio | Reglas Cline adaptables por proyecto |
| Deuda técnica elevada en proyectos legacy | Alta | Medio | Empezar con proyectos nuevos o módulos aislados |
| Resistencia si ya usan GitHub Copilot | Media | Medio | Mostrar valor diferencial (MCP, Memory Banks, SDD) |
| Complejidad de indexar codebase PHP legacy en Vector DB | Media | Bajo | Indexación incremental, empezar por módulos activos |