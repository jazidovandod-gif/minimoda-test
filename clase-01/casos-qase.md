# Catálogo de casos de prueba — MiniModa Registro (Clase 1 / TestingAI)

**Sitio:** https://minimoda-navy.vercel.app/registro

## Reglas observadas (no inventar otras)
- Campos: Nombre, Email, Contraseña (hint «Mínimo 8 caracteres.»), Confirmar contraseña, Edad (hint «Número entero entre 13 y 120.»), País (select, 9 opciones incl. Bolivia), checkbox de términos; botón «Crear cuenta».
- Banner general de error: «Revisá los campos marcados.»
- Mensajes de campo conocidos: «El nombre es obligatorio.», «El email es obligatorio.», «La contraseña es obligatoria.», «Confirmá tu contraseña.», «La edad es obligatoria.», «Seleccioná un país.», «Debés aceptar los términos.», «La contraseña debe tener al menos 8 caracteres.», «Las contraseñas no coinciden.», «La edad debe estar entre 13 y 120.»
- Éxito: «¡Registro exitoso! Bienvenido/a a MiniModa, <nombre>. Te enviamos un email de bienvenida (ver Bandeja).»
- El email no puede repetirse.
- Donde el texto exacto no está documentado se indica **(mensaje exacto a confirmar)**.
- Donde la spec solo exige mínimo 8 (sin números / sin mayúsculas / con espacios / muy larga): resultado = se acepta según la regla documentada; **verificar**.

**Total de casos:** 40

## Suites
- **Registro – Flujo general:** MM-001, MM-002, MM-036, MM-037, MM-038 (5)
- **Registro – Email:** MM-003, MM-023, MM-024, MM-025, MM-026, MM-027, MM-028, MM-040 (8)
- **Registro – Contraseña:** MM-004, MM-005, MM-009, MM-010, MM-011, MM-012, MM-013, MM-014, MM-015, MM-039 (10)
- **Registro – Edad:** MM-006, MM-007, MM-016, MM-017, MM-018, MM-019, MM-020, MM-021, MM-022 (9)
- **Registro – País y términos:** MM-008, MM-034, MM-035 (3)
- **Registro – Nombre:** MM-029, MM-030, MM-031, MM-032, MM-033 (5)

## MM-001 — Registro: alta exitosa con datos válidos
- **Suite:** Registro – Flujo general
- **Prioridad:** alta | **Severidad:** crítica | **Tipo:** positivo
- **Precondiciones:** Estar en https://minimoda-navy.vercel.app/registro con el formulario de registro visible (recargar si hace falta).
- **Pasos:**
  1. Completar Nombre — datos: `Prueba QA`
  2. Completar Email — datos: `qa.prueba+mm001@example.com`
  3. Completar Contraseña — datos: `Segura123`
  4. Completar Confirmar contraseña — datos: `Segura123`
  5. Completar Edad — datos: `25`
  6. Seleccionar País — datos: `Bolivia`
  7. Marcar checkbox de términos — datos: `Acepto los términos y condiciones`
  8. Clic en «Crear cuenta»
- **Resultado esperado final:** Banner verde «¡Registro exitoso! Bienvenido/a a MiniModa, Prueba QA. Te enviamos un email de bienvenida (ver Bandeja).» Sin errores de validación.

## MM-002 — Registro: todos los campos vacíos
- **Suite:** Registro – Flujo general
- **Prioridad:** alta | **Severidad:** mayor | **Tipo:** negativo
- **Precondiciones:** Estar en https://minimoda-navy.vercel.app/registro con el formulario de registro visible (recargar si hace falta).
- **Pasos:**
  1. Dejar todos los campos vacíos y País sin seleccionar; no marcar términos
  2. Clic en «Crear cuenta»
- **Resultado esperado final:** Banner «Revisá los campos marcados.» Mensajes: «El nombre es obligatorio.», «El email es obligatorio.», «La contraseña es obligatoria.», «Confirmá tu contraseña.», «La edad es obligatoria.», «Seleccioná un país.», «Debés aceptar los términos.» No se crea la cuenta.

## MM-003 — Registro: email sin arroba
- **Suite:** Registro – Email
- **Prioridad:** alta | **Severidad:** mayor | **Tipo:** negativo
- **Precondiciones:** Estar en https://minimoda-navy.vercel.app/registro con el formulario de registro visible (recargar si hace falta).
- **Pasos:**
  1. Completar Nombre — datos: `Prueba QA`
  2. Completar Email — datos: `usuarioejemplo.com`
  3. Completar Contraseña y Confirmar — datos: `Segura123`
  4. Completar Edad — datos: `25`
  5. Seleccionar País — datos: `Bolivia`
  6. Marcar términos
  7. Clic en «Crear cuenta»
