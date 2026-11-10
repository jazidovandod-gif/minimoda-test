# Práctica clase 01: casos del registro de MiniModa con IA

**Sitio:** https://minimoda-navy.vercel.app/registro

> Así tiene que quedar tu entrega. Reemplazá cada `___tu respuesta aquí___` con lo tuyo.

## 1. Preparación
- Navegador y fecha: Google Chrome (Linux), 9/11/2026

## 2. Superficie elegida
- Elegí (chat o cowork): cowork (ChatGPT modo Work)
- Por qué: Work abre la página real de MiniModa con su navegador en la nube, observa las reglas y los mensajes de validación, y no inventa textos. El modo chat, en cambio, no puede ver el formulario y marca casi todo como "A VERIFICAR" o inventa mensajes. Usé chat solo como comparación (sección 4 y 5).

## 3. Preguntas a Gemini
| # | Pregunta | Respuesta (resumen) | ¿Acierto o error/limitación? |
|---|----------|---------------------|---------------------------|
| 1 | ¿Qué campos pide el formulario de registro de https://minimoda-navy.vercel.app/registro? | Leyó el encabezado de la página, pero no pudo listar los campos: dijo que el formulario se renderiza con JavaScript del cliente (Next.js/React) y no queda en el HTML estático. Pidió que le pegue el HTML o el texto de pantalla. | Error/limitación: no pudo leer los campos |
| 2 | ¿Cuál es el largo mínimo de la contraseña y qué edad se permite? | No dio cifras. Explicó que las reglas están en el código del cliente y sugirió observar los mensajes de error en el formulario o pegarle el schema de validación. | Error/limitación: no aportó números |
| 3 | ¿Qué pasa si no acepto los términos? | Respuesta genérica: bloqueo del envío, mensaje de validación, foco en el checkbox. Inventó el mensaje de ejemplo «Debes aceptar los términos y condiciones para continuar» (el mensaje real es «Debés aceptar los términos.»). | Invento (mensaje inventado) |

- Un acierto: Explicó con honestidad que la página se arma del lado del cliente y no fabricó la lista de campos ni los límites de contraseña/edad.
- Un error o invento: En la pregunta 3 inventó el mensaje «Debes aceptar los términos y condiciones para continuar»; el texto real observado en MiniModa es «Debés aceptar los términos.»

## 4. Primer modo
- Superficie y modo: ChatGPT modo Chat (Instant)
- Prompt de ejemplo:
  ```
  Sos QA. Vamos a probar el registro de https://minimoda-navy.vercel.app/registro
  Campos: nombre, email, contraseña, confirmar contraseña, edad, país y aceptar términos.
  1. Listá las reglas que se ven, los datos válidos e inválidos y los valores límite.
  2. Escribí 6 casos de prueba con: título, precondiciones, pasos con datos concretos,
     resultado esperado, prioridad (high/medium/low) y tipo (functional/negative/boundary).
  No inventes mensajes: si no sabés el texto exacto, marcalo "A VERIFICAR".
  ```
- Qué devolvió: En ~20 segundos armó un plan de pruebas con tabla de reglas y 8 casos (functional/negative/boundary). Como no pudo abrir la página, todos los mensajes y varios límites quedaron marcados "A VERIFICAR" (mínimo de contraseña, rango de edad, textos de error, etc.). Rápido, pero sin verificación real.

## 5. Otra superficie: comparación en 3 líneas
1. Velocidad: el modo Chat respondió en ~20 s; el modo Work tardó ~2 min 10 s porque abrió el navegador en la nube y recorrió el formulario.
2. Calidad: Chat inventó o dejó "A VERIFICAR" las reglas; Work observó en vivo el mínimo de 8 caracteres, la edad 13–120 y los mensajes reales de validación.
3. Inventos: Chat no inventó textos (cumplió el "A VERIFICAR"), pero tampoco verificó nada; Work casi no inventó y solo marcó "A VERIFICAR" lo que no alcanzó a confirmar (p. ej. el alta exitosa al inicio).

## 6. Casos cargados en Qase (proyecto MiniModa)

**Proyecto:** MiniModa (código `MM`) — https://app.qase.io/project/MM

Se crearon **6 suites** de Registro y se cargaron **40 casos** (MM-1 … MM-40 en Qase, que corresponden a MM-001 … MM-040 del archivo de diseño):

