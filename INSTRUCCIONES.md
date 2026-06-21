# Instrucciones de uso

## Requisitos

- Tener [Claude Code](https://claude.com/claude-code) instalado.
- No se necesita ninguna otra instalación, librería, ni conexión a internet para usar los planes generados (son archivos HTML autónomos).

## Pasos

1. **Abre esta carpeta (`kit-entrenamiento-y-nutricion`) con Claude Code.**

2. **Escribe cualquier mensaje** (por ejemplo, "hola" o "quiero un plan de entrenamiento"). Claude te dará la bienvenida y te preguntará qué plan quieres generar primero.

3. **Responde a las preguntas de forma natural**, como si hablaras con un entrenador o un nutricionista: para quién es el plan, objetivo, nivel, días disponibles, restricciones, etc. No necesitas tener todos los datos — si falta algo, Claude usará valores generales en su lugar.

4. **Espera a que Claude genere el archivo HTML.** Verás un resumen final con el nombre del archivo y las pestañas que incluye.

5. **Abre el archivo `.html` generado con doble clic** (se abrirá en tu navegador habitual). Funciona sin conexión.

6. **(Opcional) Genera el segundo plan** (entrenamiento o nutrición, el que falte) repitiendo los pasos 2-5 para la misma persona. Si ambos archivos existen en la carpeta, se enlazarán automáticamente entre sí con un botón en la cabecera.

7. **Usa el plan**: marca pesos, repeticiones, sesiones completadas, comidas hechas, etc. directamente en la página — se guarda automáticamente en el navegador.

8. **Haz copias de seguridad de tu progreso** con el botón "Exportar progreso" (descarga un `.json`). Si cambias de navegador o quieres restaurar el progreso, usa "Importar progreso" y selecciona ese archivo.

## Estructura del kit

```
kit-entrenamiento-y-nutricion/
├── CLAUDE.md                                  ← Mensaje de bienvenida y descripción del kit
├── INSTRUCCIONES.md                           ← Este archivo
└── .claude/
    └── skills/
        ├── entrenador-personal.md             ← Skill que genera el plan de entrenamiento
        └── nutricion-descanso-recuperacion.md ← Skill que genera el plan de nutrición/descanso/recuperación
```

Los archivos `.html` generados (por ejemplo, `Plan de Entrenamiento - [Nombre].html` y `Plan de Nutricion y Descanso - [Nombre].html`) se crearán en esta misma carpeta, junto a estos archivos.
