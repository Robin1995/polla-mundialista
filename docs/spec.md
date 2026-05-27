# Product Specification: PollaMundialista Dashboard

## 3. User Stories

US-001: Grid Dashboard Visualizer
Como participante de la polla,
Quiero ver un tablero organizado con los partidos categorizados por su estado,
Para poder identificar fácilmente cuáles juegos están abiertos para modificar y cuáles están cerrados.

Criterios de Aceptación:

- Los partidos en estado live muestran un badge visual parpadeante de "EN VIVO".

- Los partidos finalizados muestran el puntaje total obtenido de forma clara al lado de los marcadores.

US-002: Dynamic Prediction Input
Como participante de la polla,
Quiero registrar y modificar mis marcadores estimados para los próximos partidos,
Para asegurar mi participación antes del pitazo inicial.

Criterios de Aceptación:

- Las entradas numéricas de goles se validan estrictamente como enteros mayores o iguales a cero.

- Al guardar los cambios, se actualizan de forma reactiva las proyecciones globales usando Signals.

## 4. Immutable Business Rules (Gherkin Framework)

BR-001: Bloqueo de Predicción Iniciada (PREDICTION_LOCKED)
GIVEN un partido de fútbol cuyo estado actual es live o finished,

WHEN el usuario emite una petición para crear o modificar su predicción,

THEN el sistema rechaza la operación inmediatamente y devuelve el código de error PREDICTION_LOCKED.

BR-002: Motor de Evaluación de Puntaje (SCORE_CALCULATION_NOT_ALLOWED)
GIVEN un partido cuyo estado es scheduled o live,

WHEN se solicita un cálculo de puntos para la polla,

THEN el sistema bloquea la ejecución y arroja el error SCORE_CALCULATION_NOT_ALLOWED.

GIVEN un partido en estado finished, los puntos se asignan así:

- 3 Puntos: Si el usuario acertó el marcador exacto (Ej: Pronóstico 2-1, Resultado Real 2-1).

- 1 Punto: Si el usuario acertó el ganador o el empate, pero no el marcador exacto (Ej: Pronóstico 3-0, Resultado Real 1-0).

- 0 Puntos: Si no acertó el resultado general.

BR-003: Prevención de Duplicados (DUPLICATE_PREDICTION)
GIVEN una predicción ya registrada para un matchId específico,

WHEN se envía una nueva petición de creación para ese mismo partido,

THEN el sistema cancela el proceso y arroja un error DUPLICATE_PREDICTION.

## 5. Exclusions & Scope Limitations

❌ Sistemas complejos de autenticación OAuth en Fase 1 (se usarán mocks locales).

❌ Tablas de posiciones globales multijugador en tiempo real.