- **Resultado esperado final:** No se crea la cuenta. Banner «Revisá los campos marcados.» (si aplica) y mensaje de email inválido bajo el campo (mensaje exacto a confirmar).

## MM-004 — Registro: contraseña de 7 caracteres
- **Suite:** Registro – Contraseña
- **Prioridad:** alta | **Severidad:** mayor | **Tipo:** borde
- **Precondiciones:** Estar en https://minimoda-navy.vercel.app/registro con el formulario de registro visible (recargar si hace falta).
- **Pasos:**
  1. Completar Nombre — datos: `Prueba QA`
  2. Completar Email — datos: `qa.prueba+mm004@example.com`
  3. Completar Contraseña — datos: `1234567`
  4. Completar Confirmar contraseña — datos: `1234567`
  5. Completar Edad — datos: `25`
  6. Seleccionar País — datos: `Bolivia`
  7. Marcar términos
  8. Clic en «Crear cuenta»
- **Resultado esperado final:** Banner «Revisá los campos marcados.» Bajo contraseña: «La contraseña debe tener al menos 8 caracteres.» (helper: «Mínimo 8 caracteres.»). No se crea la cuenta.

## MM-005 — Registro: contraseñas no coinciden
- **Suite:** Registro – Contraseña
- **Prioridad:** alta | **Severidad:** mayor | **Tipo:** negativo
- **Precondiciones:** Estar en https://minimoda-navy.vercel.app/registro con el formulario de registro visible (recargar si hace falta).
- **Pasos:**
  1. Completar Nombre — datos: `Prueba QA`
  2. Completar Email — datos: `qa.prueba+mm005@example.com`
  3. Completar Contraseña — datos: `Segura123`
  4. Completar Confirmar contraseña — datos: `Segura999`
  5. Completar Edad — datos: `25`
  6. Seleccionar País — datos: `Bolivia`
  7. Marcar términos
  8. Clic en «Crear cuenta»
- **Resultado esperado final:** Banner «Revisá los campos marcados.» Mensaje «Las contraseñas no coinciden.» No se crea la cuenta.

## MM-006 — Registro: edad 12 (límite inferior -1)
- **Suite:** Registro – Edad
- **Prioridad:** alta | **Severidad:** mayor | **Tipo:** borde
- **Precondiciones:** Estar en https://minimoda-navy.vercel.app/registro con el formulario de registro visible (recargar si hace falta).
- **Pasos:**
  1. Completar Nombre — datos: `Prueba QA`
  2. Completar Email — datos: `qa.prueba+mm006@example.com`
  3. Completar Contraseña y Confirmar — datos: `Segura123`
  4. Completar Edad — datos: `12`
  5. Seleccionar País — datos: `Bolivia`
  6. Marcar términos
  7. Clic en «Crear cuenta»
- **Resultado esperado final:** Banner «Revisá los campos marcados.» Bajo edad: «La edad debe estar entre 13 y 120.» (helper: «Número entero entre 13 y 120.»). No se crea la cuenta.

## MM-007 — Registro: edad 121 (límite superior +1)
- **Suite:** Registro – Edad
- **Prioridad:** alta | **Severidad:** mayor | **Tipo:** borde
- **Precondiciones:** Estar en https://minimoda-navy.vercel.app/registro con el formulario de registro visible (recargar si hace falta).
- **Pasos:**
  1. Completar Nombre — datos: `Prueba QA`
  2. Completar Email — datos: `qa.prueba+mm007@example.com`
  3. Completar Contraseña y Confirmar — datos: `Segura123`
  4. Completar Edad — datos: `121`
  5. Seleccionar País — datos: `Bolivia`
  6. Marcar términos
  7. Clic en «Crear cuenta»
- **Resultado esperado final:** Banner «Revisá los campos marcados.» Bajo edad: «La edad debe estar entre 13 y 120.» No se crea la cuenta.

## MM-008 — Registro: sin aceptar términos
- **Suite:** Registro – País y términos
- **Prioridad:** alta | **Severidad:** mayor | **Tipo:** negativo
- **Precondiciones:** Estar en https://minimoda-navy.vercel.app/registro con el formulario de registro visible (recargar si hace falta).
- **Pasos:**
  1. Completar Nombre — datos: `Prueba QA`
  2. Completar Email — datos: `qa.prueba+mm008@example.com`
  3. Completar Contraseña y Confirmar — datos: `Segura123`
  4. Completar Edad — datos: `25`
  5. Seleccionar País — datos: `Bolivia`
  6. Dejar checkbox de términos sin marcar
  7. Clic en «Crear cuenta»
