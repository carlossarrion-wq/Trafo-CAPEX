# 🔷 Plan Piloto — Equipo SAP

## 1. Contexto del Piloto SAP

### 1.1 Descripción del Equipo
El equipo piloto SAP es el primer equipo de desarrollo SAP en adoptar el ecosistema de desarrollo aumentado por IA. Su experiencia servirá de referencia para el resto de equipos SAP de la organización.

### 1.2 Stack Tecnológico del Equipo

| Tecnología | Descripción |
|------------|-------------|
| **ABAP** | Lenguaje principal de desarrollo SAP |
| **SAP Fiori / UI5** | Desarrollo de interfaces de usuario |
| **SAP BTP** | Business Technology Platform (Cloud) |
| **S/4HANA** | Sistema ERP principal |
| **SAP Transport System** | Gestión de cambios y transportes |

### 1.3 Información del Equipo

| Campo | Valor |
|-------|-------|
| **Nombre del equipo** | [Por definir] |
| **Tech Lead** | [Por definir] |
| **Número de developers** | [Por definir] |
| **Proyectos activos** | [Por definir] |
| **Fecha de inicio del piloto** | [Por definir] |

---

## 2. Componentes del Ecosistema para SAP

### 2.1 MCP SAP — Capacidades Específicas

El MCP SAP proporciona a Cline acceso directo al ecosistema SAP:

```
MCP SAP — HERRAMIENTAS DISPONIBLES
├── sap_search_object      → Buscar objetos ABAP (programas, FMs, clases)
├── sap_read_program       → Leer código fuente de programas
├── sap_read_function      → Leer módulos de función
├── sap_read_class         → Leer clases ABAP (OO)
├── sap_read_table         → Leer estructura de tablas
├── sap_get_transport      → Consultar órdenes de transporte
├── sap_list_packages      → Listar paquetes de desarrollo
├── sap_btp_list_apps      → Listar apps en BTP
├── sap_fiori_get_app      → Obtener info de apps Fiori
└── sap_get_api_spec       → Obtener specs de APIs SAP
```

### 2.2 Reglas Cline para SAP (`.clinerules/sap.md`)

Las reglas Cline para SAP incluyen:

```
ESTÁNDARES SAP — RESUMEN
├── NAMING CONVENTIONS
│   ├── Programas: Z[ÁREA][DESCRIPCIÓN] (ej: ZFIMM_PEDIDOS)
│   ├── Módulos de función: Z_[ÁREA]_[DESCRIPCIÓN]
│   ├── Clases: ZCL_[ÁREA]_[DESCRIPCIÓN]
│   ├── Interfaces: ZIF_[ÁREA]_[DESCRIPCIÓN]
│   └── Tablas: Z[ÁREA][DESCRIPCIÓN] (ej: ZFIMM_PEDIDOS)
│
├── DESARROLLO ABAP
│   ├── Preferir ABAP OO sobre programación procedural
│   ├── Usar SELECT con campos específicos (no SELECT *)
│   ├── Evitar SELECT dentro de bucles (N+1 problem)
│   ├── Usar tipos internos (TYPE TABLE OF) correctamente
│   └── Documentar con comentarios ABAP Doc
│
├── MODULARIDAD
│   ├── Separar lógica de negocio de presentación
│   ├── Usar patrones MVC en Fiori
│   ├── Crear módulos de función reutilizables
│   └── Evitar código duplicado (DRY principle)
│
└── TESTING
    ├── Crear ABAP Unit tests para lógica de negocio
    ├── Cobertura mínima del 70%
    └── Tests independientes del sistema (mocks)
```

### 2.3 Libro Blanco SAP

El Libro Blanco SAP cubre:
- Guía de desarrollo ABAP moderno (Clean ABAP)
- Patrones de desarrollo Fiori/UI5
- Guía de desarrollo en BTP (CAPM, RAP)
- Patrones de integración SAP (RFC, BAPI, OData, REST)
- Estándares de calidad y performance
- Guía de testing en SAP

### 2.4 Memory Bank SAP

