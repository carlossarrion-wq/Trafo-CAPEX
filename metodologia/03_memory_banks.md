# 🧠 Memory Banks — Gestión del Conocimiento por Proyecto

## 1. ¿Qué son los Memory Banks?

Los **Memory Banks** son el sistema de memoria persistente del ecosistema. Resuelven uno de los principales retos de los agentes IA: **la falta de memoria entre sesiones**.

Sin Memory Banks, Cline y los demás agentes comienzan cada sesión "desde cero", sin conocimiento del proyecto, sus decisiones técnicas, su arquitectura ni su historial. Con Memory Banks, el agente tiene acceso inmediato a todo el contexto relevante del proyecto.

```
SIN MEMORY BANKS                    CON MEMORY BANKS
────────────────────                ────────────────────────────────
Sesión 1: Cline aprende             Sesión 1: Cline aprende
          el proyecto               Sesión 2: Cline recuerda TODO
Sesión 2: Cline olvida              Sesión N: Contexto acumulado
          todo                                y enriquecido
```

---

## 2. Estructura de un Memory Bank

Cada proyecto tiene su propio Memory Bank con la siguiente estructura estándar:

```
memory-bank/
├── projectbrief.md        ← El "qué" del proyecto
├── productContext.md      ← El "por qué" del proyecto
├── systemPatterns.md      ← El "cómo" técnico
├── techContext.md         ← El stack y entorno
├── activeContext.md       ← El estado actual
└── progress.md            ← El progreso y pendientes
```

### 2.1 `projectbrief.md` — El Proyecto

**Propósito**: Documento fundacional que define qué es el proyecto.

```markdown
# Project Brief: [Nombre del Proyecto]

## Descripción
[Qué es el proyecto en 2-3 frases]

## Objetivos
- [Objetivo 1]
- [Objetivo 2]

## Alcance
### En alcance:
- [Item]
### Fuera de alcance:
- [Item]

## Stakeholders
| Rol | Nombre | Responsabilidad |
|-----|--------|-----------------|

## Fechas Clave
| Hito | Fecha |
|------|-------|

## Restricciones
- [Restricción técnica, de negocio o de tiempo]
```

### 2.2 `productContext.md` — El Contexto del Producto

**Propósito**: Explica por qué existe el proyecto y qué problemas resuelve.

```markdown
# Product Context: [Nombre del Proyecto]

## Problema que Resuelve
[Descripción del problema de negocio]

## Usuarios y Casos de Uso Principales
| Usuario | Caso de Uso Principal |
|---------|----------------------|

## Flujos de Negocio Clave
[Descripción de los flujos principales]

## Integraciones con Otros Sistemas
| Sistema | Tipo de Integración | Dirección |
|---------|--------------------|-----------| 

## Decisiones de Producto
| Decisión | Justificación | Fecha |
|----------|---------------|-------|
```

### 2.3 `systemPatterns.md` — Patrones del Sistema

**Propósito**: Documenta la arquitectura, patrones de diseño y decisiones técnicas del proyecto.

```markdown
# System Patterns: [Nombre del Proyecto]

## Arquitectura del Sistema
[Descripción de la arquitectura con diagrama ASCII si aplica]

## Patrones de Diseño Utilizados
| Patrón | Dónde se Aplica | Justificación |
|--------|----------------|---------------|

## Decisiones de Arquitectura (ADRs)
| ADR | Decisión | Justificación | Fecha |
|-----|----------|---------------|-------|

## Convenciones de Código
- Naming: [convención]
- Estructura de carpetas: [convención]
- Manejo de errores: [patrón]

## Anti-patrones a Evitar
- [Anti-patrón 1 y por qué evitarlo]
```

### 2.4 `techContext.md` — Contexto Técnico

**Propósito**: Documenta el stack tecnológico, dependencias y entorno de desarrollo.

```markdown
# Tech Context: [Nombre del Proyecto]

## Stack Tecnológico
| Capa | Tecnología | Versión | Notas |
|------|-----------|---------|-------|

## Dependencias Principales
| Dependencia | Versión | Propósito |
|-------------|---------|-----------|

## Entorno de Desarrollo
- IDE: [VS Code + extensiones]
- Herramientas: [lista]
- Configuración especial: [notas]

## Entornos
| Entorno | URL/Host | Propósito |
|---------|----------|-----------|

## Credenciales y Accesos
[NO incluir credenciales reales. Referenciar a vault/gestor de secretos]

## Configuración de MCP Servers
[Lista de MCP servers configurados para este proyecto]
```

### 2.5 `activeContext.md` — Contexto Activo

**Propósito**: Captura el estado actual del trabajo. Es el archivo que más frecuentemente se actualiza.

```markdown
# Active Context: [Nombre del Proyecto]

## Última Actualización
[Fecha y hora]

## Trabajo en Curso
[Descripción de lo que se está desarrollando ahora mismo]

## Decisiones Recientes
| Decisión | Justificación | Fecha |
|----------|---------------|-------|

## Problemas Abiertos
| Problema | Estado | Responsable |
|----------|--------|-------------|

## Próximos Pasos
1. [Paso 1]
2. [Paso 2]

## Contexto para la Próxima Sesión
[Notas específicas para que Cline retome el trabajo sin fricción]
```

### 2.6 `progress.md` — Progreso del Proyecto

**Propósito**: Registra qué está hecho, qué falta y el estado general del proyecto.

```markdown
# Progress: [Nombre del Proyecto]

## Estado General
[En progreso / En revisión / Completado]

## Completado ✅
- [Feature/componente completado]

## En Progreso 🔄
- [Feature/componente en desarrollo]

## Pendiente 📋
- [Feature/componente por desarrollar]

## Bloqueado 🚫
| Item | Bloqueante | Responsable |
|------|-----------|-------------|

## Métricas
| Métrica | Valor |
|---------|-------|
| Story Points completados | X |
| Story Points pendientes | X |
| Cobertura de tests | X% |
| Deuda técnica identificada | X items |
```

