# 🔌 Catálogo de Integraciones MCP

## 1. Introducción al Model Context Protocol (MCP)

El **Model Context Protocol (MCP)** es un protocolo abierto que estandariza la forma en que los agentes de IA (como Cline) se conectan con herramientas y fuentes de datos externas. Funciona como una capa de abstracción que permite a Cline interactuar con cualquier sistema a través de una interfaz uniforme.

### 1.1 Arquitectura MCP

```
┌─────────────────────────────────────────────────────────────┐
│                    CLINE (MCP Client)                        │
│                                                             │
│  • Descubre herramientas disponibles en cada MCP Server     │
│  • Invoca herramientas con parámetros estructurados         │
│  • Recibe resultados y los incorpora al contexto            │
└──────────────────────────┬──────────────────────────────────┘
                           │ MCP Protocol
          ┌────────────────┼────────────────┐
          │                │                │
   ┌──────▼──────┐  ┌──────▼──────┐  ┌──────▼──────┐
   │  MCP Server │  │  MCP Server │  │  MCP Server │
   │    (SAP)    │  │  (Remedy)   │  │  (VectorDB) │
   └──────┬──────┘  └──────┬──────┘  └──────┬──────┘
          │                │                │
     [SAP APIs]      [Remedy REST]    [Qdrant API]
```

### 1.2 Tipos de Capacidades MCP

| Tipo | Descripción | Ejemplo |
|------|-------------|---------|
| **Tools** | Acciones que el agente puede ejecutar | `create_ticket`, `search_code` |
| **Resources** | Datos que el agente puede leer | `project_documentation`, `api_spec` |
| **Prompts** | Plantillas de prompts reutilizables | `review_spec_template` |

---

## 2. MCP SAP

### 2.1 Descripción
Servidor MCP que proporciona acceso al ecosistema SAP, incluyendo S/4HANA, BTP y herramientas de desarrollo ABAP.

### 2.2 Herramientas (Tools)

| Tool | Descripción | Parámetros |
|------|-------------|------------|
| `sap_search_object` | Busca objetos de desarrollo ABAP | `object_name`, `object_type`, `package` |
| `sap_read_program` | Lee el código fuente de un programa ABAP | `program_name`, `include` |
| `sap_read_function` | Lee el código de un módulo de función | `function_name`, `function_group` |
| `sap_read_class` | Lee una clase ABAP | `class_name` |
| `sap_read_table` | Lee la estructura de una tabla | `table_name` |
| `sap_execute_report` | Ejecuta un report en modo análisis | `report_name`, `parameters` |
| `sap_get_transport` | Obtiene info de una orden de transporte | `transport_number` |
| `sap_list_packages` | Lista paquetes de desarrollo | `prefix`, `application_component` |
| `sap_btp_list_apps` | Lista aplicaciones en BTP | `space`, `org` |
| `sap_fiori_get_app` | Obtiene info de una app Fiori | `app_id` |
| `sap_get_api_spec` | Obtiene spec de una API SAP | `api_name`, `version` |

### 2.3 Recursos (Resources)

| Resource | Descripción |
|----------|-------------|
| `sap://development-standards` | Estándares de desarrollo SAP de la organización |
| `sap://naming-conventions` | Convenciones de naming por tipo de objeto |
| `sap://architecture-patterns` | Patrones de arquitectura SAP aprobados |
| `sap://transport-landscape` | Descripción del landscape de transportes |

### 2.4 Casos de Uso

```
CASO 1: Cline desarrolla una nueva función ABAP
  → sap_search_object: busca funciones similares existentes
  → sap_read_function: lee implementaciones de referencia
  → sap_read_table: entiende la estructura de datos
  → Genera código siguiendo los patrones encontrados

CASO 2: Cline resuelve una incidencia SAP
  → sap_read_program: lee el programa con el error
  → sap_read_table: verifica la estructura de datos afectada
  → sap_get_transport: verifica cambios recientes relacionados
  → Propone y aplica el fix
```

### 2.5 Configuración

```json
{
  "mcpServers": {
    "sap": {
      "command": "node",
      "args": ["./mcp-servers/sap/index.js"],
      "env": {
        "SAP_HOST": "${SAP_HOST}",
        "SAP_CLIENT": "${SAP_CLIENT}",
        "SAP_USER": "${SAP_USER}",
        "SAP_PASSWORD": "${SAP_PASSWORD}",
        "BTP_CLIENT_ID": "${BTP_CLIENT_ID}",
        "BTP_CLIENT_SECRET": "${BTP_CLIENT_SECRET}"
      }
    }
  }
}
```