- **Resultado esperado final:** Banner «Revisá los campos marcados.» Mensaje «Debés aceptar los términos.» No se crea la cuenta.

## MM-009 — Registro: contraseña exactamente 8 caracteres (acepta)
- **Suite:** Registro – Contraseña
- **Prioridad:** alta | **Severidad:** mayor | **Tipo:** borde
- **Precondiciones:** Estar en https://minimoda-navy.vercel.app/registro con el formulario de registro visible (recargar si hace falta).
- **Pasos:**
  1. Completar Nombre — datos: `Prueba QA`
  2. Completar Email — datos: `qa.prueba+mm009@example.com`
  3. Completar Contraseña — datos: `Abcdef12`
  4. Completar Confirmar — datos: `Abcdef12`
  5. Completar Edad — datos: `25`
  6. Seleccionar País — datos: `Bolivia`
  7. Marcar términos
  8. Clic en «Crear cuenta»
- **Resultado esperado final:** Alta exitosa según regla documentada (mínimo 8). Banner «¡Registro exitoso! Bienvenido/a a MiniModa, Prueba QA. Te enviamos un email de bienvenida (ver Bandeja).»

## MM-010 — Registro: contraseña sin números (≥8)
- **Suite:** Registro – Contraseña
- **Prioridad:** media | **Severidad:** menor | **Tipo:** borde
- **Precondiciones:** Estar en https://minimoda-navy.vercel.app/registro con el formulario de registro visible (recargar si hace falta).
- **Pasos:**
  1. Completar Nombre — datos: `Prueba QA`
  2. Completar Email — datos: `qa.prueba+mm010@example.com`
  3. Completar Contraseña — datos: `SoloLetras`
  4. Completar Confirmar — datos: `SoloLetras`
  5. Completar Edad — datos: `25`
  6. Seleccionar País — datos: `Bolivia`
  7. Marcar términos
  8. Clic en «Crear cuenta»
- **Resultado esperado final:** Se acepta según la regla documentada («Mínimo 8 caracteres.»; no exige números). Verificar: alta exitosa o mensaje adicional si hubiera otra regla no documentada.

## MM-011 — Registro: contraseña sin mayúsculas (≥8)
- **Suite:** Registro – Contraseña
- **Prioridad:** media | **Severidad:** menor | **Tipo:** borde
- **Precondiciones:** Estar en https://minimoda-navy.vercel.app/registro con el formulario de registro visible (recargar si hace falta).
- **Pasos:**
  1. Completar Nombre — datos: `Prueba QA`
  2. Completar Email — datos: `qa.prueba+mm011@example.com`
  3. Completar Contraseña — datos: `segura123`
  4. Completar Confirmar — datos: `segura123`
  5. Completar Edad — datos: `25`
  6. Seleccionar País — datos: `Bolivia`
  7. Marcar términos
  8. Clic en «Crear cuenta»
- **Resultado esperado final:** Se acepta según la regla documentada (mínimo 8; no exige mayúsculas). Verificar: alta exitosa.

## MM-012 — Registro: contraseña con espacios (≥8)
- **Suite:** Registro – Contraseña
- **Prioridad:** media | **Severidad:** menor | **Tipo:** borde
- **Precondiciones:** Estar en https://minimoda-navy.vercel.app/registro con el formulario de registro visible (recargar si hace falta).
- **Pasos:**
  1. Completar Nombre — datos: `Prueba QA`
  2. Completar Email — datos: `qa.prueba+mm012@example.com`
  3. Completar Contraseña — datos: `Segura 12`
  4. Completar Confirmar — datos: `Segura 12`
  5. Completar Edad — datos: `25`
  6. Seleccionar País — datos: `Bolivia`
  7. Marcar términos
  8. Clic en «Crear cuenta»
- **Resultado esperado final:** Se acepta según la regla documentada (mínimo 8; no prohíbe espacios). Verificar: alta exitosa o rechazo si el sistema trimea/rechaza espacios.

## MM-013 — Registro: contraseña muy larga (256 caracteres)
- **Suite:** Registro – Contraseña
- **Prioridad:** media | **Severidad:** menor | **Tipo:** borde
- **Precondiciones:** Estar en https://minimoda-navy.vercel.app/registro con el formulario de registro visible (recargar si hace falta).
- **Pasos:**
  1. Completar Nombre — datos: `Prueba QA`
  2. Completar Email — datos: `qa.prueba+mm013@example.com`
  3. Completar Contraseña — datos: `AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA`
  4. Completar Confirmar — datos: `AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA`
  5. Completar Edad — datos: `25`
  6. Seleccionar País — datos: `Bolivia`
  7. Marcar términos
  8. Clic en «Crear cuenta»