---

## 3. Ciclo de Vida del Memory Bank

### 3.1 Inicialización (Inicio del Proyecto)

```
INICIALIZACIÓN DEL MEMORY BANK
────────────────────────────────────────────────────────────
1. Developer proporciona documentación inicial del proyecto
   (specs existentes, documentación técnica, emails, etc.)

2. Cline lee toda la documentación disponible

3. Cline genera los 6 archivos del Memory Bank
   con la información extraída

4. Developer revisa y complementa los archivos

5. Memory Bank queda listo para uso
────────────────────────────────────────────────────────────
```

### 3.2 Mantenimiento (Durante el Desarrollo)

```
ACTUALIZACIÓN DEL MEMORY BANK
────────────────────────────────────────────────────────────
CUÁNDO actualizar:
  • Al tomar una decisión técnica importante
  • Al completar un feature o componente
  • Al resolver un problema complejo
  • Al cambiar la arquitectura o los patrones
  • Al inicio/fin de cada sesión de trabajo

QUIÉN actualiza:
  • Cline actualiza automáticamente activeContext.md y progress.md
  • Developer revisa y valida las actualizaciones
  • Tech Lead actualiza systemPatterns.md tras decisiones de arquitectura

CÓMO actualiza Cline:
  • Al inicio de sesión: lee todos los archivos del Memory Bank
  • Durante la sesión: identifica información nueva relevante
  • Al final de la sesión: actualiza los archivos correspondientes
────────────────────────────────────────────────────────────
```

### 3.3 Consulta (Uso por los Agentes)

```
CONSULTA DEL MEMORY BANK
────────────────────────────────────────────────────────────
• Cline: carga el Memory Bank al inicio de cada tarea
• Agente de Conceptualización: consulta para contexto histórico
• Agentes OpenSpec: consultan para generar specs consistentes
• Agente de Estimación: consulta para calibrar estimaciones
• Agente de Revisión: consulta para verificar consistencia
────────────────────────────────────────────────────────────
```

---

## 4. Memory Banks por Tecnología

Cada tecnología tiene consideraciones específicas en sus Memory Banks:

### 4.1 Memory Bank SAP

Archivos adicionales recomendados:
```
memory-bank/
├── [archivos estándar]
├── sap_landscape.md       ← Descripción del landscape SAP (DEV/QAS/PRD)
├── sap_objects.md         ← Inventario de objetos ABAP del proyecto
├── sap_customizing.md     ← Configuración de customizing relevante
└── sap_transports.md      ← Historial de transportes importantes
```

### 4.2 Memory Bank Microsoft

Archivos adicionales recomendados:
```
memory-bank/
├── [archivos estándar]
├── azure_resources.md     ← Recursos Azure del proyecto
├── ado_structure.md       ← Estructura de Azure DevOps (repos, pipelines)
└── power_platform.md      ← Componentes de Power Platform (si aplica)
```

### 4.3 Memory Bank MuleSoft

Archivos adicionales recomendados:
```
memory-bank/
├── [archivos estándar]
├── api_catalog.md         ← Catálogo de APIs del proyecto
├── integration_patterns.md ← Patrones de integración utilizados
└── anypoint_structure.md  ← Estructura en Anypoint Platform
```

### 4.4 Memory Bank Darwin

Archivos adicionales recomendados:
```
memory-bank/
├── [archivos estándar]
├── component_library.md   ← Componentes React reutilizables
├── api_contracts.md       ← Contratos de API backend
└── db_schema.md           ← Esquema de base de datos
```

---

## 5. Relación con Otros Componentes

### 5.1 Memory Banks + Vector DB
- El contenido de los Memory Banks se **indexa en la Vector DB**
- Esto permite búsquedas semánticas sobre el conocimiento del proyecto
- La Vector DB complementa los Memory Banks con búsqueda por similitud

### 5.2 Memory Banks + Graph DB
- Las relaciones entre entidades documentadas en los Memory Banks se **modelan en la Graph DB**
- La Graph DB permite consultas estructurales que los Memory Banks no pueden responder
- Ejemplo: "¿Qué módulos dependen del componente X?" → Graph DB

### 5.3 Memory Banks + Reglas Cline
- Las reglas Cline (`.clinerules`) son **complementarias** a los Memory Banks
- Las reglas definen **cómo** trabajar (estándares, convenciones)
- Los Memory Banks definen **qué** es el proyecto (contexto, decisiones)

---

## 6. Buenas Prácticas

### 6.1 Qué SÍ incluir
✅ Decisiones técnicas y su justificación  
✅ Patrones de diseño adoptados  
✅ Problemas resueltos y cómo se resolvieron  
✅ Dependencias y sus versiones  
✅ Convenciones de naming y estructura  
✅ Contexto de negocio relevante para el desarrollo  
✅ Próximos pasos y trabajo pendiente  

### 6.2 Qué NO incluir
❌ Credenciales o secretos (usar vault)  
❌ Datos personales de usuarios  
❌ Información confidencial de negocio no necesaria para el desarrollo  
❌ Código fuente (está en Git)  
❌ Documentación redundante con la spec (referenciar, no duplicar)  

### 6.3 Mantenimiento de la Calidad
- Revisar y limpiar el Memory Bank al inicio de cada sprint
- Archivar información obsoleta en lugar de eliminarla
- Mantener `activeContext.md` siempre actualizado
- Validar que las decisiones documentadas siguen siendo válidas