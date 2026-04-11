# Swift Patterns

Repositorio de Swift Playground orientado a producción que demuestra patrones
arquitectónicos reales utilizados en aplicaciones fintech en iOS.

No es un tutorial básico — es una referencia estructurada para desarrolladores
intermedios y senior que buscan código limpio, mantenible y escalable.

---

## ¿Por qué existe este repositorio?

La mayoría del contenido de Swift se enfoca en sintaxis o ejemplos simples.
Este repositorio se enfoca en decisiones reales de arquitectura:

- Precisión en cálculos monetarios
- Concurrencia segura
- Servicios desacoplados
- Almacenamiento seguro
- Manejo predecible del estado

El contexto fintech es intencional: aquí la **correctitud es crítica**.

---

## ¿Para quién es?

- Desarrolladores iOS que quieren subir a nivel senior
- Ingenieros que entran a fintech
- Preparación para entrevistas técnicas (arquitectura)
- Personas construyendo apps de pagos, banca o trading

---

## Temas

- Lazy Loading
- Dependency Injection
- Modularization
- State Management
- Concurrency
- Precision Handling
- Secure Storage

---

## Setup

1. Clona el repositorio
2. Abre `Patterns.playground` en Xcode
3. Navega por las páginas desde la barra lateral
4. Revisa la carpeta `Docs/` para teoría

---

## Nota importante

En aplicaciones financieras:

- `Double` NO es seguro para dinero
- Estado compartido NO es seguro en concurrencia
- Servicios acoplados NO son testeables

Este repositorio existe para evitar esos errores.

---

## Licencia

MIT
