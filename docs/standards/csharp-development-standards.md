# C# Development Standards

**Version:** 1.0  
**Status:** Baseline proposal  
**Scope:** Outlier .NET libraries, APIs, services, collectors, applications, and tests.

## 1. Purpose

This document establishes common practices that make Outlier code easier to read, maintain, test, and publish. It was prepared from a review of `outlier-spa/dataset`, a .NET 8 library published as `Outlier.DataSet`, which includes domain types, extensions, JSON and Excel support, domain exceptions, and automated tests.

Rules marked as **required** apply to new code and substantially changed files. Existing code does not need to be rewritten merely to comply; improvements are made incrementally.

## 2. Principles

1. **Clarity over cleverness.** Explicit names are preferable to obscure abbreviations.
2. **One responsibility per type.** Each class, method, and project has a distinguishable purpose.
3. **Dependencies point toward the core.** Domain code does not depend on Excel, JSON, databases, UI, or infrastructure.
4. **Public APIs are contracts.** Breaking changes require an explicit versioning and migration decision.
5. **Validate at boundaries.** External input is validated as it enters the system.
6. **Tests protect behaviour.** Every fixed defect and business rule is covered by an automated test.

## 3. Repository and Solution Structure

The baseline layout for a .NET repository is:

```text
<repository>/
├── README.md
├── .editorconfig
├── Directory.Build.props
├── Directory.Packages.props          # when package versions are centralized
├── .github/workflows/
├── docs/
├── samples/                          # optional
└── src/
    ├── Outlier.<Product>/
    └── Outlier.<Product>.Tests/
```

- Production projects live under `src/`.
- Test projects are named `Outlier.<Product>.Tests`; do not use the singular `UnitTest`.
- Test fixtures and files are stored under the test project, for example `TestData/`.
- `docs/` contains architectural decisions and technical documentation. `README.md` explains installation, a quick start, and compatibility.
- Do not commit `bin/`, `obj/`, test results, secrets, or local IDE files.

### 3.1 Projects and Dependencies

- Assembly and NuGet package names use `Outlier.<Product>` in PascalCase, for example `Outlier.DataSet`.
- A domain or `Core` project must not reference serialization, files, API, UI, or infrastructure projects.
- Use `Outlier.<Product>.Serialization` when JSON/XML serialization has external dependencies or is a separable responsibility.
- Split optional integrations such as Excel, SQL, and Azure when they materially increase dependencies or package size.
- Published packages declare `PackageId`, `Authors`, `Company`, `RepositoryUrl`, license, version, `TargetFramework`, and SourceLink/symbols where applicable.

## 4. Files, Namespaces, and Types

### 4.1 One Type per File — Required

- Each public class, interface, record, enum, and exception has its own file.
- The file name matches the type name: `Column.cs`, `DataConverter.cs`, `ColumnNotFoundException.cs`.
- A small, strictly local private type is the only exception.
- Extension classes are named for the capability, for example `ColumnExtensions.cs` or `ColumnValidationExtensions.cs`.

### 4.2 Partial Classes

- Use `partial` only when the class is split into stable responsibilities, for example `Column.cs` and `Column.Validation.cs`.
- Use a complete responsibility name; avoid abbreviated suffixes such as `Column.Check.cs`.
- Partial files must not duplicate initialization logic, fields, or unnecessary imports.

### 4.3 Namespaces

- The namespace mirrors the folder structure: `Outlier.DataSet.Serialization.Json` for `Serialization/Json/DataConverter.cs`.
- Use file-scoped namespaces.

```csharp
namespace Outlier.DataSet;
```

- Do not use `Common` or `Utils` as a generic destination. Name types for what they do: `ValueConverter`, `ColumnValidator`, or `CsvFormatter`.

## 5. Naming

| Element | Convention | Example |
| --- | --- | --- |
| Namespace, type, method, property, event | PascalCase | `Definition`, `GetColumn` |
| Parameter and local variable | camelCase | `columnName`, `parsedValue` |
| Private readonly field | `_camelCase` | `_values`, `_definition` |
| Constant | PascalCase | `DefaultDateFormat` |
| Interface | `I` prefix | `IDataSerializer` |
| Asynchronous method | `Async` suffix | `ReadAsync` |
| Test | `Method_Scenario_ExpectedResult` | `GetColumn_WhenMissing_ThrowsColumnNotFoundException` |
| Boolean | question or state | `HasDefault`, `isValid`, `canSerialize` |