---

## 3. MCP Microsoft

### 3.1 Descripción
Servidor MCP que integra el ecosistema Microsoft: Azure DevOps, Microsoft Graph API, Azure Resource Manager y Power Platform.

### 3.2 Herramientas (Tools)

#### Azure DevOps
| Tool | Descripción | Parámetros |
|------|-------------|------------|
| `ado_get_workitem` | Obtiene un work item por ID | `id`, `project` |
| `ado_search_workitems` | Busca work items por criterios | `query`, `project`, `type` |
| `ado_create_workitem` | Crea un nuevo work item | `type`, `title`, `description`, `project` |
| `ado_get_repo` | Obtiene info de un repositorio | `repo_name`, `project` |
| `ado_get_file` | Lee un archivo del repositorio | `repo`, `path`, `branch` |
| `ado_list_pipelines` | Lista pipelines de CI/CD | `project`, `folder` |
| `ado_get_pipeline_run` | Obtiene resultado de una ejecución | `pipeline_id`, `run_id` |

#### Microsoft Graph
| Tool | Descripción | Parámetros |
|------|-------------|------------|
| `graph_get_user` | Obtiene info de un usuario | `user_id_or_email` |
| `graph_search_sharepoint` | Busca en SharePoint | `query`, `site_id` |
| `graph_get_teams_channel` | Obtiene mensajes de un canal Teams | `team_id`, `channel_id` |

### 3.3 Casos de Uso

```
CASO 1: Cline trabaja en una historia de usuario
  → ado_get_workitem: obtiene los criterios de aceptación
  → ado_get_file: lee el código existente relacionado
  → Implementa la funcionalidad según los criterios
  → ado_create_workitem: crea sub-tareas si es necesario

CASO 2: Cline investiga un bug reportado
  → ado_search_workitems: busca bugs similares resueltos
  → ado_get_pipeline_run: verifica si hay fallos en CI/CD
  → graph_search_sharepoint: busca documentación relacionada
```

---

## 4. MCP MuleSoft

### 4.1 Descripción
Servidor MCP que proporciona acceso a Anypoint Platform para gestión de APIs, integraciones y deployments MuleSoft.

### 4.2 Herramientas (Tools)

| Tool | Descripción | Parámetros |
|------|-------------|------------|
| `mule_list_apis` | Lista APIs en Anypoint Exchange | `organization`, `search_term` |
| `mule_get_api_spec` | Obtiene la spec RAML/OAS de una API | `api_id`, `version` |
| `mule_get_flow` | Obtiene el XML de un flow Mule | `app_name`, `flow_name` |
| `mule_list_connectors` | Lista conectores disponibles | `category`, `search_term` |
| `mule_get_deployment` | Obtiene info de un deployment | `app_name`, `environment` |
| `mule_list_environments` | Lista entornos disponibles | `organization` |
| `mule_get_app_logs` | Obtiene logs de una aplicación | `app_name`, `environment`, `lines` |
| `mule_search_exchange` | Busca assets en Exchange | `query`, `type` |

### 4.3 Casos de Uso

```
CASO 1: Cline desarrolla una nueva integración
  → mule_list_apis: busca APIs existentes que puede reutilizar
  → mule_get_api_spec: lee los contratos de las APIs a integrar
  → mule_list_connectors: verifica conectores disponibles
  → Genera el flow Mule siguiendo los patrones del libro blanco

CASO 2: Cline diagnostica un error en producción
  → mule_get_app_logs: obtiene los logs del error
  → mule_get_flow: lee el flow afectado
  → mule_get_deployment: verifica la versión desplegada
  → Propone el fix
```

---

## 5. MCP Remedy

### 5.1 Descripción
Servidor MCP que integra BMC Remedy (o equivalente ITSM) para acceso a tickets, incidencias, cambios y problemas directamente desde el entorno de desarrollo.

### 5.2 Herramientas (Tools)

