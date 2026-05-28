# 🔧 Componentes Core del Ecosistema

## 1. CLINE — Agente de Codificación Central

### 1.1 Descripción
Cline es el **agente de codificación principal** del ecosistema. Opera dentro del IDE (VS Code) y tiene capacidad para leer, escribir y ejecutar código, así como interactuar con sistemas externos a través de MCP servers.

### 1.2 Capacidades Nativas
- Lectura y escritura de archivos del proyecto
- Ejecución de comandos en terminal
- Navegación y comprensión del codebase
- Interacción con MCP servers
- Aplicación de reglas y estándares (`.clinerules`)
- Gestión de Memory Banks

### 1.3 Skills por Tecnología
Cline se especializa por tecnología mediante la carga de **skills específicos** que incluyen:

```
SKILL SAP
├── Conocimiento de ABAP (sintaxis, patrones, best practices)
├── Conocimiento de Fiori/UI5
├── Conocimiento de BTP (Cloud Foundry, CAPM, RAP)
├── Estándares de naming SAP
├── Patrones de integración SAP
└── Acceso a MCP SAP

SKILL MICROSOFT
├── Conocimiento de .NET / C# / Azure
├── Conocimiento de Power Platform
├── Patrones de arquitectura Azure
├── Estándares de naming Microsoft
└── Acceso a MCP Microsoft

SKILL MULESOFT
├── Conocimiento de Mule 4 / DataWeave
├── Patrones de integración (EIP)
├── Anypoint Platform best practices
├── Estándares de API design
└── Acceso a MCP MuleSoft

SKILL DARWIN
├── Conocimiento de React (hooks, context, patterns)
├── Conocimiento de PHP (Laravel/Symfony)
├── Patrones de arquitectura frontend/backend
├── Estándares de API REST
└── Acceso a MCP Darwin
```

### 1.4 Reglas Cline (`.clinerules`)
Cada tecnología tiene su propio conjunto de reglas que Cline aplica automáticamente:

```
.clinerules/
├── global.md          ← Reglas globales (seguridad, documentación, git)
├── sap.md             ← Estándares SAP (naming, modularidad, performance)
├── microsoft.md       ← Estándares Microsoft (.NET, Azure, naming)
├── mulesoft.md        ← Estándares MuleSoft (API design, error handling)
└── darwin.md          ← Estándares Darwin (React patterns, PHP conventions)
```

### 1.5 Libros Blancos por Tecnología
Complementan las reglas con guías de desarrollo completas:

| Libro Blanco | Contenido |
|--------------|-----------|
| **Libro Blanco SAP** | Guía de desarrollo ABAP, Fiori, BTP; patrones de integración; estándares de calidad |
| **Libro Blanco Microsoft** | Guía .NET/Azure; arquitectura de microservicios; DevOps practices |
| **Libro Blanco MuleSoft** | API-led connectivity; patrones de integración; error handling; logging |
| **Libro Blanco Darwin** | React architecture; PHP best practices; API design; testing strategy |

---

## 2. Memory Banks — Gestión del Conocimiento por Proyecto

### 2.1 Descripción
Los Memory Banks son **repositorios de conocimiento estructurado** específicos de cada proyecto. Permiten a Cline y los demás agentes operar con contexto completo del proyecto, sin necesidad de re-descubrir información ya conocida.

### 2.2 Estructura de un Memory Bank

```
memory-bank/
├── projectbrief.md        ← Qué es el proyecto, objetivos, alcance
├── productContext.md      ← Por qué existe, problemas que resuelve, UX goals
├── systemPatterns.md      ← Arquitectura, patrones de diseño, decisiones técnicas
├── techContext.md         ← Stack tecnológico, dependencias, entorno de desarrollo
├── activeContext.md       ← Estado actual, trabajo en curso, próximos pasos
└── progress.md            ← Qué funciona, qué falta, estado del proyecto
```

### 2.3 Ciclo de Vida del Memory Bank

```
INICIALIZACIÓN                    MANTENIMIENTO                    CONSULTA
──────────────                    ─────────────                    ────────
• Al inicio del proyecto          • Tras cada sesión de trabajo    • Al inicio de cada tarea
• Cline lee toda la               • Cline actualiza archivos       • Cline carga el contexto
  documentación disponible          relevantes con nuevas           completo del proyecto
• Genera los archivos base          decisiones y patrones         • Agentes consultan para
  del memory bank                 • Developer revisa y valida       generar specs contextuales
```

### 2.4 Beneficios
- **Continuidad**: El contexto persiste entre sesiones
- **Consistencia**: Todos los agentes trabajan con la misma información
- **Onboarding**: Nuevos desarrolladores se ponen al día rápidamente
- **Trazabilidad**: Las decisiones técnicas quedan documentadas

---

## 3. Vector Database — Base de Conocimiento Semántica

### 3.1 Descripción
La Vector DB almacena **representaciones semánticas** (embeddings) de documentación, código, specs y otros artefactos del proyecto. Permite búsquedas por similitud semántica, no solo por palabras clave.

