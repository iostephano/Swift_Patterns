# Swift Patterns

Playground de Swift que documenta siete patrones de ingeniería iOS aplicados a un dominio fintech simulado, con el detalle de cuándo conviene usarlos y cuándo no.

<img width="1500" height="500" alt="repositorio" src="https://github.com/user-attachments/assets/a1747323-efd2-4e3e-b2d7-8105ae1fd0b6" />

## Propósito

Este repositorio es material educativo de **SwiftLatam**. No es una aplicación, ni una librería, ni un paquete distribuible.

Cada página del playground toma un problema real del dominio financiero pagos, saldos, KYC, custodia de tokens y muestra un patrón que lo resuelve. Todas siguen la misma estructura:

1. **Problema.** Qué falla si no se aplica el patrón.
2. **Solución.** Cómo se implementa en Swift.
3. **Cuándo usarlo.**
4. **Cuándo NO usarlo.**

El cuarto punto es deliberado. La mayoría del material sobre patrones enseña a aplicarlos; muy poco enseña a reconocer cuándo son sobreingeniería.

## Para quién es

- Desarrolladores iOS de nivel intermedio y senior.
- Ingenieros que entran al dominio fintech.
- Preparación de entrevistas técnicas de arquitectura.

Se asume familiaridad con Swift, protocolos y `async/await`.

## Contenidos

| Página | Patrón | Contexto fintech |
|---|---|---|
| `LazyLoading` | Carga diferida | Inicialización costosa bajo demanda |
| `DependencyInjection` | Inyección por protocolos e inicializador | Gateway de pagos, logger y detección de fraude sustituibles |
| `Modularization` | Fronteras de módulo | Separación de responsabilidades por dominio |
| `StateManagement` | Estado único, reducer, flujo unidireccional | Ciclo de vida de un pago |
| `Concurrency` | `actor`, `async let`, `TaskGroup` | Llamadas concurrentes a servicios |
| `PrecisionHandling` | `Decimal` y redondeo centralizado | Aritmética de dinero sin pérdida de precisión |
| `SecureStorage` | Keychain y abstracción de almacenamiento | Custodia de tokens de sesión |

## Decisiones técnicas

Algunas decisiones del código son intencionales y podrían leerse como descuidos. Están explicadas en comentarios dentro de las páginas correspondientes:

**`Decimal`, nunca `Double`, para dinero.** Los valores monetarios se construyen con `Decimal(string:)` y el redondeo pasa por un único punto. `Double` introduce errores de representación inaceptables en aritmética financiera.

**Inyección de dependencias sin contenedor.** Protocolos e inicializadores bastan. No se usa ningún framework de DI de terceros, y la página explica por qué la mayoría de proyectos tampoco lo necesita.

**`precondition` para el mismatch de moneda.** Sumar soles con dólares es un error de programador, no una condición recuperable. La validación de datos externos pertenece al borde del sistema, antes de construir un `Money`.

**Estados imposibles irrepresentables.** `StateManagement` modela el ciclo de un pago con un `enum` y un reducer, de modo que el sistema de tipos impide combinaciones inválidas.

**Módulos simulados con `enum`.** Un playground no admite targets separados. La página lo declara explícitamente: en un proyecto real estos serían Swift Packages.

## Requisitos

- Xcode <!-- CONFIRMAR VERSIÓN --> o superior.
- Swift 6 (declarado en el playground).
- Plataforma destino: iOS.

## Ejecución

1. Clona el repositorio.
2. Abre `Patterns.playground` en Xcode.
3. Muestra el navegador de páginas y recorre las siete en cualquier orden. Cada una es autocontenida.

No hay dependencias externas que instalar. No hay `Package.swift`, `Podfile` ni `Cartfile`.

## Estado

Las siete páginas compilan y se ejecutan en Xcode. Verificado adicionalmente con `swiftc -typecheck` bajo `-swift-version 6 -strict-concurrency=complete`, sin errores ni warnings.

El repositorio es material de referencia estable. No está en desarrollo activo.

## Limitaciones conocidas

**No hay pruebas automatizadas.** Los Swift Playgrounds no admiten un target de pruebas nativo. La testabilidad se demuestra conceptualmente mediante *test doubles* (`MockGateway`, `MockLogger`, `MockFraudDetector`), pero ninguna prueba se ejecuta. Validar la lógica pura con XCTest o Swift Testing exigiría extraerla a un Swift Package, lo que cambiaría la naturaleza del repositorio.

**`TokenManager.persist` no es atómico.** Guarda el access token y el refresh token en dos operaciones independientes. Si la segunda falla, queda un estado parcial. La limitación está documentada en el código: un sistema real requeriría compensación o escritura atómica. Se conserva así porque implementar el rollback oscurecería el patrón que la página enseña.

**Los servicios son simulados.** El networking se emula con `Task.sleep`. `KeychainStore` sí usa el Keychain real, con `kSecAttrAccessibleAfterFirstUnlockThisDeviceOnly`.

**Nunca registres tokens.** El código lo advierte de forma explícita. Los ejemplos imprimen valores solo con fines didácticos, con datos ficticios.

## Licencia

MIT. Ver [LICENSE](LICENSE).

## SwiftLatam

Material educativo de SwiftLatam. Compartido para que otras personas aprendan.