- Use abbreviations only when universally understood (`Id`, `Json`, `Csv`, `Url`).
- Avoid vague names such as `Helper`, `Manager`, `Utils`, `Data2`, `Process`, or `Handle` without a meaningful qualifier.
- Collection names are plural: `columns`, `definitions`, `values`.
- Custom exception names end in `Exception` and state the problem.

## 6. Code Style

- Use 4 spaces; do not use tabs.
- Put braces on their own line.
- Leave one blank line between logically distinct members.
- Recommended maximum line length: 160 characters.
- Use `var` only when the assigned expression makes the type clear; otherwise use an explicit type.
- Prefer clear code over LINQ chains that are difficult to debug.
- Order `using` directives as `System.*`, external packages, and `Outlier.*`; remove unused directives.
- Do not leave debug comments, commented-out code, or markers such as `//ho`. Git preserves history. Use a tracked issue for pending work, optionally as `TODO(<issue>):`.

### 6.1 Methods

- A method does one thing and its name describes its result.
- Prefer early returns to reduce nesting.
- Recommended maximum method length: 40 lines. Extract named domain steps when a method grows beyond that.
- Avoid boolean parameters that drastically change behaviour. Prefer an overload, enum, or options type.
- Public methods validate arguments with `ArgumentNullException.ThrowIfNull(...)` or an appropriate domain exception.

```csharp
public Column GetColumn(string name)
{
    ArgumentException.ThrowIfNullOrWhiteSpace(name);

    return _columnsByName.TryGetValue(name, out var column)
        ? column
        : throw new ColumnNotFoundException(name);
}
```

## 7. Domain Design and Encapsulation

- Mutable fields are private. Do not expose mutable `List<T>` or `Dictionary<TKey, TValue>` values through a public API.
- Expose `IReadOnlyCollection<T>`, `IReadOnlyList<T>`, or `IReadOnlyDictionary<TKey, TValue>` when consumers only need to read.
- Types maintain their own invariants and should not expose a way to become invalid.
- Use `record` or `record struct` for immutable value objects with value equality. Use `class` for entities with identity or controlled mutable state.
- Constructors leave instances valid. Public properties do not bypass validation.
- Avoid `dynamic` and `object` in public APIs. If they are unavoidable in a data library, isolate them in the core and provide typed methods such as `Get<T>` and `Set<T>`.

For `Outlier.DataSet`, `Data.Values` should evolve toward a read-only view; mutations should go through an indexer or `SetValue`, where conversion and validation are enforced.

## 8. Nullability and Types — Required

New projects enable nullable reference types:

```xml
<Nullable>enable</Nullable>
<ImplicitUsings>enable</ImplicitUsings>
<TreatWarningsAsErrors>true</TreatWarningsAsErrors>
```

- Members that may have no value are explicitly nullable: `string? Description`.
- Do not assign `null` to non-nullable types such as `string` or `object`.
- Do not use `!` to suppress warnings without a verifiable guarantee.
- Choose types based on meaning: `DateOnly`, `TimeOnly`, `DateTimeOffset`, and `decimal` as appropriate. Use `DateTimeOffset` for absolute instants or cross-time-zone data.
- Explicitly declare culture when serializing, comparing, or converting persisted values. Use `CultureInfo.InvariantCulture` for machine formats.

## 9. Errors, Validation, and Logging

- Exceptions represent exceptional conditions, not normal control flow.
- Throw domain exceptions when they improve understanding, for example `ColumnNotFoundException` or `InvalidDefinitionException`.
- Custom exceptions include an actionable message and preserve an inner exception where relevant.
- Never catch `Exception` merely to hide it. Rethrow with `throw;` or wrap it while preserving the inner exception.
- Do not use `InvalidProgramException` for invalid data or business rules. Use `InvalidOperationException`, `ArgumentException`, or a domain-specific exception.
- Libraries do not write directly to the console. Use `ILogger<T>` when diagnostic logging is necessary, or return an explicit result for expected failures.

