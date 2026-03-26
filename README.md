# TechNova Cloud v2.0 - Refactorización XSD

Este repositorio contiene la evolución del proyecto de Auditoría de Infraestructura Cloud, cumpliendo con los requisitos de refactorización y uso de indicadores avanzados de XSD (RA6 - CE e, i).

## Cambios Realizados
Se han implementado las 6 misiones de mantenimiento crítico:
- **Modularización**: Uso de `xs:attributeGroup` y `xs:group` para hardware y atributos.
- **Validación de Cantidades**: GPU opcional y límite de 8 discos.
- **Lógica Excluyente**: Implementación de `xs:choice` para la configuración de red (IP/DHCP).
- **Flexibilidad**: Uso de `xs:all` en el nodo de auditoría.
- **Integridad**: Restricción `xs:unique` para evitar duplicidad de IDs.

## Respuestas a la Misión

### 1. Ahorro de líneas de código
Al utilizar grupos (`attributeGroup` y `group`), se ha optimizado la definición del esquema. 
- **Ahorro**: Se han ahorrado aproximadamente **20 líneas de código repetitivo** por cada declaración de servidor. 
- **Impacto**: En lugar de definir manualmente 3 atributos y 4 elementos de hardware en cada nodo, ahora solo se invocan dos referencias (`ref`), facilitando la escalabilidad del catálogo.

### 2. Error de Duplicidad en VS Code
Al intentar introducir dos servidores con el mismo atributo `@id`, el motor de validación basado en la restricción `xs:unique` genera el siguiente error:
> *"Identity Constraint Violation: The value 'srv-web-01' is not unique within the scope of the identity constraint 'UnicoID'."*