- **Resultado esperado final:** Se acepta según la regla documentada (solo mínimo 8; sin máximo documentado). Verificar: alta exitosa o límite máximo no documentado (mensaje exacto a confirmar).

## MM-014 — Registro: contraseña solo espacios (8 espacios)
- **Suite:** Registro – Contraseña
- **Prioridad:** media | **Severidad:** mayor | **Tipo:** negativo
- **Precondiciones:** Estar en https://minimoda-navy.vercel.app/registro con el formulario de registro visible (recargar si hace falta).
- **Pasos:**
  1. Completar Nombre — datos: `Prueba QA`
  2. Completar Email — datos: `qa.prueba+mm014@example.com`
  3. Completar Contraseña — datos: `        `
  4. Completar Confirmar — datos: `        `
  5. Completar Edad — datos: `25`
  6. Seleccionar País — datos: `Bolivia`
  7. Marcar términos
  8. Clic en «Crear cuenta»
- **Resultado esperado final:** Comportamiento a verificar: rechazo como vacía/obligatoria («La contraseña es obligatoria.») o aceptación por longitud ≥8. No inventar mensaje; documentar lo observado.

## MM-015 — Registro: confirmación de contraseña vacía
- **Suite:** Registro – Contraseña
- **Prioridad:** alta | **Severidad:** mayor | **Tipo:** negativo
- **Precondiciones:** Estar en https://minimoda-navy.vercel.app/registro con el formulario de registro visible (recargar si hace falta).
- **Pasos:**
  1. Completar Nombre — datos: `Prueba QA`
  2. Completar Email — datos: `qa.prueba+mm015@example.com`
  3. Completar Contraseña — datos: `Segura123`
  4. Dejar Confirmar contraseña vacío
  5. Completar Edad — datos: `25`
  6. Seleccionar País — datos: `Bolivia`
  7. Marcar términos
  8. Clic en «Crear cuenta»
- **Resultado esperado final:** Banner «Revisá los campos marcados.» Mensaje «Confirmá tu contraseña.» No se crea la cuenta.

## MM-016 — Registro: edad 13 (límite inferior inclusive)
- **Suite:** Registro – Edad
- **Prioridad:** alta | **Severidad:** mayor | **Tipo:** borde
- **Precondiciones:** Estar en https://minimoda-navy.vercel.app/registro con el formulario de registro visible (recargar si hace falta).
- **Pasos:**
  1. Completar Nombre — datos: `Prueba QA`
  2. Completar Email — datos: `qa.prueba+mm016@example.com`
  3. Completar Contraseña y Confirmar — datos: `Segura123`
  4. Completar Edad — datos: `13`
  5. Seleccionar País — datos: `Bolivia`
  6. Marcar términos
  7. Clic en «Crear cuenta»
- **Resultado esperado final:** Alta exitosa. Banner «¡Registro exitoso! Bienvenido/a a MiniModa, Prueba QA. Te enviamos un email de bienvenida (ver Bandeja).»

## MM-017 — Registro: edad 120 (límite superior inclusive)
- **Suite:** Registro – Edad
- **Prioridad:** alta | **Severidad:** mayor | **Tipo:** borde
- **Precondiciones:** Estar en https://minimoda-navy.vercel.app/registro con el formulario de registro visible (recargar si hace falta).
- **Pasos:**
  1. Completar Nombre — datos: `Prueba QA`
  2. Completar Email — datos: `qa.prueba+mm017@example.com`
  3. Completar Contraseña y Confirmar — datos: `Segura123`
  4. Completar Edad — datos: `120`
  5. Seleccionar País — datos: `Bolivia`
  6. Marcar términos
  7. Clic en «Crear cuenta»
- **Resultado esperado final:** Alta exitosa. Banner «¡Registro exitoso! Bienvenido/a a MiniModa, Prueba QA. Te enviamos un email de bienvenida (ver Bandeja).»

## MM-018 — Registro: edad 0
- **Suite:** Registro – Edad
- **Prioridad:** media | **Severidad:** mayor | **Tipo:** negativo
- **Precondiciones:** Estar en https://minimoda-navy.vercel.app/registro con el formulario de registro visible (recargar si hace falta).
- **Pasos:**
  1. Completar Nombre — datos: `Prueba QA`
  2. Completar Email — datos: `qa.prueba+mm018@example.com`
  3. Completar Contraseña y Confirmar — datos: `Segura123`
  4. Completar Edad — datos: `0`
  5. Seleccionar País — datos: `Bolivia`
  6. Marcar términos
  7. Clic en «Crear cuenta»
- **Resultado esperado final:** Banner «Revisá los campos marcados.» «La edad debe estar entre 13 y 120.» No se crea la cuenta.