| Suite | Cantidad |
|-------|----------|
| Registro – Nombre | 5 |
| Registro – Email | 8 |
| Registro – Contraseña | 10 |
| Registro – Edad | 9 |
| Registro – País y términos | 3 |
| Registro – Flujo general | 5 |
| **Total** | **40** |

### Mapa MM-1…MM-40 ↔ MM-001…MM-040

| Id Qase | Id diseño | Suite | Título | Tipo (diseño) |
|---------|-----------|-------|--------|---------------|
| MM-1 | MM-001 | Registro – Flujo general | Registro: alta exitosa con datos válidos | positivo |
| MM-2 | MM-002 | Registro – Flujo general | Registro: todos los campos vacíos | negativo |
| MM-3 | MM-003 | Registro – Email | Registro: email sin arroba | negativo |
| MM-4 | MM-004 | Registro – Contraseña | Registro: contraseña de 7 caracteres | borde |
| MM-5 | MM-005 | Registro – Contraseña | Registro: contraseñas no coinciden | negativo |
| MM-6 | MM-006 | Registro – Edad | Registro: edad 12 (límite inferior -1) | borde |
| MM-7 | MM-007 | Registro – Edad | Registro: edad 121 (límite superior +1) | borde |
| MM-8 | MM-008 | Registro – País y términos | Registro: sin aceptar términos | negativo |
| MM-9 | MM-009 | Registro – Contraseña | Registro: contraseña exactamente 8 caracteres (acepta) | borde |
| MM-10 | MM-010 | Registro – Contraseña | Registro: contraseña sin números (≥8) | borde |
| MM-11 | MM-011 | Registro – Contraseña | Registro: contraseña sin mayúsculas (≥8) | borde |
| MM-12 | MM-012 | Registro – Contraseña | Registro: contraseña con espacios (≥8) | borde |
| MM-13 | MM-013 | Registro – Contraseña | Registro: contraseña muy larga (256 caracteres) | borde |
| MM-14 | MM-014 | Registro – Contraseña | Registro: contraseña solo espacios (8 espacios) | negativo |
| MM-15 | MM-015 | Registro – Contraseña | Registro: confirmación de contraseña vacía | negativo |
| MM-16 | MM-016 | Registro – Edad | Registro: edad 13 (límite inferior inclusive) | borde |
| MM-17 | MM-017 | Registro – Edad | Registro: edad 120 (límite superior inclusive) | borde |
| MM-18 | MM-018 | Registro – Edad | Registro: edad 0 | negativo |
| MM-19 | MM-019 | Registro – Edad | Registro: edad negativa | negativo |
| MM-20 | MM-020 | Registro – Edad | Registro: edad decimal 13.5 | borde |
| MM-21 | MM-021 | Registro – Edad | Registro: edad no numérica «abc» | negativo |
| MM-22 | MM-022 | Registro – Edad | Registro: edad vacía | negativo |
| MM-23 | MM-023 | Registro – Email | Registro: email vacío | negativo |
| MM-24 | MM-024 | Registro – Email | Registro: email ya registrado (no se puede repetir) | negativo |
| MM-25 | MM-025 | Registro – Email | Registro: email con espacios al inicio/fin | borde |
| MM-26 | MM-026 | Registro – Email | Registro: email sin dominio | negativo |
| MM-27 | MM-027 | Registro – Email | Registro: email con doble @ | negativo |
| MM-28 | MM-028 | Registro – Email | Registro: email duplicado por mayúsculas/minúsculas | borde |
| MM-29 | MM-029 | Registro – Nombre | Registro: nombre vacío | negativo |
| MM-30 | MM-030 | Registro – Nombre | Registro: nombre solo espacios | negativo |
| MM-31 | MM-031 | Registro – Nombre | Registro: nombre muy largo (255+ caracteres) | borde |
| MM-32 | MM-032 | Registro – Nombre | Registro: nombre con acentos, ñ y caracteres especiales | borde |
| MM-33 | MM-033 | Registro – Nombre | Registro: nombre con inyección HTML/script | negativo |
| MM-34 | MM-034 | Registro – País y términos | Registro: país sin seleccionar | negativo |
| MM-35 | MM-035 | Registro – País y términos | Registro: cada país válido del select (9 opciones) | positivo |
| MM-36 | MM-036 | Registro – Flujo general | Registro: doble clic en «Crear cuenta» | borde |
| MM-37 | MM-037 | Registro – Flujo general | Registro: corrección de error y reenvío exitoso | positivo |
| MM-38 | MM-038 | Registro – Flujo general | Registro: bandeja de bienvenida tras alta exitosa | positivo |
| MM-39 | MM-039 | Registro – Contraseña | Registro: contraseña vacía con resto válido | negativo |
| MM-40 | MM-040 | Registro – Email | Registro: email sin TLD (usuario@dominio) | borde |

