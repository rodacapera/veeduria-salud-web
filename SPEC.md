# Especificación: Página de registro del Congreso Nacional de Salud Mental

## Estado

Borrador para revisión. Esta especificación debe aprobarse antes de pasar a plan, tareas o implementación.

## Supuestos actuales

1. El alcance corresponde a la ruta `/registro`, no a una funcionalidad nueva de toda la plataforma.
2. La inscripción seguirá usando el formulario embebido de Proshare ya presente en el proyecto.
3. La página debe conservar el lenguaje visual institucional de VEESIPP Colombia y funcionar en navegadores modernos.
4. El contenido visible del congreso —fechas, sede, agenda, aliados y textos legales— se considera fuente editorial existente; no se cambiará sin confirmación.
5. No se requiere persistencia propia, autenticación ni API nueva para esta iteración.

## Objetivo

Construir y mantener una página de registro clara, confiable y responsive para el Congreso Nacional de Salud Mental Integral 2026. La página debe explicar el propósito del evento, mostrar su agenda, llevar al usuario al formulario de inscripción y comunicar la información institucional y legal necesaria.

### Usuario principal

Personas interesadas en asistir al congreso desde dispositivos móviles o de escritorio, incluyendo ciudadanía, profesionales y organizaciones aliadas.

## Alcance funcional

- Encabezado institucional con logotipos y respaldo oficial.
- Hero con nombre del congreso, ubicación, descripción, imagen de apoyo y CTA hacia el registro.
- Sección que explique por qué participar.
- Agenda organizada por días.
- Formulario de inscripción embebido en la sección `#registro`.
- Información del evento, aliados y enlaces legales.
- Animaciones de entrada existentes, sin impedir navegación ni lectura.
- Adaptación responsive para anchos de escritorio, tablet y móvil.

## Fuera de alcance

- Crear un sistema propio de registro o reemplazar Proshare.
- Cambiar la identidad visual global del sitio.
- Rediseñar las páginas distintas de `/registro`.
- Agregar pagos, cuentas de usuario, notificaciones o administración de inscritos.
- Modificar textos institucionales sin validación editorial.

## Stack técnico

- Next.js 16 con App Router.
- React 19 y TypeScript.
- CSS global modularizado por archivos importados desde `src/index.css`.
- Motion para animaciones existentes.
- Tailwind disponible en el proyecto, pero los estilos de esta página usan principalmente CSS propio.

## Comandos

```bash
npm run dev
npm run lint
npm run build
npm run start
```

No existe actualmente un script de pruebas automatizadas en `package.json`; cualquier incorporación de uno requiere decisión explícita.

## Estructura relevante

```text
app/registro/page.tsx                    # Ruta pública del registro
src/views/Registration/Registration.tsx # Composición de la vista
src/components/registration/             # Secciones de la página
src/styles/reference.css                 # Estilos visuales de la página
src/styles/congreso.css                  # Estilos de la variante anterior/relacionada
src/index.css                            # Imports globales de estilos
public/                                  # Logos e imágenes públicas
```

## Requisitos de experiencia

1. El CTA principal debe llevar al usuario a `#registro` sin navegación ambigua.
2. El formulario embebido debe conservar título accesible y dimensiones utilizables en móvil.
3. La jerarquía visual debe distinguir encabezado, hero, beneficios, agenda, registro e información legal.
4. El contenido no debe desbordarse horizontalmente en anchos de 480 px o menores.
5. Los enlaces y botones deben mostrar estados de foco visibles y tener texto comprensible.
6. Las animaciones deben ser decorativas: el contenido debe seguir siendo usable si se reducen o desactivan las animaciones del sistema.
7. Las imágenes deben mantener proporciones, texto alternativo cuando sean informativas y carga compatible con el renderizado de Next.js.

## Estilo de código

Los componentes deben ser pequeños, semánticos y reutilizables cuando exista repetición real. Los nombres de clases de esta página usan el prefijo `ref-` para evitar colisiones.

```tsx
<section id="registro" className="ref-section ref-registration">
  <div className="ref-wrap">
    <h2>Inscríbete al Congreso</h2>
    <a className="ref-green-button" href="#registro">
      Registrarme
    </a>
  </div>
</section>
```

Convenciones:

- Componentes y tipos en PascalCase.
- Variables, funciones y clases CSS en camelCase/kebab-case según el contexto existente.
- HTML semántico (`header`, `main`, `section`, `article`, `footer`).
- No introducir estilos inline salvo una necesidad concreta de datos dinámicos.
- Mantener los colores y espaciados en CSS; evitar duplicar reglas entre `reference.css` y `congreso.css` sin justificarlo.

## Estrategia de verificación

- `npm run lint` debe finalizar sin errores.
- `npm run build` debe completar correctamente.
- Verificación manual en `/registro` en escritorio y móvil.
- Comprobar el flujo de cada CTA hasta `#registro`.
- Comprobar que el iframe de Proshare carga o, si el proveedor falla, que la página conserva una presentación entendible.
- Comprobar teclado: foco visible, orden lógico y acceso a enlaces/botones.
- Comprobar que no aparece scroll horizontal en viewport móvil.

## Límites

- Siempre: conservar contenido institucional aprobado, usar HTML semántico, validar responsive y ejecutar lint/build antes de entregar.
- Preguntar antes: cambiar el proveedor del formulario, añadir dependencias, modificar textos legales, cambiar rutas públicas o introducir una API/base de datos.
- Nunca: incluir secretos, eliminar pruebas o validaciones existentes, editar archivos de `node_modules`, ocultar errores con supresiones de lint o romper enlaces legales.

## Criterios de éxito

- `/registro` carga sin errores de compilación ni errores de TypeScript.
- La página presenta de forma coherente las cinco áreas principales: identidad, propuesta, agenda, inscripción e información legal.
- Todos los CTA internos llevan a la sección de inscripción.
- El formulario embebido es visible y usable en desktop y móvil.
- No hay desbordamiento horizontal en móvil.
- Los elementos interactivos son navegables por teclado y tienen foco visible.
- `npm run lint` y `npm run build` pasan.

## Preguntas abiertas

1. ¿La especificación debe cubrir únicamente `/registro` o también el resto del sitio VEESIPP?
2. ¿El contenido de fechas, lugar, agenda y aliados ya está aprobado editorialmente?
3. ¿Hay una referencia visual concreta que deba igualarse además de los estilos actuales de `reference.css`?
4. ¿Se requiere una prueba automatizada de la página o basta por ahora con lint, build y verificación manual?