## MM-019 — Registro: edad negativa
- **Suite:** Registro – Edad
- **Prioridad:** media | **Severidad:** mayor | **Tipo:** negativo
- **Precondiciones:** Estar en https://minimoda-navy.vercel.app/registro con el formulario de registro visible (recargar si hace falta).
- **Pasos:**
  1. Completar Nombre — datos: `Prueba QA`
  2. Completar Email — datos: `qa.prueba+mm019@example.com`
  3. Completar Contraseña y Confirmar — datos: `Segura123`
  4. Completar Edad — datos: `-5`
  5. Seleccionar País — datos: `Bolivia`
  6. Marcar términos
  7. Clic en «Crear cuenta»
- **Resultado esperado final:** Banner «Revisá los campos marcados.» «La edad debe estar entre 13 y 120.» (o rechazo de no entero; mensaje exacto a confirmar si difiere). No se crea la cuenta.

## MM-020 — Registro: edad decimal 13.5
- **Suite:** Registro – Edad
- **Prioridad:** media | **Severidad:** mayor | **Tipo:** borde
- **Precondiciones:** Estar en https://minimoda-navy.vercel.app/registro con el formulario de registro visible (recargar si hace falta).
- **Pasos:**
  1. Completar Nombre — datos: `Prueba QA`
  2. Completar Email — datos: `qa.prueba+mm020@example.com`
  3. Completar Contraseña y Confirmar — datos: `Segura123`
  4. Completar Edad — datos: `13.5`
  5. Seleccionar País — datos: `Bolivia`
  6. Marcar términos
  7. Clic en «Crear cuenta»
- **Resultado esperado final:** Rechazo: la edad debe ser número entero entre 13 y 120 (helper). Mensaje exacto a confirmar (posible «La edad debe estar entre 13 y 120.» u otro). No se crea la cuenta.

## MM-021 — Registro: edad no numérica «abc»
- **Suite:** Registro – Edad
- **Prioridad:** media | **Severidad:** mayor | **Tipo:** negativo
- **Precondiciones:** Estar en https://minimoda-navy.vercel.app/registro con el formulario de registro visible (recargar si hace falta).
- **Pasos:**
  1. Completar Nombre — datos: `Prueba QA`
  2. Completar Email — datos: `qa.prueba+mm021@example.com`
  3. Completar Contraseña y Confirmar — datos: `Segura123`
  4. Intentar Completar Edad — datos: `abc`
  5. Seleccionar País — datos: `Bolivia`
  6. Marcar términos
  7. Clic en «Crear cuenta»
- **Resultado esperado final:** No se acepta valor no numérico (campo bloquea o muestra error). Si llega a enviar: banner «Revisá los campos marcados.» y mensaje de edad inválida/obligatoria (mensaje exacto a confirmar). No se crea la cuenta.

## MM-022 — Registro: edad vacía
- **Suite:** Registro – Edad
- **Prioridad:** alta | **Severidad:** mayor | **Tipo:** negativo
- **Precondiciones:** Estar en https://minimoda-navy.vercel.app/registro con el formulario de registro visible (recargar si hace falta).
- **Pasos:**
  1. Completar Nombre — datos: `Prueba QA`
  2. Completar Email — datos: `qa.prueba+mm022@example.com`
  3. Completar Contraseña y Confirmar — datos: `Segura123`
  4. Dejar Edad vacía
  5. Seleccionar País — datos: `Bolivia`
  6. Marcar términos
  7. Clic en «Crear cuenta»
- **Resultado esperado final:** Banner «Revisá los campos marcados.» «La edad es obligatoria.» No se crea la cuenta.

## MM-023 — Registro: email vacío
- **Suite:** Registro – Email
- **Prioridad:** alta | **Severidad:** mayor | **Tipo:** negativo
- **Precondiciones:** Estar en https://minimoda-navy.vercel.app/registro con el formulario de registro visible (recargar si hace falta).
- **Pasos:**
  1. Completar Nombre — datos: `Prueba QA`
  2. Dejar Email vacío
  3. Completar Contraseña y Confirmar — datos: `Segura123`
  4. Completar Edad — datos: `25`
  5. Seleccionar País — datos: `Bolivia`
  6. Marcar términos
  7. Clic en «Crear cuenta»
- **Resultado esperado final:** Banner «Revisá los campos marcados.» «El email es obligatorio.» No se crea la cuenta.