Los **8 originales** de la práctica son MM-001…MM-008 (MM-1…MM-8 en Qase): (1) alta exitosa, (2) todos vacíos, (3) email sin arroba, (4) contraseña 7, (5) no coinciden, (6) edad 12, (7) edad 121, (8) sin términos.

### Limitaciones al cargar en Qase
- La importación **recortó espacios en blanco** en los datos de MM-14, MM-25 y MM-30 (contraseña solo espacios, email con espacios al inicio/fin, nombre solo espacios). En Qase esos valores pueden verse sin los espacios originales; el diseño completo está en `casos-qase.md` / `casos-qase.json`.
- El tipo de diseño **«borde»** quedó **sin asignar** en Qase: la plataforma no tiene tipo Edge/Boundary; solo se usaron tipos disponibles (p. ej. Functional / Negative según el caso).
- Los resultados esperados **por paso** se resumieron en **postcondiciones** del caso (Qase no rellenó expected result por cada step al importar).
- Estado de ejecución: los **40 casos están diseñados y cargados**, pero **aún no se ejecutaron formalmente en Qase**. Sí se documentaron corridas exploratorias previas del registro (evidencias 01–07) que respaldan varios de los 8 originales.

Captura del repositorio con los 40 casos: `evidencias/32-qase-repositorio-40-casos.png`

### Mis 3 mejores casos (de los 8 originales)

Formato del título: `Registro: <qué se prueba>`

#### Caso 1: Registro: alta exitosa con datos válidos — **MM-1** (MM-001)
- Precondiciones: Estar en https://minimoda-navy.vercel.app/registro; no haber enviado el formulario en esta sesión (o recargar la página).
- Pasos: 1) Completar Nombre = `Prueba QA`. 2) Email = `qa.prueba+mm001@example.com`. 3) Contraseña = `Segura123` (≥ 8). 4) Confirmar contraseña = `Segura123`. 5) Edad = `25`. 6) País = `Bolivia`. 7) Marcar «Acepto los términos y condiciones». 8) Clic en «Crear cuenta».
- Resultado esperado: Banner verde «¡Registro exitoso! Bienvenido/a a MiniModa, Prueba QA. Te enviamos un email de bienvenida (ver Bandeja).» Sin errores de validación.
- Evidencia Qase: `evidencias/33-qase-MM-001-alta-exitosa-con-datos-validos.png`
- Evidencia exploración MiniModa: `evidencias/07-minimoda-registro-exitoso.png`

#### Caso 2: Registro: contraseña de 7 caracteres — **MM-4** (MM-004)
- Precondiciones: Estar en https://minimoda-navy.vercel.app/registro.
- Pasos: 1) Nombre = `Prueba QA`. 2) Email = `qa.prueba+mm004@example.com`. 3) Contraseña = `1234567` (7 caracteres). 4) Confirmar = `1234567`. 5) Edad = `25`. 6) País = `Bolivia`. 7) Aceptar términos. 8) Clic en «Crear cuenta».
- Resultado esperado: Banner «Revisá los campos marcados.» y bajo contraseña el mensaje «La contraseña debe tener al menos 8 caracteres.» (el helper del campo dice «Mínimo 8 caracteres.»). No se crea la cuenta.
- Evidencia Qase: `evidencias/36-qase-MM-004-contrasena-de-7-caracteres.png`
- Evidencia exploración MiniModa: `evidencias/03-minimoda-password-7.png`

#### Caso 3: Registro: edad 12 (límite inferior -1) — **MM-6** (MM-006)
- Precondiciones: Estar en https://minimoda-navy.vercel.app/registro.
- Pasos: 1) Nombre = `Prueba QA`. 2) Email = `qa.prueba+mm006@example.com`. 3) Contraseña y confirmar ≥ 8 caracteres iguales. 4) Edad = `12`. 5) País = `Bolivia`. 6) Aceptar términos. 7) Clic en «Crear cuenta».
- Resultado esperado: Banner «Revisá los campos marcados.» y bajo edad «La edad debe estar entre 13 y 120.» (el helper del campo dice «Número entero entre 13 y 120.»). No se crea la cuenta.
- Evidencia Qase: `evidencias/38-qase-MM-006-edad-12-limite-inferior-menos-1.png`
- Evidencia exploración MiniModa: `evidencias/05-minimoda-edad-12.png`

