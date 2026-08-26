# C# Development Standards

**Versión:** 1.0  
**Estado:** Propuesta base  
**Alcance:** librerías, APIs, servicios, collectors, aplicaciones y pruebas .NET de Outlier.

## 1. Propósito

Este documento define reglas comunes para que el código de Outlier sea fácil de leer, mantener, probar y publicar. Se construyó revisando `outlier-spa/dataset`, una librería .NET 8 publicada como `Outlier.DataSet`, que contiene un núcleo de dominio, extensiones, conversores JSON/Excel, excepciones específicas y pruebas.

El estándar separa reglas **obligatorias** de recomendaciones. Las reglas obligatorias aplican a código nuevo y a archivos modificados de manera relevante; no obligan a refactorizar masivamente código existente.

## 2. Principios

1. **Claridad antes que brevedad.** Un nombre explícito vale más que una abreviación poco evidente.
2. **Una responsabilidad por tipo.** Cada clase, método y proyecto debe tener un propósito distinguible.
3. **Las dependencias van hacia el núcleo.** El dominio no depende de Excel, JSON, base de datos, UI ni infraestructura.
4. **Las APIs públicas son contratos.** Los cambios incompatibles requieren una decisión consciente de versión y migración.
5. **Validar en los límites.** Entradas externas se validan al entrar; el núcleo no propaga estados inválidos.
6. **Pruebas junto al comportamiento.** Todo bug corregido y toda regla de negocio nueva debe quedar cubierta por una prueba.

## 3. Estructura de repositorio y solución

Los repositorios .NET siguen esta forma base:

```text
<repositorio>/
├── README.md
├── .editorconfig
├── Directory.Build.props
├── Directory.Packages.props          # si se centralizan versiones
├── .github/workflows/
├── docs/
├── samples/                          # opcional
├── tests/                            # opcional si no se usa src/*Tests
└── src/
    ├── Outlier.<Producto>/
    └── Outlier.<Producto>.Tests/
```

- Los proyectos productivos viven en `src/`.
- Las pruebas se nombran `Outlier.<Producto>.Tests`; no `UnitTest` en singular.
- Los archivos de prueba y datos de prueba viven bajo el proyecto de pruebas, por ejemplo `TestData/`.
- `docs/` contiene decisiones técnicas y documentación de arquitectura; el `README.md` explica instalación, uso rápido y compatibilidad.
- No se versionan `bin/`, `obj/`, resultados de pruebas, secretos ni archivos locales de IDE.

### 3.1 Proyectos y dependencias

- El nombre de ensamblado y paquete NuGet usa `Outlier.<Producto>` en PascalCase: por ejemplo, `Outlier.DataSet`.
- Un proyecto de dominio o `Core` no referencia proyectos de serialización, archivos, API o infraestructura.
- La serialización va en `Outlier.<Producto>.Serialization` cuando depende de paquetes externos o cuando el contrato JSON/XML forma parte de una responsabilidad separable.
- Los paquetes de integración opcional, como Excel, SQL o Azure, se separan cuando aumentan materialmente las dependencias o el tamaño del paquete principal.
- Todo paquete publicado debe declarar: `PackageId`, `Authors`, `Company`, `RepositoryUrl`, licencia, versión, `TargetFramework` y generación de símbolos/SourceLink cuando corresponda.

## 4. Convenciones de archivos, namespaces y tipos

### 4.1 Regla de un tipo por archivo

- Cada clase, interfaz, record, enum o excepción pública vive en su propio archivo.
- El archivo se llama igual que el tipo: `Column.cs`, `DataConverter.cs`, `ColumnNotFoundException.cs`.
- Una excepción permitida es un tipo privado, pequeño y estrictamente local. No se usa para agrupar clases de producción sin relación.
- Las extensiones de un mismo concepto pueden agruparse como `ColumnExtensions.cs` o dividirse por responsabilidad: `ColumnValidationExtensions.cs`.

### 4.2 Clases parciales

