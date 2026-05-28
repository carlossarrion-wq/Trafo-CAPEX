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
   │    (SAP)    │  │   (Jira)    │  │  (Microsoft)│
   └──────┬──────┘  └──────┬──────┘  └──────┬──────┘
          │                │                │
     [SAP APIs]      [Jira REST API]   [Azure DevOps]
```

### 1.2 Tipos de Capacidades MCP

| Tipo | Descripción | Ejemplo |
|------|-------------|---------|
| **Tools** | Acciones que el agente puede ejecutar | `create_ticket`, `search_code` |
| **Resources** | Datos que el agente puede leer | `project_documentation`, `api_spec` |
| **Prompts** | Plantillas de prompts reutilizables | `review_spec_template` |

---

## 2. Estado de los MCPs — Visión General

La estrategia de adopción de MCPs se divide en **3 horizontes** según su disponibilidad actual:

```
HORIZONTE 1 — PILOTO (Etapas 2.1 y 2.2)
─────────────────────────────────────────────────────────────────
  MCPs que YA EXISTEN y se pueden usar desde el primer día.
  Requieren selección, exploración y configuración.

  ✅ MCP SAP       → ABAP Remote Filesystem (existe, hay que seleccionar y configurar)
  ✅ MCP Microsoft → Azure DevOps MCP (existe, hay que seleccionar y configurar)
  ✅ MCP Jira      → Jira MCP oficial (existe, hay que configurar)

HORIZONTE 2 — USO MASIVO (Etapa 2.3)
─────────────────────────────────────────────────────────────────
  MCPs que HAY QUE CONSTRUIR en paralelo durante el piloto.
  Se incorporan cuando estén listos y validados.

  🔨 MCP Remedy    → A construir (API REST Remedy disponible)
  🔨 MCP MuleSoft  → A construir (Anypoint Platform API disponible)

HORIZONTE 3 — FUTURO (Post-piloto)
─────────────────────────────────────────────────────────────────
  MCPs que requieren decisiones de arquitectura adicionales
  o cuyo acceso se resuelve mejor por otras vías.

  🔲 MCP Vector DB → A construir (requiere infraestructura Aurora+pgvector)
  🔲 MCP Graph DB  → A construir (requiere decisión de plataforma)
  ➡️ Git/GitHub/GitLab → Acceso vía CLI del desarrollador (no MCP)
