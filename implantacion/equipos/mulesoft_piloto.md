# 🟠 Plan Piloto — Equipo MuleSoft

## 1. Contexto del Piloto MuleSoft

### 1.1 Descripción del Equipo
El equipo piloto MuleSoft es el primer equipo de integración en adoptar el ecosistema de desarrollo aumentado por IA. Su experiencia servirá de referencia para el resto de equipos MuleSoft de la organización.

### 1.2 Stack Tecnológico del Equipo

| Tecnología | Descripción |
|------------|-------------|
| **Mule 4** | Runtime de integración principal |
| **DataWeave 2.0** | Lenguaje de transformación de datos |
| **Anypoint Platform** | Plataforma de gestión de APIs e integraciones |
| **Anypoint Exchange** | Repositorio de assets reutilizables |
| **Anypoint Studio** | IDE de desarrollo MuleSoft |
| **CloudHub / RTF** | Plataforma de despliegue |

### 1.3 Información del Equipo

| Campo | Valor |
|-------|-------|
| **Nombre del equipo** | [Por definir] |
| **Tech Lead** | [Por definir] |
| **Número de developers** | [Por definir] |
| **Proyectos activos** | [Por definir] |
| **Fecha de inicio del piloto** | [Por definir] |

---

## 2. Componentes del Ecosistema para MuleSoft

### 2.1 MCP MuleSoft — Capacidades Específicas

```
MCP MULESOFT — HERRAMIENTAS DISPONIBLES
├── mule_list_apis          → Listar APIs en Anypoint Exchange
├── mule_get_api_spec       → Obtener spec RAML/OAS de una API
├── mule_get_flow           → Obtener XML de un flow Mule
├── mule_list_connectors    → Listar conectores disponibles
├── mule_get_deployment     → Info de deployment en entorno
├── mule_list_environments  → Listar entornos disponibles
├── mule_get_app_logs       → Obtener logs de una aplicación
└── mule_search_exchange    → Buscar assets en Exchange
```

### 2.2 Reglas Cline para MuleSoft (`.clinerules/mulesoft.md`)

```
ESTÁNDARES MULESOFT — RESUMEN
├── API DESIGN (API-Led Connectivity)
│   ├── Seguir la metodología API-Led (System, Process, Experience)
│   ├── Diseñar APIs en RAML o OpenAPI antes de implementar
│   ├── Versionar APIs (v1, v2...) en la URL
│   ├── Usar HTTP status codes correctamente
│   └── Documentar todos los endpoints con ejemplos
│
├── DESARROLLO MULE 4
│   ├── Separar lógica en flows reutilizables (sub-flows)
│   ├── Usar Error Handling global + específico por flow
│   ├── Logging estructurado en todos los flows
│   ├── Externalizar configuración (properties files)
│   └── Usar Secure Properties para credenciales
│
├── DATAWEAVE
│   ├── Funciones DataWeave reutilizables en módulos
│   ├── Evitar transformaciones complejas inline
│   ├── Documentar transformaciones no obvias
│   └── Tests unitarios para transformaciones complejas
│
└── TESTING
    ├── MUnit para tests unitarios de flows
    ├── Cobertura mínima del 70%
    ├── Tests de integración con sistemas mock
    └── Postman/Newman para tests de API
```

### 2.3 Libro Blanco MuleSoft

El Libro Blanco MuleSoft cubre:
- Guía de API-Led Connectivity (System, Process, Experience APIs)
- Patrones de integración empresarial (EIP) en Mule 4
- Guía de DataWeave 2.0 (transformaciones, funciones, módulos)
- Estándares de error handling y logging
- Guía de seguridad (OAuth, JWT, TLS)
- Guía de testing con MUnit
- Patrones de despliegue en CloudHub/RTF

### 2.4 Memory Bank MuleSoft

```
memory-bank/
├── projectbrief.md
├── productContext.md
├── systemPatterns.md
├── techContext.md
├── activeContext.md
├── progress.md
├── api_catalog.md