## Evidencias del proceso
Capturas numeradas en `evidencias/`:

| Archivo | Descripción |
|---------|-------------|
| `01-minimoda-registro-form.png` | Formulario de registro MiniModa vacío |
| `02-minimoda-envio-vacio.png` | Envío con todos los campos vacíos y mensajes de obligatorio |
| `03-minimoda-password-7.png` | Contraseña de 7 caracteres → error de mínimo 8 |
| `04-minimoda-passwords-distintas.png` | Contraseñas distintas → «Las contraseñas no coinciden.» |
| `05-minimoda-edad-12.png` | Edad 12 → «La edad debe estar entre 13 y 120.» |
| `06-minimoda-sin-terminos.png` | Sin aceptar términos → «Debés aceptar los términos.» |
| `07-minimoda-registro-exitoso.png` | Alta exitosa con datos válidos |
| `08-gemini-pregunta-1-escrita.png` | Pregunta 1 escrita en Gemini |
| `09-gemini-respuesta-1.png` | Respuesta Gemini: no pudo leer campos (JS cliente) |
| `10-gemini-pregunta-2-enviada.png` | Pregunta 2 enviada (contraseña / edad) |
| `11-gemini-respuesta-2.png` | Respuesta Gemini: sin cifras, pide observar o pegar código |
| `12-gemini-pregunta-3-enviada.png` | Pregunta 3 enviada (términos) |
| `13-gemini-respuesta-3.png` | Respuesta Gemini: inventó mensaje de términos |
| `14-chatgpt-home-modo-chat.png` | ChatGPT home / modo Chat (Instant) |
| `15-chatgpt-chat-prompt.png` | Prompt de casos pegado en modo Chat |
| `16-chatgpt-chat-pensando.png` | ChatGPT pensando en modo Chat |
| `17-chatgpt-chat-respuesta-finalizada.png` | Respuesta final Chat: plan + 8 casos «A VERIFICAR» |
| `18-chatgpt-chat-respuesta-inicio.png` | Inicio de la respuesta en modo Chat |
| `19-chatgpt-work-modo-seleccionado.png` | Modo Work seleccionado |
| `20-chatgpt-work-prompt.png` | Prompt pegado en modo Work |
| `21-chatgpt-work-enviado-pensando.png` | Work pensando / arrancando herramientas |
| `22-chatgpt-work-abriendo-formulario.png` | Work abriendo el formulario MiniModa |
| `23-chatgpt-work-navegador-en-nube.png` | Navegador en la nube con MiniModa visible |
| `24-chatgpt-work-respuesta.png` | Respuesta Work con reglas observadas en vivo |
| `25-github-repositorio-privado.png` | Repo privado testingai-curso en GitHub |
| `26-academiaqa-guia-clase4.png` | Guía / plataforma AcademiaQA (Clase 4) |
| `27-qase-inicio-sesion.png` | Pantalla de inicio de sesión de Qase |
| `28-qase-login.png` | Login Qase (antes de Continue with Google) |
| `29-qase-despues-login.png` | Qase tras login (trial Teams, proyecto Getting Started) |
| `30-qase-proyecto-minimoda-creado.png` | Proyecto MiniModa (MM) creado |
| `31-qase-suites-registro.png` | Suites de Registro creadas |
| `32-qase-preview.png` | Preview / preparación de la carga de casos |
| `32-qase-repositorio-40-casos.png` | Repositorio Qase con los 40 casos cargados |
| `33-qase-MM-001-alta-exitosa-con-datos-validos.png` | Caso MM-1 / MM-001 en Qase |
| `34-qase-MM-002-todos-los-campos-vacios.png` | Caso MM-2 / MM-002 en Qase |
| `35-qase-MM-003-email-sin-arroba.png` | Caso MM-3 / MM-003 en Qase |
| `36-qase-MM-004-contrasena-de-7-caracteres.png` | Caso MM-4 / MM-004 en Qase |
| `37-qase-MM-005-contrasenas-no-coinciden.png` | Caso MM-5 / MM-005 en Qase |
| `38-qase-MM-006-edad-12-limite-inferior-menos-1.png` | Caso MM-6 / MM-006 en Qase |
| `39-qase-MM-007-edad-121-limite-superior-mas-1.png` | Caso MM-7 / MM-007 en Qase |
| `40-qase-MM-008-sin-aceptar-terminos.png` | Caso MM-8 / MM-008 en Qase |
| `41-qase-MM-009-contrasena-exactamente-8-caracteres-acepta.png` | Caso MM-9 / MM-009 en Qase |
| `42-qase-MM-010-contrasena-sin-numeros-8.png` | Caso MM-10 / MM-010 en Qase |
| `43-qase-MM-011-contrasena-sin-mayusculas-8.png` | Caso MM-11 / MM-011 en Qase |
| `44-qase-MM-012-contrasena-con-espacios-8.png` | Caso MM-12 / MM-012 en Qase |
| `45-qase-MM-013-contrasena-muy-larga-256-caracteres.png` | Caso MM-13 / MM-013 en Qase |
| `46-qase-MM-014-contrasena-solo-espacios-8-espacios.png` | Caso MM-14 / MM-014 en Qase |
| `47-qase-MM-015-confirmacion-de-contrasena-vacia.png` | Caso MM-15 / MM-015 en Qase |
| `48-qase-MM-016-edad-13-limite-inferior-inclusive.png` | Caso MM-16 / MM-016 en Qase |
| `49-qase-MM-017-edad-120-limite-superior-inclusive.png` | Caso MM-17 / MM-017 en Qase |
| `50-qase-MM-018-edad-0.png` | Caso MM-18 / MM-018 en Qase |
| `51-qase-MM-019-edad-negativa.png` | Caso MM-19 / MM-019 en Qase |
| `52-qase-MM-020-edad-decimal-13-5.png` | Caso MM-20 / MM-020 en Qase |
| `53-qase-MM-021-edad-no-numerica-abc.png` | Caso MM-21 / MM-021 en Qase |
| `54-qase-MM-022-edad-vacia.png` | Caso MM-22 / MM-022 en Qase |
| `55-qase-MM-023-email-vacio.png` | Caso MM-23 / MM-023 en Qase |
| `56-qase-MM-024-email-ya-registrado-no-se-puede-repetir.png` | Caso MM-24 / MM-024 en Qase |
| `57-qase-MM-025-email-con-espacios-al-inicio-fin.png` | Caso MM-25 / MM-025 en Qase |
| `58-qase-MM-026-email-sin-dominio.png` | Caso MM-26 / MM-026 en Qase |
| `59-qase-MM-027-email-con-doble-arroba.png` | Caso MM-27 / MM-027 en Qase |
| `60-qase-MM-028-email-duplicado-por-mayusculas-minusculas.png` | Caso MM-28 / MM-028 en Qase |
| `61-qase-MM-029-nombre-vacio.png` | Caso MM-29 / MM-029 en Qase |
| `62-qase-MM-030-nombre-solo-espacios.png` | Caso MM-30 / MM-030 en Qase |
| `63-qase-MM-031-nombre-muy-largo-255-caracteres.png` | Caso MM-31 / MM-031 en Qase |
| `64-qase-MM-032-nombre-con-acentos-n-y-caracteres-especiales.png` | Caso MM-32 / MM-032 en Qase |
| `65-qase-MM-033-nombre-con-inyeccion-html-script.png` | Caso MM-33 / MM-033 en Qase |
| `66-qase-MM-034-pais-sin-seleccionar.png` | Caso MM-34 / MM-034 en Qase |
| `67-qase-MM-035-cada-pais-valido-del-select-9-opciones.png` | Caso MM-35 / MM-035 en Qase |
| `68-qase-MM-036-doble-clic-en-crear-cuenta.png` | Caso MM-36 / MM-036 en Qase |
| `69-qase-MM-037-correccion-de-error-y-reenvio-exitoso.png` | Caso MM-37 / MM-037 en Qase |
| `70-qase-MM-038-bandeja-de-bienvenida-tras-alta-exitosa.png` | Caso MM-38 / MM-038 en Qase |
| `71-qase-MM-039-contrasena-vacia-con-resto-valido.png` | Caso MM-39 / MM-039 en Qase |
| `72-qase-MM-040-email-sin-tld-usuario-dominio.png` | Caso MM-40 / MM-040 en Qase |
| `73-minimoda-producto-stock.png` | Producto MiniModa con stock visible (exploración stock; sección 6b pendiente de redactar) |
| `74-minimoda-cantidad-mayor-al-stock.png` | Cantidad mayor al stock en el producto |
| `75-minimoda-carrito-sobre-stock.png` | Carrito con cantidad por encima del stock |
| `76-minimoda-checkout-sobre-stock.png` | Checkout con compra por encima del stock |
| `77-minimoda-compra-confirmada-sobre-stock.png` | Confirmación de compra por encima del stock |
| `78-minimoda-carrito-cantidad-cero.png` | Carrito con cantidad 0 (exploración stock; sección 6b pendiente) |