- `partial` se usa solo cuando una clase se divide por responsabilidades estables, por ejemplo `Column.cs` y `Column.Validation.cs`.
- Se prefiere el sufijo descriptivo completo; no `Column.Check.cs`.
- Cada archivo parcial conserva una responsabilidad clara y no duplica `using`, campos o lógica de inicialización innecesariamente.

### 4.3 Namespaces

- El namespace replica la carpeta desde el proyecto: `Outlier.DataSet.Serialization.Json` para `Serialization/Json/DataConverter.cs`.
- Se usa file-scoped namespace:

```csharp
namespace Outlier.DataSet;
```

- No se usa `Common` ni `Utils` como destino genérico. Un tipo se nombra por su responsabilidad: `ValueConverter`, `ColumnValidator`, `TypeConverter` o `CsvFormatter`.

## 5. Nombres

| Elemento | Convención | Ejemplo |
| --- | --- | --- |
| Namespace, tipo, método, propiedad, evento | PascalCase | `Definition`, `GetColumn` |
| Parámetro y variable local | camelCase | `columnName`, `parsedValue` |
| Campo privado readonly | `_camelCase` | `_values`, `_definition` |
| Constante | PascalCase | `DefaultDateFormat` |
| Interfaz | prefijo `I` | `IDataSerializer` |
| Método asíncrono | sufijo `Async` | `ReadAsync` |
| Prueba | `Método_Escenario_Resultado` | `GetColumn_WhenMissing_ThrowsColumnNotFoundException` |
| Booleano | pregunta o estado | `HasDefault`, `isValid`, `canSerialize` |

Reglas adicionales:

- No se usan abreviaciones salvo que sean universalmente conocidas (`Id`, `Json`, `Csv`, `Url`).
- No se usan nombres vagos como `Helper`, `Manager`, `Utils`, `Data2`, `Process` o `Handle` sin un complemento que describa qué hacen.
- Los nombres de colecciones son plurales: `columns`, `definitions`, `values`.
- Los nombres de excepciones describen el problema y terminan en `Exception`.

## 6. Estilo de código

### 6.1 Formato

- Indentación de 4 espacios; sin tabs.
- Llaves siempre en línea propia.
- Una línea en blanco entre miembros lógicamente distintos.
- Máximo recomendado: 160 caracteres por línea.
- Se usan `var` cuando el tipo es evidente por la expresión del lado derecho; de otro modo se declara el tipo explícito.
- Se prefiere una expresión clara antes que LINQ encadenado difícil de depurar.
- `using` se ordenan: `System.*`, paquetes externos, `Outlier.*`; se eliminan los no usados.
- No se dejan comentarios de depuración, código comentado ni marcadores como `//ho`. El historial vive en Git; una tarea pendiente vive en un issue con `TODO(<issue>):` temporal.

### 6.2 Métodos

- Un método debe hacer una sola cosa y tener un nombre que explique el resultado.
- Se prefiere retornar temprano para disminuir anidación.
- Máximo recomendado: 40 líneas por método. Si supera ese tamaño, se extraen pasos con nombres de dominio.
- Evitar parámetros `bool` que cambian radicalmente el comportamiento. Preferir una sobrecarga, enum u objeto de opciones.
- Métodos públicos validan argumentos y lanzan `ArgumentNullException.ThrowIfNull(...)` o una excepción de dominio apropiada.

```csharp
public Column GetColumn(string name)
{
    ArgumentException.ThrowIfNullOrWhiteSpace(name);

    return _columnsByName.TryGetValue(name, out var column)
        ? column
        : throw new ColumnNotFoundException(name);
}
```

## 7. Diseño de dominio y encapsulación

- Los campos mutables son privados. No se exponen colecciones mutables como `Dictionary` o `List` desde una API pública.
- Se expone `IReadOnlyCollection<T>`, `IReadOnlyList<T>` o `IReadOnlyDictionary<TKey, TValue>` cuando el consumidor solo debe leer.
- Las invariantes se preservan dentro del tipo: una entidad o value object no entrega una forma de quedar inválido.
- Se usan `record` o `record struct` para valores inmutables con igualdad por valor; `class` para entidades con identidad o estado mutable controlado.
- Los constructores dejan el objeto en un estado válido. Las propiedades públicas no deben permitir romper invariantes sin validación.
- Evitar `dynamic` y `object` en APIs públicas. Cuando sean inevitables por una librería de datos como `DataSet`, aislarlos dentro del núcleo y ofrecer métodos tipados como `Get<T>` y `Set<T>`.