Estructura específica para proyectos SAP:
```
memory-bank/
├── projectbrief.md
├── productContext.md
├── systemPatterns.md
├── techContext.md
├── activeContext.md
├── progress.md
├── sap_landscape.md       ← Landscape DEV/QAS/PRD, sistemas, clientes
├── sap_objects.md         ← Inventario de objetos ABAP del proyecto
├── sap_customizing.md     ← Configuración de customizing relevante
└── sap_transports.md      ← Historial de transportes importantes
```

---

## 3. Plan de Adopción — 3 Meses

### 3.1 Mes 1: Arranque y Adopción Básica

#### Semana 1-2: Onboarding SAP
- [ ] Formación: Introducción al Ecosistema (2h)
- [ ] Formación: Cline Básico (4h)
- [ ] Formación: Memory Banks (2h)
- [ ] Configuración de VS Code + Cline en cada máquina
- [ ] Configuración del MCP SAP (conexión al sistema DEV)
- [ ] Configuración del MCP Remedy
- [ ] Primera sesión práctica: explorar código SAP existente con Cline

#### Semana 3-4: Primeros Casos Reales SAP
- [ ] Usar Cline para entender un programa ABAP complejo existente
- [ ] Usar MCP SAP para buscar objetos relacionados
- [ ] Crear el Memory Bank del primer proyecto piloto
- [ ] Usar Cline para resolver una incidencia menor con contexto de Remedy
- [ ] Documentar primeras impresiones y ajustes necesarios

**Hito Mes 1**: Todos los developers han usado Cline en al menos 3 tareas reales

### 3.2 Mes 2: Adopción del Flujo SDD

#### Semana 5-6: Spec Driven Development SAP
- [ ] Formación: Spec Driven Development (4h)
- [ ] Formación: Agentes OpenSpec (3h)
- [ ] Primer Concept Brief generado con el Agente de Conceptualización
- [ ] Primera Functional Spec generada con agentes OpenSpec
- [ ] Primera Technical Spec SAP (con patrones ABAP)
- [ ] Primera estimación con el Agente de Estimación

#### Semana 7-8: Flujo Completo con MCP
- [ ] Flujo SDD completo en un feature real (spec → código → test)
- [ ] Uso activo de MCP SAP durante la codificación
- [ ] Uso activo de MCP Remedy para vincular código con tickets
- [ ] Primer ABAP Unit test generado por Cline
- [ ] Actualización del Memory Bank con decisiones del sprint

**Hito Mes 2**: Al menos 2 features desarrollados con el flujo SDD completo

### 3.3 Mes 3: Consolidación y Medición

#### Semana 9-10: Autonomía SAP
- [ ] Equipo opera el flujo SDD sin soporte constante
- [ ] Memory Banks actualizados y enriquecidos
- [ ] Vector DB con documentación SAP del proyecto indexada
- [ ] Graph DB con relaciones de módulos SAP modeladas

#### Semana 11-12: Medición y Cierre del Piloto
- [ ] Medición de KPIs (ver sección 4)
- [ ] Encuesta de satisfacción al equipo
- [ ] Documentación de lecciones aprendidas
- [ ] Presentación de resultados al Sponsor
- [ ] Identificación del "champion" SAP para la expansión

**Hito Mes 3**: KPIs de éxito alcanzados, equipo autónomo

---

## 4. KPIs del Piloto SAP

| KPI | Baseline | Objetivo Mes 1 | Objetivo Mes 2 | Objetivo Mes 3 |
|-----|---------|---------------|---------------|---------------|
| % developers usando Cline | 0% | > 80% | > 90% | > 95% |
| % features con spec previa | 0% | 20% | 60% | > 80% |
| Tiempo medio en entender código legacy | [baseline] | -10% | -25% | -40% |
| Tiempo medio en resolver incidencias | [baseline] | -5% | -20% | -35% |
| Cobertura de ABAP Unit tests | [baseline] | +5% | +15% | +25% |
| NPS del equipo | — | — | — | > 40 |

---

## 5. Casos de Uso Prioritarios para el Piloto SAP

