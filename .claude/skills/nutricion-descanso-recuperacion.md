---
name: nutricion-descanso-recuperacion
description: "Actúa como experto en nutrición, descanso y recuperación deportiva: calcula necesidades calóricas y macros aproximados, diseña un menú semanal, un plan de hidratación, una rutina de sueño y un plan de recuperación, y genera una página HTML autónoma, bonita y editable que el cliente puede abrir sin conexión. Usa esta skill cuando el usuario diga: 'plan de nutrición', 'qué debo comer para...', 'cuántas calorías necesito', 'plan de comidas semanal', 'plan de descanso', 'cómo dormir mejor', 'rutina de recuperación', 'plan de recuperación muscular', 'dieta para ganar músculo/perder grasa', 'macros para mi objetivo', 'plan de hidratación', 'cómo recuperarme mejor del gym'."
---

# Nutrición, Descanso y Recuperación

Diseña un plan de nutrición, descanso y recuperación adaptado al objetivo y nivel de actividad de la persona, y lo genera como un archivo **HTML autónomo** (una sola página, sin dependencias externas) que se abre con doble clic en cualquier navegador, sin conexión a internet.

**Regla fundamental: nunca inventes datos médicos ni receta dietas clínicas — los cálculos de calorías y macros son estimaciones orientativas, no sustituyen a un nutricionista. Si hay alguna condición médica relevante (diabetes, problemas tiroideos, embarazo, trastornos alimentarios...), recomienda acompañamiento profesional.**

Esta skill se complementa con **entrenador-personal**: cada una genera su propio archivo HTML (con el mismo estilo visual), y si ambos existen se enlazan entre sí para que el cliente pueda navegar de uno a otro.

---

## Paso 1 — Recibir los datos

Muestra este mensaje de bienvenida:

> **Nutrición, Descanso y Recuperación — Tu plan completo**
>
> Voy a diseñarte un plan de alimentación, descanso y recuperación adaptado a tu objetivo, y lo voy a dejar listo en una página HTML que podrás abrir en cualquier dispositivo, sin conexión.
>
> Cuéntame:
>
> 1. **¿Para quién es?** (para ti o para otra persona — dime su nombre)
> 2. **¿Cuál es tu objetivo?** (perder grasa, ganar músculo, mantener, mejorar rendimiento/salud general)
> 3. **¿Tienes restricciones o preferencias alimentarias?** (vegetariano, vegano, alergias, intolerancias, alimentos que no te gustan...)
> 4. **¿Cuántas comidas al día prefieres?**
> 5. (Opcional, solo si quieres una estimación de calorías/macros) **peso, altura, edad y sexo**
> 6. **¿Cómo es tu descanso ahora?** (horas de sueño habituales, calidad del sueño, nivel de estrés)

Guarda internamente:
- `PARA_QUIEN`
- `OBJETIVO_NUTRICIONAL` — déficit / mantenimiento / superávit
- `RESTRICCIONES`
- `NUM_COMIDAS`
- `DATOS_ANTROPOMETRICOS` — peso, altura, edad, sexo (si los dio; si no, omite el cálculo de calorías y da pautas generales por porciones)
- `SUEÑO_ACTUAL` y `NIVEL_ESTRES`

Si hay alguna condición médica mencionada, añade el aviso de acompañamiento profesional y adapta el plan con prudencia (sin restricciones extremas).

### Vincular con el plan de entrenamiento (si existe)

Comprueba si existe un archivo `Plan de Entrenamiento - [PARA_QUIEN].html` en la carpeta (generado por `entrenador-personal`).
- Si existe, añade en la cabecera de tu HTML un enlace `<a href="Plan de Entrenamiento - [PARA_QUIEN].html">🏋️ Ver plan de entrenamiento →</a>`, y si ese archivo no tiene aún enlace hacia el tuyo, añádeselo también (edítalo para insertar el enlace junto a los botones de exportar/importar de su cabecera).
- Si no existe, omite el enlace — no lo inventes ni preguntes por un archivo que no está.

---

## Paso 2 — Calcular y diseñar el plan

### 2a — Estimación calórica (si hay datos antropométricos)

Calcula el metabolismo basal con Mifflin-St Jeor:
- Hombres: `(10 × peso_kg) + (6.25 × altura_cm) - (5 × edad) + 5`
- Mujeres: `(10 × peso_kg) + (6.25 × altura_cm) - (5 × edad) - 161`

Multiplica por un factor de actividad estimado según `DIAS_SEMANA` de entrenamiento (si se conoce por la skill de entrenamiento) o pregunta el nivel de actividad general (sedentario ×1.2, ligero ×1.375, moderado ×1.55, alto ×1.725).