## MM-024 — Registro: email ya registrado (no se puede repetir)
- **Suite:** Registro – Email
- **Prioridad:** alta | **Severidad:** crítica | **Tipo:** negativo
- **Precondiciones:** Estar en https://minimoda-navy.vercel.app/registro con el formulario de registro visible (recargar si hace falta). Haber registrado previamente el email qa.prueba+dup@example.com (o usar uno ya existente).
- **Pasos:**
  1. Completar Nombre — datos: `Prueba QA`
  2. Completar Email — datos: `qa.prueba+dup@example.com`
  3. Completar Contraseña y Confirmar — datos: `Segura123`
  4. Completar Edad — datos: `25`
  5. Seleccionar País — datos: `Bolivia`
  6. Marcar términos
  7. Clic en «Crear cuenta»
- **Resultado esperado final:** No se crea una segunda cuenta. Se muestra error de email duplicado/ya registrado (mensaje exacto a confirmar).

## MM-025 — Registro: email con espacios al inicio/fin
- **Suite:** Registro – Email
- **Prioridad:** media | **Severidad:** menor | **Tipo:** borde
- **Precondiciones:** Estar en https://minimoda-navy.vercel.app/registro con el formulario de registro visible (recargar si hace falta).
- **Pasos:**
  1. Completar Nombre — datos: `Prueba QA`
  2. Completar Email — datos: `  qa.prueba+mm025@example.com  `
  3. Completar Contraseña y Confirmar — datos: `Segura123`
  4. Completar Edad — datos: `25`
  5. Seleccionar País — datos: `Bolivia`
  6. Marcar términos
  7. Clic en «Crear cuenta»
- **Resultado esperado final:** Verificar: el sistema trimea y acepta, o rechaza como inválido (mensaje exacto a confirmar). Documentar comportamiento real.

## MM-026 — Registro: email sin dominio
- **Suite:** Registro – Email
- **Prioridad:** alta | **Severidad:** mayor | **Tipo:** negativo
- **Precondiciones:** Estar en https://minimoda-navy.vercel.app/registro con el formulario de registro visible (recargar si hace falta).
- **Pasos:**
  1. Completar Nombre — datos: `Prueba QA`
  2. Completar Email — datos: `usuario@`
  3. Completar Contraseña y Confirmar — datos: `Segura123`
  4. Completar Edad — datos: `25`
  5. Seleccionar País — datos: `Bolivia`
  6. Marcar términos
  7. Clic en «Crear cuenta»
- **Resultado esperado final:** No se crea la cuenta. Error de formato de email (mensaje exacto a confirmar).

## MM-027 — Registro: email con doble @
- **Suite:** Registro – Email
- **Prioridad:** media | **Severidad:** mayor | **Tipo:** negativo
- **Precondiciones:** Estar en https://minimoda-navy.vercel.app/registro con el formulario de registro visible (recargar si hace falta).
- **Pasos:**
  1. Completar Nombre — datos: `Prueba QA`
  2. Completar Email — datos: `usuario@@example.com`
  3. Completar Contraseña y Confirmar — datos: `Segura123`
  4. Completar Edad — datos: `25`
  5. Seleccionar País — datos: `Bolivia`
  6. Marcar términos
  7. Clic en «Crear cuenta»
- **Resultado esperado final:** No se crea la cuenta. Error de formato de email (mensaje exacto a confirmar).

## MM-028 — Registro: email duplicado por mayúsculas/minúsculas
- **Suite:** Registro – Email
- **Prioridad:** media | **Severidad:** mayor | **Tipo:** borde
- **Precondiciones:** Estar en https://minimoda-navy.vercel.app/registro con el formulario de registro visible (recargar si hace falta). Haber registrado previamente qa.prueba+case@example.com.
- **Pasos:**
  1. Completar Nombre — datos: `Prueba QA`
  2. Completar Email — datos: `QA.Prueba+Case@Example.com`
  3. Completar Contraseña y Confirmar — datos: `Segura123`
  4. Completar Edad — datos: `25`
  5. Seleccionar País — datos: `Bolivia`
  6. Marcar términos
  7. Clic en «Crear cuenta»
- **Resultado esperado final:** Verificar si el email se trata case-insensitive: rechazo por duplicado (mensaje exacto a confirmar) o alta distinta. Documentar.

## MM-029 — Registro: nombre vacío
- **Suite:** Registro – Nombre
- **Prioridad:** alta | **Severidad:** mayor | **Tipo:** negativo
- **Precondiciones:** Estar en https://minimoda-navy.vercel.app/registro con el formulario de registro visible (recargar si hace falta).
- **Pasos:**
  1. Dejar Nombre vacío
  2. Completar Email — datos: `qa.prueba+mm029@example.com`
  3. Completar Contraseña y Confirmar — datos: `Segura123`
  4. Completar Edad — datos: `25`
  5. Seleccionar País — datos: `Bolivia`
  6. Marcar términos
  7. Clic en «Crear cuenta»
- **Resultado esperado final:** Banner «Revisá los campos marcados.» «El nombre es obligatorio.» No se crea la cuenta.

