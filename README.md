# Power-Automate

Automatización con Power Automate

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

### **Usar un Flow dentro de otro Flow**

_Nota: "Child Flow" va a ser el Flow que se llamará dentro de otro Flow_

El "Child Flow" debe ser un **Instant Cloud Flow**.
Hay 2 formas principales para usar un Flow dentro de otro Flow. Una requiere usar una Solution y otra no.

Desde el Flow padre usar el Connector

1. "When an HTTP request is received" (No usa Solutions, pero requiere funcionalidades Premium. Además es más difícil de debuggear)
2. "Run a Child Flow" (Requiere que el Child Flow esté en una misma Solution que el Flow padre)

Usaremos la solución de Run a Child Flow por su mantenibilidad, facilidad de Debugging y ya que es más fácil manejar dependencias dentro de las Solution (más fácil de ver qué se conecta con qué).
Por otro lado, con el Connector "Run a Child Flow", el Flow padre espera a que el Child Flow termine su proceso antes del Flow padre continuar (cosa que no pasa con la opción del _HTTP-based call_).

Se debe justificar más sobre la otra opción? se deben dar más detalles???