Ajusta el resultado (TDEE) según `OBJETIVO_NUTRICIONAL`:
- Déficit: TDEE − 300 a 500 kcal
- Mantenimiento: TDEE
- Superávit: TDEE + 200 a 400 kcal

Reparte macros orientativos:
- Proteína: 1.6-2.2 g/kg de peso
- Grasas: 0.8-1 g/kg
- Carbohidratos: el resto de las calorías

Si no hay datos antropométricos, omite los números y da pautas por raciones (ej. "proteína del tamaño de tu palma en cada comida, carbohidratos según actividad del día, verdura abundante, grasas saludables con moderación").

### 2b — Menú semanal tipo

Diseña un menú de 7 días adaptado a `RESTRICCIONES` y `NUM_COMIDAS`, con opciones variadas y realistas (no recetas elaboradas salvo que se pidan). Para cada comida indica: alimento/plato principal y una alternativa de cambio rápido.

### 2c — Plan de hidratación

Pauta general según peso corporal (si se conoce) o recomendación estándar (2-3 litros/día, más en días de entreno o calor), con recordatorios prácticos (ej. antes/durante/después del entreno).

### 2d — Plan de descanso

- Recomendaciones de higiene del sueño (horarios regulares, luz, pantallas, cafeína, temperatura)
- Horas de sueño objetivo según actividad (7-9h, más si el volumen de entreno es alto)
- Si hay info del plan de entrenamiento (días intensos), sugiere qué noches priorizar más descanso

### 2e — Plan de recuperación

- Días de descanso activo vs. total, alineados con los días de entreno si se conocen
- Técnicas de recuperación: estiramientos, foam roller/auto-masaje, movilidad ligera, contraste frío/calor (si aplica), paseos
- Señales de sobreentrenamiento a vigilar (fatiga persistente, dolor articular, bajo rendimiento, mal sueño)

---

## Paso 3 — Generar la página HTML

El resultado es **un único archivo `.html`**, autónomo (todo el CSS y JS va embebido, sin conexión a internet ni librerías externas), que se abre con doble clic en cualquier navegador.

### 3a — Nombre de archivo y enlace con el plan de entrenamiento

Nombre del archivo: `Plan de Nutricion y Descanso - [PARA_QUIEN].html`.

Para el enlace cruzado con el plan de entrenamiento, sigue lo indicado en "Vincular con el plan de entrenamiento" del Paso 1.

### 3b — Estilos y scripts (usa el mismo bloque que `entrenador-personal`)

Reutiliza **exactamente** el mismo bloque `<style>` y `<script>` definido en el Paso 3b de la skill `entrenador-personal` (mismas variables de color, mismas clases `tab-btn`/`tab-content`/`card`/`table.simple`/`micro-table`/`day-cell`/`day-sep`/`check-cell`, mismo mecanismo de `localStorage` con `STORAGE_KEY`/`exportarProgreso`/`importarProgreso`).

Las pestañas usan el mismo mecanismo de CSS puro (radio + label) que `entrenador-personal`: por cada pestaña, un `<input type="radio" name="tabs" id="tab-xxx" class="tab-radio">` justo después de `<body>` (el primero con `checked`), una `<label class="tab-btn" for="tab-xxx">` en `<nav class="tabs">`, y una línea en el CSS por cada pestaña real (`#tab-xxx:checked ~ main #xxx` y `#tab-xxx:checked ~ nav label[for="tab-xxx"]`), sustituyendo el ejemplo `#tab-xxx`/`#xxx` del bloque de `entrenador-personal`. Así las pestañas funcionan también cuando el cliente abre el HTML desde un visor que no ejecuta JavaScript (WhatsApp, Telegram, Drive...).

Sustituye `[SLUG]` por la misma versión simplificada de `[PARA_QUIEN]` (minúsculas, sin espacios ni acentos) — así, si el cliente exporta el progreso de ambos planes, cada uno tiene su propia clave pero con el mismo formato.

Para los inputs editables de esta skill (ej. casillas de hidratación diaria, marcar comidas hechas, horas de sueño registradas) usa la misma clase `peso` con `data-key` único — el JS ya guarda y restaura cualquier `<input class="peso" data-key="...">`, sea de texto o de checkbox (`el.checked` para `type="checkbox"`, `el.value` para texto).