## MM-030 — Registro: nombre solo espacios
- **Suite:** Registro – Nombre
- **Prioridad:** media | **Severidad:** mayor | **Tipo:** negativo
- **Precondiciones:** Estar en https://minimoda-navy.vercel.app/registro con el formulario de registro visible (recargar si hace falta).
- **Pasos:**
  1. Completar Nombre — datos: `     `
  2. Completar Email — datos: `qa.prueba+mm030@example.com`
  3. Completar Contraseña y Confirmar — datos: `Segura123`
  4. Completar Edad — datos: `25`
  5. Seleccionar País — datos: `Bolivia`
  6. Marcar términos
  7. Clic en «Crear cuenta»
- **Resultado esperado final:** Verificar rechazo como vacío («El nombre es obligatorio.») u otro mensaje (mensaje exacto a confirmar). No se debería crear cuenta con nombre en blanco.

## MM-031 — Registro: nombre muy largo (255+ caracteres)
- **Suite:** Registro – Nombre
- **Prioridad:** baja | **Severidad:** menor | **Tipo:** borde
- **Precondiciones:** Estar en https://minimoda-navy.vercel.app/registro con el formulario de registro visible (recargar si hace falta).
- **Pasos:**
  1. Completar Nombre — datos: `NNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNN`
  2. Completar Email — datos: `qa.prueba+mm031@example.com`
  3. Completar Contraseña y Confirmar — datos: `Segura123`
  4. Completar Edad — datos: `25`
  5. Seleccionar País — datos: `Bolivia`
  6. Marcar términos
  7. Clic en «Crear cuenta»
- **Resultado esperado final:** Verificar: aceptación, truncado o error de longitud máxima (mensaje exacto a confirmar). Documentar límite real.

## MM-032 — Registro: nombre con acentos, ñ y caracteres especiales
- **Suite:** Registro – Nombre
- **Prioridad:** media | **Severidad:** menor | **Tipo:** borde
- **Precondiciones:** Estar en https://minimoda-navy.vercel.app/registro con el formulario de registro visible (recargar si hace falta).
- **Pasos:**
  1. Completar Nombre — datos: `María José Ñandú-Pérez`
  2. Completar Email — datos: `qa.prueba+mm032@example.com`
  3. Completar Contraseña y Confirmar — datos: `Segura123`
  4. Completar Edad — datos: `25`
  5. Seleccionar País — datos: `Bolivia`
  6. Marcar términos
  7. Clic en «Crear cuenta»
- **Resultado esperado final:** Alta exitosa esperada (UTF-8). Banner «¡Registro exitoso! Bienvenido/a a MiniModa, María José Ñandú-Pérez. Te enviamos un email de bienvenida (ver Bandeja).» Verificar que el nombre se muestre intacto.

## MM-033 — Registro: nombre con inyección HTML/script
- **Suite:** Registro – Nombre
- **Prioridad:** alta | **Severidad:** crítica | **Tipo:** negativo
- **Precondiciones:** Estar en https://minimoda-navy.vercel.app/registro con el formulario de registro visible (recargar si hace falta).
- **Pasos:**
  1. Completar Nombre — datos: `<script>alert(1)</script><b>XSS</b>`
  2. Completar Email — datos: `qa.prueba+mm033@example.com`
  3. Completar Contraseña y Confirmar — datos: `Segura123`
  4. Completar Edad — datos: `25`
  5. Seleccionar País — datos: `Bolivia`
  6. Marcar términos
  7. Clic en «Crear cuenta»
- **Resultado esperado final:** Si se acepta el alta, el nombre debe mostrarse escapado (sin ejecutar script ni renderizar HTML). Verificar en banner y Bandeja. Rechazo también es válido (mensaje exacto a confirmar).

## MM-034 — Registro: país sin seleccionar
- **Suite:** Registro – País y términos
- **Prioridad:** alta | **Severidad:** mayor | **Tipo:** negativo
- **Precondiciones:** Estar en https://minimoda-navy.vercel.app/registro con el formulario de registro visible (recargar si hace falta).
- **Pasos:**
  1. Completar Nombre — datos: `Prueba QA`
  2. Completar Email — datos: `qa.prueba+mm034@example.com`
  3. Completar Contraseña y Confirmar — datos: `Segura123`
  4. Completar Edad — datos: `25`
  5. Dejar País sin seleccionar
  6. Marcar términos
  7. Clic en «Crear cuenta»
- **Resultado esperado final:** Banner «Revisá los campos marcados.» «Seleccioná un país.» No se crea la cuenta.