─────────────────────────────────────────────────────────────────
```

### Tabla Resumen de MCPs

| MCP | Sistema | Estado | Horizonte | Acción |
|-----|---------|--------|-----------|--------|
| **MCP SAP** | SAP S/4HANA / ABAP | ✅ Existe | H1 — Piloto | Seleccionar, explorar y configurar |
| **MCP Microsoft** | Azure DevOps | ✅ Existe | H1 — Piloto | Seleccionar, explorar y configurar |
| **MCP Jira** | Atlassian Jira | ✅ Existe | H1 — Piloto | Configurar |
| **MCP Remedy** | BMC Remedy / ITSM | 🔨 A construir | H2 — Uso Masivo | Construir durante el piloto |
| **MCP MuleSoft** | Anypoint Platform | 🔨 A construir | H2 — Uso Masivo | Construir durante el piloto |
| **MCP Vector DB** | Aurora RDS + pgvector | 🔲 A construir | H3 — Futuro | Requiere infraestructura previa |
| **MCP Graph DB** | Neo4j / Neptune | 🔲 A construir | H3 — Futuro | Requiere decisión de plataforma |
| **Git/GitHub/GitLab** | Repositorios Git | ➡️ Vía CLI | — | Acceso nativo por terminal del dev |

---

## 3. HORIZONTE 1 — MCPs Existentes (Piloto)

### 3.1 MCP SAP — ABAP Remote Filesystem

#### Estado: ✅ Existe — Seleccionar y configurar

**Descripción**: El servidor MCP **ABAP Remote Filesystem** permite a Cline acceder al repositorio de desarrollo SAP (S/4HANA, BTP) directamente desde VS Code. Es la opción más madura disponible para SAP.

**Referencia**: [ABAP Remote Filesystem MCP](https://github.com/mario-andreschak/mcp-abap-abap-adt-api)

**Capacidades principales (39 herramientas en 12 categorías)**:

| Categoría | Herramientas destacadas |
|-----------|------------------------|
| **Objetos ABAP** | Leer/escribir programas, clases, funciones, includes |
| **Navegación** | Buscar objetos, listar paquetes, explorar jerarquías |
| **Transportes** | Crear órdenes, añadir objetos, gestionar releases |
| **Activación** | Activar objetos de desarrollo |
| **Syntax Check** | Verificar sintaxis ABAP antes de activar |
| **Unit Tests** | Ejecutar tests ABAP Unit |
| **Code Completion** | Sugerencias de código en contexto SAP |
| **Where-Used** | Encontrar usos de un objeto en el sistema |
| **Documentación** | Leer/escribir documentación de objetos |
| **BTP/Fiori** | Acceso a apps Fiori y servicios BTP |

**Alternativa evaluada**: AWS for SAP MCP Server (https://docs.aws.amazon.com/mcp-sap/latest/awsforsapmcp/introduction.html)

**Acción requerida en Etapa 1**:
- [ ] Evaluar y seleccionar entre ABAP Remote Filesystem y AWS for SAP MCP
- [ ] Probar conectividad con el sistema SAP del equipo piloto
- [ ] Documentar configuración específica del entorno

**Configuración base**:
```json
{
  "mcpServers": {
    "abap-remote-filesystem": {
      "command": "node",
      "args": ["./mcp-servers/abap-remote-filesystem/index.js"],
      "env": {
        "SAP_HOST": "${SAP_HOST}",
        "SAP_CLIENT": "${SAP_CLIENT}",
        "SAP_USER": "${SAP_USER}",
        "SAP_PASSWORD": "${SAP_PASSWORD}"
      }
    }
  }
}
```

---

### 3.2 MCP Microsoft — Azure DevOps

#### Estado: ✅ Existe — Seleccionar y configurar

**Descripción**: Existen varios servidores MCP para el ecosistema Microsoft. El más relevante para el equipo piloto es el **Azure DevOps MCP**, que permite acceder a work items, repositorios y pipelines.

**Opciones disponibles**:
- [Azure DevOps MCP Server](https://github.com/microsoft/azure-devops-mcp) — Oficial Microsoft
- [Microsoft Graph MCP](https://github.com/microsoftgraph/msgraph-mcp) — Para SharePoint, Teams, usuarios

**Capacidades principales**:

| Área | Capacidades |
|------|-------------|
| **Work Items** | Leer, crear, actualizar historias, bugs, tareas |
| **Repositorios** | Leer archivos, listar ramas, ver commits |
| **Pipelines** | Ver estado de builds y releases |
| **Boards** | Consultar sprints y backlogs |
| **Pull Requests** | Ver y comentar PRs |

**Acción requerida en Etapa 1**:
- [ ] Seleccionar el MCP más adecuado para el equipo piloto Microsoft
- [ ] Configurar autenticación (PAT o Service Principal)
- [ ] Validar acceso a los proyectos del equipo piloto

**Configuración base**:
```json
{
  "mcpServers": {
    "azure-devops": {
      "command": "node",
      "args": ["./mcp-servers/azure-devops/index.js"],
      "env": {
        "AZURE_DEVOPS_ORG": "${ADO_ORG}",
        "AZURE_DEVOPS_PAT": "${ADO_PAT}"
      }
    }
  }
}
```

---

### 3.3 MCP Jira

#### Estado: ✅ Existe — Configurar

**Descripción**: Existe un servidor MCP oficial para Jira que permite a Cline acceder a proyectos, issues, sprints y comentarios directamente desde el IDE.

**Referencia**: [Atlassian Jira MCP](https://github.com/atlassian/mcp-atlassian) o equivalente comunitario

**Capacidades principales**:

| Tool | Descripción |
|------|-------------|
| `jira_get_issue` | Obtiene detalle completo de un issue |
| `jira_search_issues` | Busca issues por JQL |
| `jira_create_issue` | Crea un nuevo issue |
| `jira_update_issue` | Actualiza campos de un issue |
| `jira_add_comment` | Añade un comentario |
| `jira_get_sprint` | Obtiene el sprint activo |
| `jira_list_projects` | Lista proyectos disponibles |
| `jira_get_board` | Obtiene el tablero del equipo |
| `jira_transition_issue` | Cambia el estado de un issue |
| `jira_get_attachments` | Obtiene adjuntos de un issue |

**Casos de uso**:
```
CASO 1: Developer trabaja en una historia Jira
  → jira_get_issue: obtiene criterios de aceptación y descripción
  → jira_get_sprint: verifica el contexto del sprint actual
  → Cline implementa la funcionalidad con el contexto completo
  → jira_add_comment: registra el progreso

CASO 2: Resolución de bug
  → jira_search_issues: busca bugs similares resueltos
  → jira_get_issue: obtiene el detalle del bug reportado
  → Cline propone y aplica el fix
  → jira_transition_issue: mueve el issue a "In Review"