Para `Outlier.DataSet`, `Data.Values` debería evolucionar hacia una vista de solo lectura y la modificación debe pasar por el indexador o `SetValue`, donde se aplica conversión y validación.

## 8. Nullability y tipos

- Todo proyecto nuevo habilita nullable reference types:

```xml
<Nullable>enable</Nullable>
<ImplicitUsings>enable</ImplicitUsings>
<TreatWarningsAsErrors>true</TreatWarningsAsErrors>
```

- Un miembro que puede no tener valor se declara explícitamente nullable: `string? Description`.
- No se asigna `null` a tipos no-nullables como `string` u `object`.
- No se usa el operador `!` para silenciar advertencias sin una garantía verificable.
- Preferir `DateOnly`, `TimeOnly`, `DateTimeOffset` y `decimal` según el significado del dato. Para instantes absolutos o datos entre zonas horarias, usar `DateTimeOffset`.
- La cultura se declara explícitamente al serializar, comparar o convertir valores persistidos. Para formatos de máquina se usa `CultureInfo.InvariantCulture`.

## 9. Errores, validación y logging

- Las excepciones representan situaciones excepcionales, no flujo normal.
- Cada capa lanza excepciones de su dominio cuando mejora la comprensión: `ColumnNotFoundException`, `InvalidDefinitionException`.
- Las excepciones personalizadas incluyen un mensaje accionable y preservan la excepción interna cuando existe.
- Nunca se captura `Exception` para ocultarlo. Si se agrega contexto, se relanza con `throw;` o se encapsula preservando `innerException`.
- No se lanza `InvalidProgramException` para errores de datos o reglas de negocio; se usa `InvalidOperationException`, `ArgumentException` o una excepción específica.
- Las librerías no escriben directamente a consola. Reciben `ILogger<T>` cuando deben emitir diagnósticos, o devuelven resultados explícitos cuando el error es esperable.

## 10. Colecciones, LINQ y rendimiento

- Elegir la colección por el acceso: `List<T>` para orden e índice, `Dictionary<TKey,TValue>` para búsqueda por clave, `HashSet<T>` para pertenencia.
- Definir el comparador de claves de forma explícita. Para identificadores técnicos, preferir `StringComparer.OrdinalIgnoreCase` antes que comparadores dependientes de cultura.
- No enumerar un `IEnumerable<T>` más de una vez si puede venir de una consulta o stream. Materializar una vez cuando sea necesario.
- No usar `ToList()` solo para poder llamar a `ForEach`; usar `foreach`.
- No usar `Count()` para comprobar si una secuencia tiene elementos; usar `Any()`.
- En operaciones frecuentes, evitar reflexión repetitiva, serialización innecesaria y asignaciones intermedias.

## 11. Extensiones, serialización e integraciones

- Las extensiones se agrupan por capacidad: `Filtering`, `Aggregation`, `Serialization`, `Importing`.
- Una extensión no modifica silenciosamente una colección o instancia recibida, salvo que el nombre lo indique claramente (`AddColumnInPlace`). Preferir devolver una nueva instancia cuando el costo sea razonable.
- Los conversores JSON, lectores Excel/CSV y adaptadores externos viven fuera del núcleo del dominio cuando sea posible.
- Los contratos serializados son explícitos y se cubren con pruebas de ida y vuelta: serializar → deserializar → comparar comportamiento/valor.
- El formato de fecha, nombres de propiedades y compatibilidad de versiones se consideran parte del contrato público del paquete.

## 12. APIs públicas y NuGet