Archivos de diseño de casos (también en esta carpeta): `casos-qase.md`, `casos-qase.json`.

## 6b. Prueba exploratoria: compra por encima del stock

**Sitio:** https://minimoda-navy.vercel.app  
**Producto:** «Body Manga Larga Estrellitas» (`/producto/1`, $8.500) — en pantalla muestra **«Stock: 12»**.

### Qué se hizo
1. En la ficha del producto **no hay campo de cantidad**. Se hicieron **13 clics** en «Agregar al carrito»; cada clic mostró «Listo, lo sumamos al carrito.» **sin límite** por stock.
2. Carrito quedó en **13 u / $110.500**, sin aviso de exceso de stock.
3. Con el botón «+» del carrito se llegó a **14 u / $119.000**, también sin aviso.
4. Checkout mostró «× 14, $ 119.000», envío **$ 3.500**, estimado **$ 122.500**, sin aviso de stock.
5. Con tarjeta de prueba `4111111111111111`, «Confirmar compra» devolvió:  
   «✅ Compra confirmada. Orden MM-612254. Envío a Argentina: $ 3.500. Te enviamos un email de confirmación (ver Bandeja).»
6. **Después de la compra:** el producto sigue mostrando «Stock: 12» (no se descuenta); el carrito **no se vacía** (sigue en 14 u); al **recargar la página** el carrito se pierde.
7. Con «−» se pudo bajar a **cantidad 0**: carrito vacío y «Finalizar compra» deshabilitado (**OK**). No se pudo llegar a cantidad negativa.