### 3.2 Tecnología Seleccionada: Aurora RDS + pgvector ✅

**Decisión**: Se utilizará **Amazon Aurora PostgreSQL** con la extensión **pgvector** como base de conocimiento vectorial.

| Atributo | Detalle |
|----------|---------|
| **Motor** | Amazon Aurora PostgreSQL (Serverless v2 recomendado) |
| **Extensión vectorial** | pgvector — búsqueda por similitud coseno, L2 y producto interno |
| **Ventajas** | SQL familiar, integración nativa con AWS, sin infraestructura adicional, misma BD para datos relacionales y vectoriales |
| **Escalabilidad** | Aurora Serverless v2 escala automáticamente según demanda |
| **Alta disponibilidad** | Multi-AZ nativo en Aurora |
| **Seguridad** | IAM authentication, VPC, encryption at rest y in transit |
| **Índices vectoriales** | IVFFlat e HNSW soportados por pgvector |

**Justificación de la elección**:
- Reutiliza infraestructura AWS ya existente
- Elimina la necesidad de gestionar un servicio vectorial separado
- SQL estándar para consultas híbridas (vectorial + relacional)
- Integración directa con el ecosistema AWS (IAM, VPC, CloudWatch)
- Menor coste operativo al consolidar en un único servicio de BD

**Otras tecnologías evaluadas** (descartadas):

| Tecnología | Motivo de descarte |
|------------|-------------------|
| Qdrant | Requiere infraestructura adicional separada |
| Weaviate | Mayor complejidad operativa |
| Pinecone | Coste elevado, vendor lock-in externo |

### 3.3 Contenido Indexado

```
VECTOR DB — CONTENIDO
├── Documentación técnica del sistema
│   ├── Manuales de usuario
│   ├── Documentación de APIs
│   └── Guías de arquitectura
├── Código fuente (fragmentos relevantes)
│   ├── Funciones y clases clave
│   ├── Patrones de implementación
│   └── Ejemplos de uso
├── Especificaciones (OpenSpec)
│   ├── Specs funcionales
│   ├── Specs técnicas
│   └── Specs de API
├── Tickets y resoluciones (Remedy)
│   ├── Incidencias resueltas
│   ├── Patrones de error conocidos
│   └── Soluciones aplicadas
└── Memory Banks de proyectos
    └── Decisiones y contexto histórico
```

### 3.4 Acceso vía MCP
El MCP Vector DB expone las siguientes operaciones:
- `search(query, top_k, filters)` — Búsqueda semántica
- `upsert(documents)` — Indexar nuevos documentos
- `delete(ids)` — Eliminar documentos obsoletos
- `get_similar(document_id, top_k)` — Encontrar documentos similares

---

## 4. Graph Database — Base de Relaciones

### 4.1 Descripción
La Graph DB modela las **relaciones complejas** entre entidades del sistema: módulos, funciones, datos, dependencias, equipos, tickets, etc. Permite responder preguntas como "¿qué módulos se ven afectados si cambio esta función?" o "¿qué equipos trabajan en componentes relacionados?".

### 4.2 Tecnologías Candidatas

| Tecnología | Características | Caso de Uso Ideal |
|------------|-----------------|-------------------|
| **Amazon Neptune** | Managed, compatible con Gremlin y SPARQL, integración AWS nativa | AWS, escalabilidad, alta disponibilidad |
| **IBM Context Studio** | Plataforma de gestión de contexto y conocimiento con capacidades de grafo, integración con ecosistema IBM/watsonx | Gestión de conocimiento empresarial, contexto IA, integración con herramientas IBM |

### 4.3 Modelo de Grafo

```
NODOS (Entidades)
├── :Module          → Módulo de software
├── :Function        → Función o método
├── :DataEntity      → Entidad de datos (tabla, objeto)
├── :API             → Endpoint de API
├── :Team            → Equipo de desarrollo
├── :Developer       → Desarrollador individual
├── :Ticket          → Ticket de Remedy
├── :Spec            → Especificación OpenSpec
└── :Deployment      → Despliegue en entorno

RELACIONES (Edges)
├── :DEPENDS_ON      → Módulo depende de otro módulo
├── :CALLS           → Función llama a otra función
├── :READS           → Módulo lee entidad de datos
├── :WRITES          → Módulo escribe entidad de datos
├── :EXPOSES         → Módulo expone API
├── :OWNED_BY        → Módulo pertenece a equipo
├── :DEVELOPED_BY    → Función desarrollada por developer
├── :RESOLVES        → Spec resuelve ticket
└── :DEPLOYED_IN     → Módulo desplegado en entorno
```

### 4.4 Casos de Uso

| Consulta | Valor |
|----------|-------|
| Análisis de impacto de cambios | "¿Qué se rompe si modifico X?" |
| Detección de dependencias circulares | Identificar deuda técnica |
| Mapa de propiedad del código | "¿Quién es responsable de X?" |
| Trazabilidad ticket → código | "¿Qué código resuelve este ticket?" |
| Análisis de acoplamiento | Identificar módulos muy acoplados |