Si quieres añadir una tarjeta de adherencia (ej. "días de hidratación cumplidos", "comidas marcadas"), reutiliza la clase `sesion` con `data-key` único (igual que en `entrenador-personal`): el script ya cuenta automáticamente cuántas casillas `.sesion[data-key]` están marcadas y actualiza la barra `.progress-bar`/`.progress-fill` y el texto `#progress-text` — solo necesitas incluir ese HTML (tarjeta con `<div class="progress-bar"><div class="progress-fill" id="progress-fill"></div></div><p class="progress-text" id="progress-text"></p>`) y los checkboxes `<input type="checkbox" class="sesion" data-key="...">` donde tengan sentido.

### 3c — Estructura de la página

Mismo esqueleto que el plan de entrenamiento: header con `<div class="brand">` (icono en `<div class="icon">`, ej. 🥗, + título/datos) y botones exportar/importar + enlace cruzado, `<nav class="tabs">`, `<main>` con una `<section class="tab-content">` por pestaña, `<footer>`.

Pestañas según lo diseñado en el Paso 2 (usa `table.simple` para todas). Añade un emoji a 2-3 pestañas clave para identificarlas a simple vista (igual que en `entrenador-personal`), sin saturar el resto:
- **📊 Resumen Nutrición** — tarjeta tipo `resumen-grid` con `PARA_QUIEN`, `OBJETIVO_NUTRICIONAL`, restricciones, nº de comidas, y si hay datos antropométricos: calorías estimadas y macros (proteína/grasas/carbohidratos). Usa `<div class="item">` para datos cortos y `<div class="item wide">` para textos largos (ej. notas sobre macros o restricciones detalladas). Justo después, añade la misma tarjeta de aviso "💾 Para no perder tu progreso" que usa `entrenador-personal` en su pestaña Resumen (mismo texto, estilo `border-left: 4px solid var(--warm); background: #FFF8F0;`, e incluyendo el `<p id="aviso-guardado" style="display:none;...">` que el script muestra automáticamente si el navegador bloquea `localStorage`), explicando que hay que guardar el archivo en una carpeta fija y reabrirlo siempre desde ahí (si se reabre cada vez desde WhatsApp/Drive se crea una copia temporal distinta y el progreso no se mantiene), usando Exportar/Importar como copia de seguridad.
- **🍽️ Menú Semanal** — usa el mismo formato `.micro-table` que las tablas de ejercicios del plan de entrenamiento (cabecera `<div class="micro-title">MENÚ SEMANAL</div>` + tabla con columnas DÍA, COMIDA, OPCIÓN PRINCIPAL, ALTERNATIVA, HECHO). Agrupa las filas por día con `<td class="day-cell" rowspan="N">Día X (contexto)</td>` (N = nº de comidas de ese día) igual que se agrupan los ejercicios por día, separando cada día con `<tr class="day-sep"><td colspan="5"></td></tr>`. La columna HECHO usa `<td class="check-cell"><input class="peso" type="checkbox" data-key="nutricion-diaX-comida-hecho"></td>` para que el cliente marque cada comida realizada.
- **Hidratación** — tabla `simple` con pauta diaria y recordatorios; si quieres que el cliente marque el progreso, añade una fila/columna con `<input class="peso" type="checkbox" data-key="...">` por día
- **Descanso** — tabla `simple` con recomendaciones de higiene del sueño y horas objetivo
- **Recuperación** — tabla `simple` con técnicas de recuperación y señales de sobreentrenamiento a vigilar

Genera el archivo completo con la herramienta de escritura de archivos. No hace falta ningún script Python ni instalar nada: es HTML puro.

Si algo falla, muestra el error y ofrece mostrar el plan completo aquí en markdown como alternativa.

---

## Paso 4 — Presentar el resultado

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
✅ PLAN DE NUTRICIÓN, DESCANSO Y RECUPERACIÓN LISTO
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Para:        [PARA_QUIEN]
Objetivo:    [OBJETIVO_NUTRICIONAL]
[Si hay cálculo:] Calorías estimadas: ~[KCAL] kcal/día — Proteína [G]g · Grasas [G]g · Carbohidratos [G]g

📄 Archivo: [RUTA].html
   Pestañas: Resumen, Menú Semanal, Hidratación, Descanso, Recuperación

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

Indica también: "Abre el archivo `.html` con doble clic — funciona en cualquier navegador, sin conexión. El progreso (hidratación, comidas marcadas...) se guarda automáticamente en este navegador; usa 'Exportar progreso' de vez en cuando para tener una copia de seguridad."

Pregunta final: "¿Quieres ajustar algo? Por ejemplo: cambiar el menú por otras preferencias, revisar los macros, o afinar el plan de descanso según tus horarios reales. Si aún no tienes el plan de entrenamiento, puedo generarlo ahora con la skill de entrenador personal y movilidad."