### Caso 1: Desarrollo de Nueva Funcionalidad ABAP
```
Escenario: Crear un nuevo report ABAP para análisis de datos
─────────────────────────────────────────────────────────────
1. Developer describe la necesidad al Agente de Conceptualización
2. Agente genera Concept Brief con contexto SAP
3. Agentes OpenSpec generan Functional + Technical Spec
   (consultando Memory Bank y Vector DB para patrones SAP)
4. Cline implementa el report siguiendo reglas SAP
   (usando MCP SAP para verificar tablas y estructuras)
5. Cline genera ABAP Unit tests
6. Developer revisa y aprueba
7. Memory Bank se actualiza con el nuevo patrón
```

### Caso 2: Resolución de Incidencia SAP
```
Escenario: Error en proceso de facturación
─────────────────────────────────────────────────────────────
1. Developer consulta MCP Remedy → obtiene detalle del ticket
2. Cline analiza el error con contexto del ticket
3. MCP SAP → Cline lee el programa afectado
4. Graph DB → Cline entiende qué otros módulos pueden verse afectados
5. Cline propone el fix siguiendo estándares SAP
6. Developer valida y aprueba
7. Cline implementa y genera documentación del fix
8. MCP Remedy → worklog actualizado automáticamente
```

### Caso 3: Desarrollo de App Fiori
```
Escenario: Nueva app Fiori para aprobación de pedidos
─────────────────────────────────────────────────────────────
1. Agentes OpenSpec generan spec de la app (UI + backend OData)
2. Cline implementa el servicio OData en ABAP
   (usando MCP SAP para verificar entidades de datos)
3. Cline implementa la app Fiori/UI5
   (siguiendo patrones del Libro Blanco SAP)
4. Cline genera tests de la app
5. Developer revisa y despliega en BTP
```

---

## 6. Riesgos Específicos del Piloto SAP

| Riesgo | Probabilidad | Impacto | Mitigación |
|--------|-------------|---------|------------|
| Restricciones de acceso al sistema SAP DEV | Media | Alto | Configurar usuario técnico con permisos adecuados |
| Complejidad del MCP SAP (APIs SAP) | Alta | Medio | Prototipo temprano, empezar con lectura antes que escritura |
| Resistencia por parte de developers ABAP senior | Media | Alto | Involucrar al Tech Lead como embajador, mostrar valor rápido |
| Curva de aprendizaje de Clean ABAP | Media | Medio | Formación específica, ejemplos concretos en el Libro Blanco |
| Latencia en consultas al sistema SAP | Baja | Bajo | Caché local para objetos frecuentemente consultados |

---

## 7. Configuración Técnica del Piloto SAP

### 7.1 Configuración de Cline para SAP

```json
// .vscode/settings.json (configuración del proyecto SAP)
{
  "cline.mcpServers": {
    "sap": {
      "command": "node",
      "args": ["./mcp-servers/sap/index.js"],
      "env": {
        "SAP_HOST": "${env:SAP_DEV_HOST}",
        "SAP_CLIENT": "100",
        "SAP_USER": "${env:SAP_DEV_USER}",
        "SAP_PASSWORD": "${env:SAP_DEV_PASSWORD}"
      }
    },
    "remedy": {
      "command": "node",
      "args": ["./mcp-servers/remedy/index.js"],
      "env": {
        "REMEDY_HOST": "${env:REMEDY_HOST}",
        "REMEDY_USER": "${env:REMEDY_USER}",
        "REMEDY_PASSWORD": "${env:REMEDY_PASSWORD}"
      }
    },
    "vector-db": {
      "command": "node",
      "args": ["./mcp-servers/vector-db/index.js"],
      "env": {
        "QDRANT_URL": "${env:QDRANT_URL}",
        "QDRANT_API_KEY": "${env:QDRANT_API_KEY}"
      }
    }
  }
}
```

### 7.2 Estructura de Carpetas del Proyecto SAP

```
proyecto-sap-piloto/
├── .clinerules            ← Reglas Cline (symlink a global + sap)
├── memory-bank/           ← Memory Bank del proyecto
├── specs/                 ← Especificaciones OpenSpec
│   ├── functional/
│   ├── technical/
│   └── test/
├── src/                   ← Código ABAP (exportado del sistema)
└── docs/                  ← Documentación adicional