- Todo tipo y miembro `public` se justifica porque forma parte del contrato del paquete.
- Los cambios que rompen compilación o comportamiento esperado requieren incremento de versión mayor o una ruta de deprecación.
- Las APIs obsoletas se marcan con `[Obsolete]`, mensaje de migración y fecha/versión objetivo de retiro.
- Las bibliotecas públicas generan documentación XML (`GenerateDocumentationFile=true`) para los miembros expuestos de mayor uso.
- Cada paquete publicado tiene ejemplos mínimos de instalación y uso en el README.

## 13. Pruebas

- Los proyectos de prueba usan xUnit y se nombran `*.Tests`.
- Cada prueba verifica un comportamiento observable, no detalles internos de implementación.
- Las pruebas se organizan por tipo o capacidad: `ColumnTests`, `DataSerializationTests`, `ExcelImportTests`.
- Los datos de prueba son pequeños, deterministas y viven en `TestData/`.
- Se cubren explícitamente casos normales, nulos, límites, formato/cultura, errores esperados y regresiones.
- El bug corregido primero se reproduce con una prueba que falla y luego se corrige.
- No se usa un `Program.cs` como reemplazo de pruebas automatizadas.

## 14. Configuración mínima obligatoria

Todos los repositorios nuevos incorporan `.editorconfig` y `Directory.Build.props`. Ejemplo inicial:

```xml
<!-- Directory.Build.props -->
<Project>
  <PropertyGroup>
    <TargetFramework>net8.0</TargetFramework>
    <LangVersion>latest</LangVersion>
    <Nullable>enable</Nullable>
    <ImplicitUsings>enable</ImplicitUsings>
    <TreatWarningsAsErrors>true</TreatWarningsAsErrors>
    <AnalysisLevel>latest-recommended</AnalysisLevel>
    <EnforceCodeStyleInBuild>true</EnforceCodeStyleInBuild>
  </PropertyGroup>
</Project>
```

La solución debe pasar, antes de integrar cambios:

```bash
dotnet restore
dotnet format --verify-no-changes
dotnet build --configuration Release
dotnet test --configuration Release --no-build
```

## 15. Lista de revisión para pull requests

- [ ] El cambio tiene una responsabilidad clara y nombres comprensibles.
- [ ] No incorpora tipos públicos innecesarios ni rompe contratos sin versión/migración.
- [ ] La nulabilidad está declarada correctamente.
- [ ] Las colecciones mutables no se exponen sin necesidad.
- [ ] Entradas, valores límite y errores se validan en el borde correcto.
- [ ] El código no contiene `using` sin usar, código comentado ni comentarios de depuración.
- [ ] Se agregaron o ajustaron pruebas para el comportamiento afectado.
- [ ] `dotnet format`, build y tests pasan en Release.
- [ ] Si hay cambios de serialización, se revisó compatibilidad y cultura/formato.
- [ ] README o documentación se actualizó cuando cambia la API pública.

## 16. Aplicación gradual en `Outlier.DataSet`

El repositorio ya aporta una buena base: solución bajo `src`, paquete claramente nombrado, .NET 8, SourceLink, excepciones de dominio, extensiones por capacidad y una cobertura de pruebas considerable. La prioridad no es reescribirlo, sino elevar el estándar en cada cambio futuro.

Orden recomendado:

1. Agregar `.editorconfig`, `Directory.Build.props`, nullable y analizadores; resolver advertencias de forma incremental.
2. Renombrar `Outlier.DataSet.UnitTest` a `Outlier.DataSet.Tests` y ordenar sus datos en `TestData/`.
3. Retirar `using` no usados, comentarios de depuración y bloques de código comentado.
4. Separar tipos compartidos en archivos propios (`ColumnExtensions`, etc.) y renombrar `Common/Utils.cs` por responsabilidades concretas.
5. Reducir la superficie mutable pública (`Data.Values`) y aislar conversiones/serialización del núcleo.
6. Habilitar documentación XML y completar ejemplos de consumo NuGet.

Estas acciones pueden hacerse en pull requests pequeños y compatibles, manteniendo estable el paquete `Outlier.DataSet` para sus consumidores.