## MM-035 — Registro: cada país válido del select (9 opciones)
- **Suite:** Registro – País y términos
- **Prioridad:** media | **Severidad:** menor | **Tipo:** positivo
- **Precondiciones:** Estar en https://minimoda-navy.vercel.app/registro con el formulario de registro visible (recargar si hace falta). Identificar las 9 opciones del select (incl. Bolivia); nombres exactos a confirmar en el formulario.
- **Pasos:**
  1. Para cada una de las 9 opciones de País: completar datos válidos únicos (email distinto)
  2. Seleccionar el país bajo prueba
  3. Marcar términos y clic en «Crear cuenta»
- **Resultado esperado final:** Para cada país: alta exitosa con banner «¡Registro exitoso! Bienvenido/a a MiniModa, <nombre>. Te enviamos un email de bienvenida (ver Bandeja).»

## MM-036 — Registro: doble clic en «Crear cuenta»
- **Suite:** Registro – Flujo general
- **Prioridad:** media | **Severidad:** mayor | **Tipo:** borde
- **Precondiciones:** Estar en https://minimoda-navy.vercel.app/registro con el formulario de registro visible (recargar si hace falta).
- **Pasos:**
  1. Completar todos los campos con datos válidos — datos: `email=qa.prueba+mm036@example.com`
  2. Hacer doble clic rápido en «Crear cuenta»
- **Resultado esperado final:** Se crea una sola cuenta (o se deshabilita el botón tras el primer clic). No debe haber doble alta ni error por duplicado del mismo intento. Verificar.

## MM-037 — Registro: corrección de error y reenvío exitoso
- **Suite:** Registro – Flujo general
- **Prioridad:** alta | **Severidad:** mayor | **Tipo:** positivo
- **Precondiciones:** Estar en https://minimoda-navy.vercel.app/registro con el formulario de registro visible (recargar si hace falta).
- **Pasos:**
  1. Enviar con Edad=12 y resto válido — datos: `email=qa.prueba+mm037@example.com`
  2. Observar error «La edad debe estar entre 13 y 120.»
  3. Corregir Edad a 25
  4. Clic de nuevo en «Crear cuenta»
- **Resultado esperado final:** Tras corregir, desaparece el error y se muestra el banner de alta exitosa. No quedan mensajes de validación previos.

## MM-038 — Registro: bandeja de bienvenida tras alta exitosa
- **Suite:** Registro – Flujo general
- **Prioridad:** media | **Severidad:** menor | **Tipo:** positivo
- **Precondiciones:** Estar en https://minimoda-navy.vercel.app/registro con el formulario de registro visible (recargar si hace falta).
- **Pasos:**
  1. Completar alta válida — datos: `email=qa.prueba+mm038@example.com; nombre=Prueba QA`
  2. Clic en «Crear cuenta» y observar banner de éxito
  3. Abrir/consultar la Bandeja referida en el mensaje de éxito
- **Resultado esperado final:** Tras el alta, el mensaje menciona «ver Bandeja». En Bandeja debe aparecer el email de bienvenida asociado al registro (contenido exacto a confirmar).

## MM-039 — Registro: contraseña vacía con resto válido
- **Suite:** Registro – Contraseña
- **Prioridad:** alta | **Severidad:** mayor | **Tipo:** negativo
- **Precondiciones:** Estar en https://minimoda-navy.vercel.app/registro con el formulario de registro visible (recargar si hace falta).
- **Pasos:**
  1. Completar Nombre — datos: `Prueba QA`
  2. Completar Email — datos: `qa.prueba+mm039@example.com`
  3. Dejar Contraseña vacía
  4. Dejar Confirmar vacía o con valor
  5. Completar Edad — datos: `25`
  6. Seleccionar País — datos: `Bolivia`
  7. Marcar términos
  8. Clic en «Crear cuenta»
- **Resultado esperado final:** Banner «Revisá los campos marcados.» «La contraseña es obligatoria.» (y posiblemente «Confirmá tu contraseña.»). No se crea la cuenta.

## MM-040 — Registro: email sin TLD (usuario@dominio)
- **Suite:** Registro – Email
- **Prioridad:** baja | **Severidad:** menor | **Tipo:** borde
- **Precondiciones:** Estar en https://minimoda-navy.vercel.app/registro con el formulario de registro visible (recargar si hace falta).
- **Pasos:**
  1. Completar Nombre — datos: `Prueba QA`
  2. Completar Email — datos: `usuario@dominio`
  3. Completar Contraseña y Confirmar — datos: `Segura123`
  4. Completar Edad — datos: `25`
  5. Seleccionar País — datos: `Bolivia`
  6. Marcar términos
  7. Clic en «Crear cuenta»
- **Resultado esperado final:** Verificar si se acepta o se rechaza por formato (mensaje exacto a confirmar). Documentar regla real del formulario.
