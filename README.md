# Power-Automate

Automatización del procesamiento de la entrega de Anteproyecto y Trabajos de grado con Power Automate.

Todo se empaqueta en una solución de Power Automate. Esto mantenimiento del ciclo de vida de la aplicación (ALM).

La solución llamada FIC_procesamiento_AP_TG tiene los siguientes flujos:

- **Procesamiento del formulario entrega AP y TG**: es el flujo principal. Se encarga de procesar la entrega del formulario ([Entrega Anteproyecto y proyecto de grado - posgrados](https://forms.office.com/r/XJnDhLCEiE)), lo cual implica:
  - Guardar en una lista de sharepoint ([FIC_seguimiento_AP_y_TG](https://javerianacaliedu.sharepoint.com/sites/FIC/Lists/FIC_seguimiento_AP_y_TG/Estudiantes_Publica.aspx?env=WebViewList)) el item con los datos recolectados en el formulario, su [código único del proyecto](#código-único-de-proyecto) y su ubicación de carpeta en sharepoint.
  - Crear una carpeta en SharePoint con el [código único del proyecto](#código-único-de-proyecto) (si es la primera vez que se envía el anteproyecto)
  - Guardar los archivos adjuntos del formulario en la carpeta de SharePoint
  - Enviar un correo de confirmación al estudiante

### _Código único de proyecto_

Es un código generado automáticamente por el flujo, el cuál se compone de:

- Siglas del programa:
  - Maestría en Ciencia de Datos (MCD): MCD
  - Maestría en Ingeniería Civil (MIC): MIC
  - Maestría en Ingeniería de Software (MIS): MIS
  - Maestría en Ingeniería y Ciencias (MINGC): MINGC
  - Maestría en Restauración Ecológica (MRE): MRE
- Año de entrega del anteproyecto: por ej, 2025, 2026
- Semestre de entrega del anteproyecto: por ej, 1, 2
- Número consecutivo por programa: número secuencial que aumenta por cada anteproyecto entregado. Por ej, 1, 2, 3, etc.

Ejemplos de código único de proyecto:

- MCD202519
  - MCD: Maestría en Ciencia de Datos
  - 2025: año de entrega del anteproyecto
  - 1: semestre de entrega del anteproyecto
  - 9: número consecutivo por programa (en este caso, el noveno anteproyecto entregado por estudiantes de la Maestría en Ciencia de Datos)
- MIC2025120
  - MIC: Maestría en Ingeniería Civil
  - 2025: año de entrega del anteproyecto
  - 1: semestre de entrega del anteproyecto
  - 20: número consecutivo por programa (en este caso, el vigésimo anteproyecto entregado por estudiantes de la Maestría en Ingeniería Civil)

### _Solutions_

**¿Qué son _Solutions_?**

Son 'contenedores' usados para agrupar y manejar componentes relacionados (flows, tables, apps y conections) como una sola unidad.
Útiles especialmente cuando se trabaja en ambientes que implican Application Lifecycle Management (AML) o colaboración con diferentes miembros de equipo.

**¿Para qué se usan?**

Se usan principalmente para:

- Para empaquetar todos los componentes relacionados juntos.
- Mover el trabajo entre ambientes (por ej, Dev --> Test --> Prod).
- Compartir apps, flows, y conectores más eficientemente
- Integrar con Dataverse y model-driven apps

**¿Qué se puede agregar en una _Solution_?**

- Power Automate cloud flows
- Apps canvas y apps model-driven
- Tablas y columnas de Dataverse
- Conectores personalizados
- Roles de seguridad
- Variables de entorno
- entre otros.

**Tipos de _Solution_**

- Managed: es una versión de solo lectura usado para producción. No se puede cambiar directamente.
- Unmanaged: es una versión editable usada para ambientes de desarrollo.

### _Child Flow_

"Child Flow" es un Flow que se llama dentro de otro Flow. Lo que en programación se conoce como Función o Método. El Flow que llama al Child Flow se conoce como "Parent Flow" o "Main Flow".

El Child Flow debe ser un **Instant Cloud Flow**.
Hay 2 formas principales para usar un Flow dentro de otro Flow. Una requiere usar una Solution y otra no.

Desde el Flow padre usar el Connector

1. "When an HTTP request is received" (No usa Solutions, pero requiere funcionalidades Premium. Además es más difícil de debuggear)
2. "Run a Child Flow" (Requiere que el Child Flow esté en una misma Solution que el Flow padre)

Usaremos la solución de Run a Child Flow por su mantenibilidad, facilidad de Debugging y ya que es más fácil manejar dependencias dentro de las Solution (más fácil de ver qué se conecta con qué).
Por otro lado, con el Connector "Run a Child Flow", el Flow padre espera a que el Child Flow termine su proceso antes del Flow padre continuar (cosa que no pasa con la opción del _HTTP-based call_).

Se debe justificar más sobre la otra opción? se deben dar más detalles???