## 10. Collections, LINQ, and Performance

- Choose collections by access pattern: `List<T>` for ordered/indexed access, `Dictionary<TKey, TValue>` for key lookup, and `HashSet<T>` for membership.
- Declare string key comparers explicitly. For technical identifiers, prefer `StringComparer.OrdinalIgnoreCase` to culture-dependent comparison.
- Do not enumerate an `IEnumerable<T>` more than once if it may be a query or stream. Materialize it once when needed.
- Do not use `ToList()` only to call `ForEach`; use `foreach`.
- Do not call `Count()` merely to check whether a sequence has items; use `Any()`.
- Avoid repeated reflection, unnecessary serialization, and intermediate allocations in frequently executed code.

## 11. Extensions, Serialization, and Integrations

- Group extension methods by capability: `Filtering`, `Aggregation`, `Serialization`, and `Importing`.
- An extension does not silently mutate a received collection or object unless its name explicitly says so, for example `AddColumnInPlace`.
- Keep JSON converters, Excel/CSV readers, and external adapters outside the domain core whenever possible.
- Serialized contracts require round-trip tests: serialize → deserialize → compare values and behaviour.
- Date formats, property names, and version compatibility are part of a public package contract.

## 12. Public APIs and NuGet

- Every `public` type and member is deliberate because it forms part of the package contract.
- Changes that break compilation or expected behaviour require a major version increment or a deprecation path.
- Mark deprecated APIs with `[Obsolete]`, include migration guidance, and define a target removal version.
- Public libraries generate XML documentation (`GenerateDocumentationFile=true`) for commonly used exposed members.
- Each published package has installation and usage examples in its README.

## 13. Testing

- Test projects use xUnit and follow the `*.Tests` naming convention.
- Each test verifies observable behaviour, not implementation details.
- Group tests by type or capability: `ColumnTests`, `DataSerializationTests`, `ExcelImportTests`.
- Fixtures are small, deterministic, and stored in `TestData/`.
- Cover normal paths, nulls, boundaries, culture/formatting, expected errors, and regressions.
- A corrected defect first receives a failing regression test, then the implementation is fixed.
- Do not use `Program.cs` as a replacement for automated tests.

## 14. Required Baseline Configuration

All new repositories include `.editorconfig` and `Directory.Build.props`. Baseline example:

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

Before integration, the solution passes:

```bash
dotnet restore
dotnet format --verify-no-changes
dotnet build --configuration Release
dotnet test --configuration Release --no-build
```

## 15. Pull Request Checklist

- [ ] The change has one clear responsibility and understandable names.
- [ ] It does not add unnecessary public types or break contracts without a version/migration decision.
- [ ] Nullability is accurately declared.
- [ ] Mutable collections are not exposed unnecessarily.
- [ ] Inputs, boundary values, and errors are validated at the appropriate boundary.
- [ ] The code has no unused imports, commented-out code, or debug comments.
- [ ] Tests cover the affected behaviour.
- [ ] Formatting, Release build, and tests pass.
- [ ] Serialization changes consider compatibility, culture, and formatting.
- [ ] README or documentation is updated when public APIs change.

## 16. Incremental Adoption in `Outlier.DataSet`

`Outlier.DataSet` already provides a solid base: projects under `src`, clear package naming, .NET 8, SourceLink, domain-specific exceptions, extensions grouped by capability, and substantial tests. The goal is not a full rewrite, but incremental improvement whenever code changes.

Recommended order:

1. Add `.editorconfig`, `Directory.Build.props`, nullable reference types, and analyzers; resolve warnings incrementally.
2. Rename `Outlier.DataSet.UnitTest` to `Outlier.DataSet.Tests` and move fixtures into `TestData/`.
3. Remove unused imports, debug comments, and commented-out blocks.
4. Move shared types into separate files and replace `Common/Utils.cs` with clearly scoped responsibilities.
5. Reduce the mutable public surface (`Data.Values`) and isolate conversion/serialization from the domain core.
6. Enable XML documentation and complete NuGet usage examples.

Implement these actions through small, compatible pull requests to keep `Outlier.DataSet` stable for its consumers.