### Conclusión
**BUG:** se permite comprar **14 unidades** con stock declarado de **12**.

### Bugs encontrados
| Severidad | Bug |
|-----------|-----|
| **Alta** | Se puede comprar por encima del stock (14 con stock 12); sin bloqueo en agregar, carrito ni checkout. |
| **Media** | Tras la compra confirmada el stock **no se descuenta** (sigue «Stock: 12»). |
| **Baja/media** | El carrito **no se vacía** después de una compra confirmada. |
| **Baja** | El carrito **se pierde al recargar** la página (no persiste). |
| (OK) | Cantidad 0 con «−» vacía el carrito y deshabilita «Finalizar compra»; no permite negativos. |

### Evidencias
| Archivo | Qué muestra |
|---------|-------------|
| `evidencias/73-minimoda-producto-stock.png` | Ficha del producto con «Stock: 12» |
| `evidencias/74-minimoda-cantidad-mayor-al-stock.png` | Agregar al carrito por encima del stock |
| `evidencias/75-minimoda-carrito-sobre-stock.png` | Carrito con 13 u / $110.500 |
| `evidencias/76-minimoda-checkout-sobre-stock.png` | Checkout × 14, $119.000 + envío |
| `evidencias/77-minimoda-compra-confirmada-sobre-stock.png` | Compra confirmada Orden MM-612254 |
| `evidencias/78-minimoda-carrito-cantidad-cero.png` | Carrito en cantidad 0 / Finalizar deshabilitado |


## 7. Mapa del harness
| Pieza | En lo que usé |
|-------|---------------|
| Modelo | Gemini Flash; ChatGPT Instant en chat; GPT-6.1 Sol en Work |
| App | gemini.google.com; chatgpt.com (web) |
| Harness | Chat sin herramientas vs Work: agente con navegador en la nube que ejecuta pasos |
| MCP | No se usó MCP propio; Work usó su herramienta de navegador integrada |
| Skill | Ninguna en esta práctica |

## 8. Entrega
- Link de tu repo (pegalo también en el Telegram): https://github.com/jazidovandod-gif/minimoda-test/tree/main/clase-01
- Proyecto Qase: https://app.qase.io/project/MM
