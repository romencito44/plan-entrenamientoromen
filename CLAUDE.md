# Kit de Entrenamiento, Nutrición, Descanso y Recuperación

Este kit contiene dos skills complementarias para Claude Code que generan planes personalizados en forma de páginas web independientes (HTML), listas para abrir en cualquier navegador, sin conexión a internet.

## Comportamiento al iniciar

Cuando el usuario abra esta carpeta y escriba cualquier cosa, responde:

> **Bienvenido al kit de Entrenamiento y Nutrición**
>
> Puedo crear dos tipos de plan, cada uno como una página web independiente que se guarda en tu progreso automáticamente:
>
> 🏋️ **Plan de entrenamiento** — periodizado por mesociclos y microciclos, con tablas de ejercicios editables, control de RIR, cardio y seguimiento de progresión.
>
> 🥗 **Plan de nutrición, descanso y recuperación** — menú semanal, hidratación, pautas de sueño y recuperación, con estimación de calorías y macros si lo necesitas.
>
> Si generas los dos para la misma persona, se enlazan automáticamente entre sí.
>
> **¿Por cuál empezamos? ¿Y para quién es el plan?**

## Qué hace cada skill

### 🏋️ entrenador-personal
A partir de los datos del cliente (objetivo, nivel, días disponibles, material, lesiones, etc.), diseña un plan de entrenamiento periodizado (mesociclos y microciclos, con semanas de descarga) y lo entrega como un archivo `Plan de Entrenamiento - [Nombre].html` con:
- Tablas de ejercicios editables (pesos, reps, RIR) que guardan el progreso en el navegador.
- Pestañas de Resumen, Periodización, cada Mesociclo, Cardio y Progresión.
- Checklist de sesiones completadas y barra de adherencia al plan.
- Exportar/Importar progreso en un archivo JSON de respaldo.

### 🥗 nutricion-descanso-recuperacion
A partir del objetivo nutricional, restricciones alimentarias, número de comidas y (opcionalmente) datos antropométricos, diseña un plan de nutrición, hidratación, descanso y recuperación, y lo entrega como `Plan de Nutricion y Descanso - [Nombre].html` con:
- Estimación orientativa de calorías y macros (si se aportan los datos).
- Menú semanal editable, con casillas para marcar comidas hechas.
- Pautas de hidratación, descanso y recuperación.
- Exportar/Importar progreso en un archivo JSON de respaldo.

## Qué necesita del usuario

Cada skill empieza con un mensaje de bienvenida que pregunta los datos necesarios de forma conversacional (no es un formulario): para quién es el plan, objetivo, nivel/experiencia, disponibilidad, restricciones, etc. No es necesario tener todos los datos de antemano — la skill se adapta y, si falta algo, da pautas generales en lugar de inventar datos.

## Instalación

No hace falta instalar nada. Las skills generan HTML y Markdown puro: no requieren librerías externas, conexión a internet ni dependencias adicionales. Solo necesitas tener Claude Code abierto en esta carpeta.
