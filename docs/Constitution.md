# Project Constitution: PollaMundialista

## Tech Stack
- **Design & UI Prototyping:** Google Stitch (Herramienta oficial de maquetación interactiva y Vibe Design mediante servidor MCP)
- **Frontend:** Angular (Versión estable con control flow @if/@for)
- **State Management & Reactivity:** 100% Angular Signals (`signal`, `computed`, `resource`)
- **Dependency Injection:** Enfoque funcional moderno utilizando la función `inject()` (Sin inyección por constructor para servicios o componentes)
- **Styling:** Tailwind CSS (Tema minimalista y limpio basado en los tokens de diseño de Google Stitch)
- **Testing:** Pruebas unitarias integradas utilizando el patrón AAA (Arrange-Act-Assert)

## Approved Architecture Principles
- **Layered Architecture:** Estricta separación de capas:
  - **Component Layer:** Presentación pura de la interfaz de usuario y binding reactivo mediante Signals. Implementa fielmente las vistas exportadas por Google Stitch. Sin lógica de negocio compleja.
  - **Service Layer:** Orquestación del estado, control de flujos HTTP y evaluación de reglas de negocio.
  - **Model Layer:** Definición pura de tipos, interfaces y mapeadores de datos.
- **Single Responsibility Principle (SRP):** Cada clase, función o componente debe cumplir con un único propósito aislado.
- **Human-in-the-Loop (HITL) Model:** El agente de IA es una máquina de ejecución guiada. No debe realizar cambios estructurales, de lógica ni de diseño visual sin aprobación explícita del usuario.

## Boundaries & Guardrails
### ✅ ALWAYS DO:
- Escribir pruebas unitarias automatizadas para toda la lógica y validación de reglas ANTES de dar una tarea por completada.
- Utilizar el patrón Arrange-Act-Assert (AAA) en todos los archivos de pruebas.
- Nombrar los archivos de prueba como `[nombre].spec.ts`.
- Retornar objetos de error explícitos y fuertemente tipados ante fallas de validación.
- **Sincronizar e importar** los componentes visuales, layouts y tokens de diseño generados en el canvas de Google Stitch a través del conector MCP correspondiente antes de maquetar el frontend.

### 🚫 NEVER DO:
- Nunca utilizar inyección por constructor tradicional (`constructor(private service: Service)`) para dependencias.
- Nunca usar directivas estructurales antiguas (`*ngIf`, `*ngFor`).
- Nunca mezclar lógica matemática de cálculo de puntajes dentro de las plantillas HTML o el código de los componentes visuales.
- Nunca saltarse el orden secuencial establecido en `tasks.md`.
- **Nunca improvisar la interfaz de usuario (Vibe Designing):** Queda estrictamente prohibido que la IA genere estilos, vistas o layouts en Angular que no coincidan exactamente con la especificación visual y los artefactos de diseño exportados desde Google Stitch.

## Business Error Codes
- **PREDICTION_LOCKED:** Intento de guardar o modificar un pronóstico para un partido que ya se encuentra en vivo ('live') o finalizado ('finished').
- **SCORE_CALCULATION_NOT_ALLOWED:** Intento de calcular el puntaje de la polla en un partido que aún no ha concluido.
- **DUPLICATE_PREDICTION:** Intento de registrar más de una predicción para el mismo identificador de partido (matchId).

## Error Handling Standards
Todas las validaciones o errores del sistema de cara al cliente deben producir un objeto inmutable con este esquema de ejemplo:
```json
{
  "error": "Explicación legible del error para el usuario",
  "code": "CODIGO_DE_ERROR",
  "timestamp": "ISO-8601"
}
```