| Tool | Descripción | Parámetros |
|------|-------------|------------|
| `remedy_get_ticket` | Obtiene detalle completo de un ticket | `ticket_id` |
| `remedy_search_tickets` | Busca tickets por criterios | `query`, `status`, `priority`, `assignee` |
| `remedy_get_incident` | Obtiene una incidencia | `incident_id` |
| `remedy_search_incidents` | Busca incidencias | `query`, `status`, `category`, `date_from` |
| `remedy_get_change` | Obtiene una solicitud de cambio | `change_id` |
| `remedy_create_worklog` | Añade una nota de trabajo | `ticket_id`, `notes`, `time_spent` |
| `remedy_update_status` | Actualiza el estado de un ticket | `ticket_id`, `status`, `notes` |
| `remedy_get_problem` | Obtiene un registro de problema | `problem_id` |
| `remedy_search_known_errors` | Busca errores conocidos | `query`, `category` |
| `remedy_get_sla` | Obtiene info de SLA de un ticket | `ticket_id` |

### 5.3 Recursos (Resources)

| Resource | Descripción |
|----------|-------------|
| `remedy://my-tickets` | Tickets asignados al usuario actual |
| `remedy://team-tickets` | Tickets del equipo |
| `remedy://open-incidents` | Incidencias abiertas del sistema |

### 5.4 Casos de Uso

```
CASO 1: Developer trabaja en una incidencia
  → remedy_get_incident: obtiene descripción completa del problema
  → remedy_search_known_errors: busca si hay solución conocida
  → remedy_search_incidents: busca incidencias similares resueltas
  → Cline implementa la solución
  → remedy_create_worklog: registra el trabajo realizado
  → remedy_update_status: actualiza el estado del ticket

CASO 2: Planificación del sprint
  → remedy_search_tickets: obtiene tickets pendientes del equipo
  → remedy_get_sla: verifica prioridades por SLA
  → Cline ayuda a estimar y priorizar el trabajo
```

### 5.5 Valor Diferencial
La integración con Remedy elimina el **cambio de contexto** entre el sistema de tickets y el IDE. El desarrollador puede:
- Ver el detalle del ticket sin salir de VS Code
- Tener el contexto del problema mientras codifica
- Registrar el trabajo directamente desde el IDE
- Vincular automáticamente commits con tickets

---

## 6. MCP Vector Database

### 6.1 Descripción
Servidor MCP que proporciona acceso a la base de conocimiento semántica del proyecto, permitiendo búsquedas por similitud sobre documentación, código y especificaciones.

### 6.2 Herramientas (Tools)

| Tool | Descripción | Parámetros |
|------|-------------|------------|
| `vector_search` | Búsqueda semántica | `query`, `collection`, `top_k`, `filters` |
| `vector_upsert` | Indexa documentos | `documents`, `collection` |
| `vector_delete` | Elimina documentos | `ids`, `collection` |
| `vector_get_similar` | Encuentra documentos similares | `document_id`, `collection`, `top_k` |
| `vector_list_collections` | Lista colecciones disponibles | — |
| `vector_get_stats` | Estadísticas de una colección | `collection` |

### 6.3 Colecciones Estándar

| Colección | Contenido | Actualización |
|-----------|-----------|---------------|
| `documentation` | Documentación técnica del sistema | Manual / CI/CD |
| `codebase` | Fragmentos de código indexados | Automática (git hooks) |
| `specs` | Especificaciones OpenSpec | Automática (al aprobar spec) |
| `incidents` | Incidencias resueltas y soluciones | Automática (Remedy webhook) |
| `memory_banks` | Contenido de los Memory Banks | Automática (al actualizar) |

---

## 7. MCP Graph Database

### 7.1 Descripción
Servidor MCP que proporciona acceso a la base de datos de grafos para consultas sobre relaciones entre entidades del sistema.

### 7.2 Herramientas (Tools)

| Tool | Descripción | Parámetros |
|------|-------------|------------|
| `graph_query` | Ejecuta una consulta Cypher | `query`, `parameters` |
| `graph_get_node` | Obtiene un nodo por ID | `node_id`, `node_type` |
| `graph_get_neighbors` | Obtiene nodos relacionados | `node_id`, `relationship_type`, `depth` |
| `graph_impact_analysis` | Analiza impacto de un cambio | `node_id`, `change_type` |
| `graph_find_path` | Encuentra camino entre dos nodos | `from_node`, `to_node` |
| `graph_get_dependencies` | Obtiene árbol de dependencias | `module_name`, `direction` |
| `graph_upsert_node` | Crea o actualiza un nodo | `node_type`, `properties` |