---

## 5. Capa de Integración MCP — Model Context Protocol

### 5.1 Descripción
El **Model Context Protocol (MCP)** es el protocolo estándar que permite a Cline y los agentes interactuar con sistemas externos de forma segura y estructurada. Cada sistema tiene su propio MCP Server que actúa como proxy.

### 5.2 Arquitectura MCP

```
CLINE / AGENTES
      │
      │ MCP Protocol (JSON-RPC over stdio/SSE)
      │
┌─────▼──────────────────────────────────────────────┐
│                  MCP SERVERS                        │
│                                                     │
│  ┌──────────┐  ┌──────────┐  ┌──────────┐          │
│  │ MCP SAP  │  │ MCP MSFT │  │ MCP Mule │  ...     │
│  └────┬─────┘  └────┬─────┘  └────┬─────┘          │
└───────┼─────────────┼─────────────┼────────────────┘
        │             │             │
   [SAP APIs]   [Azure APIs]  [Anypoint APIs]
```

### 5.3 Catálogo de MCP Servers

#### MCP SAP
- **Propósito**: Acceso al ecosistema SAP desde Cline
- **Capacidades**: Explorar repositorio ABAP, leer/escribir objetos de desarrollo, ejecutar transacciones, consultar datos de negocio, acceder a BTP
- **Autenticación**: OAuth 2.0 / SAP BTP credentials

> **Opciones a analizar para el MCP SAP:**
>
> | Opción | Descripción | Referencia |
> |--------|-------------|------------|
> | **ABAP Remote Filesystem** | MCP server que expone el sistema de ficheros ABAP remoto, permitiendo a Cline navegar y leer objetos ABAP directamente como si fueran archivos locales | A evaluar durante la Etapa 1 |
> | **AWS for SAP MCP Server** | MCP server oficial de AWS para integración con sistemas SAP, con soporte para operaciones SAP a través de la infraestructura AWS | [Documentación oficial](https://docs.aws.amazon.com/mcp-sap/latest/awsforsapmcp/introduction.html) |

#### MCP Microsoft
- **Propósito**: Integración con el ecosistema Microsoft
- **Capacidades**: Azure DevOps (work items, repos, pipelines), Microsoft Graph (usuarios, SharePoint, Teams), Azure Resource Manager
- **Autenticación**: Azure AD / Service Principal

#### MCP MuleSoft
- **Propósito**: Gestión de la plataforma Anypoint
- **Capacidades**: Explorar APIs, gestionar flows, consultar conectores, ver deployments, acceder a Exchange
- **Autenticación**: Anypoint Platform credentials

#### MCP Remedy
- **Propósito**: Acceso al sistema ITSM
- **Capacidades**: Consultar tickets, crear/actualizar incidencias, gestionar cambios, ver problemas, obtener historial
- **Autenticación**: Remedy API credentials

#### MCP Vector DB
- **Propósito**: Acceso a la base de conocimiento semántica
- **Capacidades**: Búsqueda semántica, indexación de documentos, gestión de colecciones
- **Autenticación**: API Key

#### MCP Graph DB
- **Propósito**: Consultas sobre el grafo de relaciones
- **Capacidades**: Consultas Cypher/Gremlin, análisis de impacto, exploración de dependencias
- **Autenticación**: Database credentials

---

## 6. Agentes Especializados

### 6.1 Agente de Conceptualización
- **Rol**: Transforma necesidades de negocio en conceptos técnicos estructurados
- **Input**: Descripción en lenguaje natural de la necesidad
- **Output**: Concept Brief (problema, solución propuesta, alcance, restricciones, criterios de éxito)
- **Herramientas**: Memory Banks, Vector DB (para contexto histórico)

### 6.2 Agentes OpenSpec
Suite de agentes que generan especificaciones formales:

| Agente | Output |
|--------|--------|
| **Spec Funcional** | Historias de usuario, criterios de aceptación, flujos de negocio |
| **Spec Técnica** | Diseño de solución, componentes, interfaces, modelo de datos |
| **Spec de API** | OpenAPI/Swagger, contratos de integración |
| **Spec de Testing** | Casos de prueba, escenarios de aceptación |

### 6.3 Agente de Estimación
- **Rol**: Estima el esfuerzo de desarrollo basándose en la spec
- **Input**: Spec completa (funcional + técnica)
- **Output**: Estimación por componente, total, riesgos, supuestos
- **Metodología**: Story points + horas, con rangos de confianza

### 6.4 Agente de Revisión / Challenge
- **Rol**: Valida y cuestiona specs y estimaciones para mejorar su calidad
- **Input**: Spec + Estimación
- **Output**: Lista de observaciones, preguntas abiertas, riesgos identificados, sugerencias de mejora
- **Perspectiva**: Actúa como "abogado del diablo" constructivo

### 6.5 Agente de Testing
- **Rol**: Genera y ejecuta casos de prueba basados en la spec
- **Input**: Spec de testing + código implementado
- **Output**: Tests unitarios, de integración, de aceptación; reporte de cobertura