```

**Acción requerida en Etapa 1**:
- [ ] Seleccionar la implementación MCP de Jira más adecuada
- [ ] Configurar autenticación (API Token Atlassian)
- [ ] Validar acceso a los proyectos de los equipos piloto

**Configuración base**:
```json
{
  "mcpServers": {
    "jira": {
      "command": "node",
      "args": ["./mcp-servers/jira/index.js"],
      "env": {
        "JIRA_HOST": "${JIRA_HOST}",
        "JIRA_EMAIL": "${JIRA_EMAIL}",
        "JIRA_API_TOKEN": "${JIRA_API_TOKEN}"
      }
    }
  }
}
```

---

## 4. HORIZONTE 2 — MCPs a Construir (Uso Masivo)

Estos MCPs se construirán **en paralelo durante el piloto** (sub-etapas 2.1 y 2.2) para estar listos en la sub-etapa 2.3 (Uso Masivo).

### 4.1 MCP Remedy

#### Estado: 🔨 A construir — API REST disponible

**Descripción**: BMC Remedy expone una API REST que permite construir un MCP server personalizado. No existe un MCP estándar para Remedy, por lo que hay que desarrollarlo.

**Base técnica**: Remedy REST API (disponible en la mayoría de instalaciones Remedy 9.x+)

**Herramientas a implementar**:

| Tool | Descripción | Endpoint Remedy |
|------|-------------|-----------------|
| `remedy_get_ticket` | Obtiene detalle de un ticket | `GET /api/arsys/v1/entry/{form}/{id}` |
| `remedy_search_tickets` | Busca tickets por criterios | `GET /api/arsys/v1/entry/{form}?q=...` |
| `remedy_get_incident` | Obtiene una incidencia | `GET /api/arsys/v1/entry/HPD:Help Desk/{id}` |
| `remedy_search_incidents` | Busca incidencias | `GET /api/arsys/v1/entry/HPD:Help Desk?q=...` |
| `remedy_create_worklog` | Añade nota de trabajo | `POST /api/arsys/v1/entry/HPD:WorkLog` |
| `remedy_update_status` | Actualiza estado | `PUT /api/arsys/v1/entry/{form}/{id}` |
| `remedy_search_known_errors` | Busca errores conocidos | `GET /api/arsys/v1/entry/PBM:Known Error?q=...` |
| `remedy_get_sla` | Obtiene info de SLA | `GET /api/arsys/v1/entry/SLM:SLA/{id}` |

**Plan de construcción**:
```
SPRINT 1 (Semana 1-2 del piloto)
  → Análisis de la API REST de Remedy disponible
  → Autenticación y conectividad básica
  → Implementar remedy_get_incident y remedy_search_incidents

SPRINT 2 (Semana 3-4 del piloto)
  → Implementar remedy_create_worklog y remedy_update_status
  → Implementar remedy_search_known_errors
  → Testing y validación con datos reales

SPRINT 3 (Semana 5-6 del piloto)
  → Implementar herramientas restantes
  → Documentación y configuración para todos los equipos
  → Listo para Uso Masivo (sub-etapa 2.3)
```

**Valor diferencial**: Elimina el cambio de contexto entre Remedy y el IDE. El developer puede ver el ticket, codificar la solución y registrar el trabajo sin salir de VS Code.

---

### 4.2 MCP MuleSoft

#### Estado: 🔨 A construir — Anypoint Platform API disponible

**Descripción**: MuleSoft Anypoint Platform expone APIs REST completas. No existe un MCP estándar para MuleSoft, por lo que hay que desarrollarlo usando la Anypoint Platform API.

**Base técnica**: [Anypoint Platform API](https://anypoint.mulesoft.com/exchange/portals/anypoint-platform/)

**Herramientas a implementar**:

| Tool | Descripción |
|------|-------------|
| `mule_list_apis` | Lista APIs en Anypoint Exchange |
| `mule_get_api_spec` | Obtiene spec RAML/OAS de una API |
| `mule_get_flow` | Obtiene el XML de un flow Mule |
| `mule_list_connectors` | Lista conectores disponibles |
| `mule_get_deployment` | Obtiene info de un deployment |
| `mule_get_app_logs` | Obtiene logs de una aplicación |
| `mule_search_exchange` | Busca assets en Exchange |

**Plan de construcción**: Similar a Remedy, en paralelo durante el piloto.

---

## 5. HORIZONTE 3 — MCPs Futuros

### 5.1 MCP Vector Database

#### Estado: 🔲 A construir — Requiere infraestructura previa

**Descripción**: Servidor MCP para búsqueda semántica sobre la base de conocimiento del proyecto. Requiere primero desplegar la infraestructura de Aurora RDS + pgvector.

**Prerequisitos**:
- Infraestructura Aurora PostgreSQL + pgvector desplegada
- Pipeline de indexación de documentación y código
- Decisión sobre modelo de embeddings (OpenAI, Cohere, etc.)

**Herramientas previstas**:

| Tool | Descripción |
|------|-------------|
| `vector_search` | Búsqueda semántica por query |
| `vector_upsert` | Indexa nuevos documentos |
| `vector_get_similar` | Encuentra documentos similares |
| `vector_list_collections` | Lista colecciones disponibles |

**Colecciones estándar previstas**:

| Colección | Contenido |
|-----------|-----------|
| `documentation` | Documentación técnica del sistema |
| `codebase` | Fragmentos de código indexados |
| `specs` | Especificaciones OpenSpec |
| `incidents` | Incidencias resueltas y soluciones |
| `memory_banks` | Contenido de los Memory Banks |

---

### 5.2 MCP Graph Database

#### Estado: 🔲 A construir — Requiere decisión de plataforma

**Descripción**: Servidor MCP para consultas sobre relaciones entre entidades del sistema (módulos, dependencias, datos, equipos).

**Prerequisitos**:
- Decisión de plataforma: Amazon Neptune vs. IBM Context Studio vs. Neo4j
- Modelo de datos del grafo definido
- Pipeline de carga inicial de relaciones

**Herramientas previstas**:

| Tool | Descripción |
|------|-------------|
| `graph_query` | Ejecuta una consulta Cypher/SPARQL |
| `graph_get_neighbors` | Obtiene nodos relacionados |
| `graph_impact_analysis` | Analiza impacto de un cambio |
| `graph_get_dependencies` | Obtiene árbol de dependencias |

---

## 6. Git / GitHub / GitLab — Acceso vía CLI

#### Estrategia: ➡️ CLI del desarrollador (no MCP)

**Justificación**: El acceso a repositorios Git se resuelve de forma más natural y segura a través de la **CLI nativa del desarrollador** en su máquina. Cline puede ejecutar comandos `git` directamente en el terminal del desarrollador, sin necesidad de un MCP server intermedio.

**Capacidades disponibles vía CLI**:
```bash
# Cline puede ejecutar directamente:
git log --oneline -20          # Ver historial de commits
git diff HEAD~1                # Ver cambios recientes
git blame <archivo>            # Ver autoría de líneas
git branch -a                  # Ver ramas disponibles
git status                     # Estado del repositorio
gh pr list                     # Listar PRs (GitHub CLI)
gh issue view <id>             # Ver issue de GitHub
```

**Ventajas de este enfoque**:
- ✅ Sin configuración adicional (el developer ya tiene git configurado)
- ✅ Usa las credenciales y permisos existentes del developer
- ✅ Funciona con cualquier proveedor (GitHub, GitLab, Azure Repos, Bitbucket)
- ✅ Cline tiene acceso nativo a la CLI del sistema

---

## 7. Hoja de Ruta de MCPs

```
ETAPA 1                    SUB-ETAPA 2.1        SUB-ETAPA 2.2        SUB-ETAPA 2.3
Definición                 Configuración        Uso Controlado       Uso Masivo
──────────────────         ─────────────────    ──────────────────   ──────────────────
• Seleccionar MCP SAP      • Instalar MCP SAP   • Usar MCP SAP       • MCP Remedy listo
• Seleccionar MCP MSFT     • Instalar MCP MSFT  • Usar MCP MSFT      • MCP Mule listo
• Seleccionar MCP Jira     • Instalar MCP Jira  • Usar MCP Jira      • Todos H1+H2 activos
• Planificar construcción  • Iniciar build      • Continuar build    
  MCP Remedy y Mule          MCP Remedy y Mule    MCP Remedy y Mule  
                           • Documentar CLI Git • Usar CLI Git       • Usar CLI Git
```

---

## 8. Criterios de Selección de MCPs (Horizonte 1)

Para los MCPs que ya existen pero hay que seleccionar, se evaluarán con los siguientes criterios:

| Criterio | Peso | Descripción |
|----------|------|-------------|
| **Madurez** | 30% | Versión estable, mantenimiento activo, comunidad |
| **Cobertura funcional** | 25% | Cubre los casos de uso prioritarios del equipo |
| **Facilidad de configuración** | 20% | Tiempo de setup, documentación disponible |
| **Seguridad** | 15% | Gestión de credenciales, permisos granulares |
| **Rendimiento** | 10% | Latencia de respuesta, límites de rate |