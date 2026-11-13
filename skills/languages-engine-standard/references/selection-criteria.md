# Selection Criteria

Use the tables to shortlist candidates by requirement. Compare only plausible options and add a candidate when the project has a requirement the listed options may not cover. Row order carries no preference.

## Frontend Language

- Start with the target surface and runtime, such as browser, mobile, desktop, or a server-rendered frontend. For languages that compile or transpile to another target, verify the build output, host interoperability, and support for the required platform APIs.
- Compare the available UI and platform libraries against the critical journeys. Check rendering and distribution needs, supported browser or OS targets, accessibility tooling, bundle or startup budgets, offline behavior, and debugging where they drive the choice.
- For an existing frontend, check component reuse, native integration, and the cost of migrating or maintaining a second toolchain. Consider shared frontend and backend types only where the interface and tooling make them useful.

| Language | Framework or UI library options | Evaluate when | Verify |
|---|---|---|---|
| JavaScript | [Vue](https://vuejs.org/guide/introduction.html) or [React](https://react.dev/learn) for component UIs, [Next.js](https://nextjs.org/docs) for React with integrated routing and rendering, or browser APIs for a small UI. | The surface runs in a browser or has an existing JavaScript codebase. | Browser targets, rendering and hosting support, and API payload validation. |
| TypeScript | [Angular](https://angular.dev/overview) for integrated routing and forms, Vue or React for component UIs, or Next.js for React with integrated routing and rendering. | The web UI benefits from static checks for shared contracts, components, or application state. | JavaScript build targets, framework and compiler compatibility, and runtime validation at external boundaries. |
| Swift | [SwiftUI](https://developer.apple.com/xcode/swiftui/) for declarative Apple UI, or [UIKit](https://developer.apple.com/documentation/uikit) when existing iOS components or required APIs make it a better fit. | An Apple-platform UI needs native SDKs or platform behavior. | Supported OS versions, SDK coverage, and the build and distribution pipeline. |
| Kotlin | [Jetpack Compose](https://developer.android.com/compose) for declarative Android UI, or Android Views for existing view-based screens. | An Android UI needs native APIs or interoperability with an existing Android codebase. | Device and OS targets, interoperability with existing views and Java code, and native build tooling. |
| Dart | [Flutter](https://docs.flutter.dev/resources/architectural-overview) for a shared UI across supported targets. | A shared UI can meet the required journeys on each target platform. | Plugin coverage, accessibility, and platform-specific behavior on each target. |
| C# | [Blazor](https://learn.microsoft.com/aspnet/core/blazor) for web UI, [.NET MAUI](https://learn.microsoft.com/en-us/dotnet/architecture/maui/introduction) for supported native targets, or [WPF](https://learn.microsoft.com/en-us/dotnet/desktop/wpf/overview/) for Windows desktop. | The frontend depends on the .NET ecosystem or targets a supported platform. | Rendering or hosting model, target support, native integration, and distribution. |

## Backend Language

- Classify the workload before comparing ecosystems. Check I/O concurrency, CPU and memory budgets, latency, startup limits, platform or SDK requirements, and the deployment runtime. Verify the programming language and its runtime together.
- Compare required libraries and supported drivers, diagnostics and testing, upgrade and support policies, and team capacity to build and operate the service. Use representative evidence for performance claims that determine the choice.
- Check contract compatibility with frontend and other consumers. Pay attention to serialization semantics and generated client support when the interface depends on them.

| Language | Framework or standard library options | Evaluate when | Verify |
|---|---|---|---|
| Java | [Spring Boot](https://spring.io/projects/spring-boot) for services that use Spring integrations and conventions. | Required SDKs, existing services, or team ownership favor the JVM ecosystem. | Java and dependency compatibility, startup, and memory under the intended deployment model. |
| Kotlin | [Ktor](https://ktor.io/docs/ktor-server.html) for a coroutine-based Kotlin service, or [Spring Boot](https://docs.spring.io/spring-boot/reference/features/kotlin.html) when Spring integrations matter. | Kotlin is a fit for the team's JVM stack or async workload. | Kotlin and framework compatibility, coroutine behavior, and blocking dependencies. |
| C# | [ASP.NET Core](https://learn.microsoft.com/en-us/aspnet/core/overview) with Minimal APIs for a small HTTP surface or controllers for structured MVC APIs. | Existing .NET services, team expertise, or required SDKs favor .NET. | Hosting support, dependency compatibility, and deployment constraints. |
| JavaScript | [Express](https://expressjs.com/) for routing and middleware on Node.js. | The service benefits from an existing JavaScript codebase, packages, or tooling. | Node.js and package compatibility, runtime validation, and CPU-heavy request behavior. |
| TypeScript | [NestJS](https://docs.nestjs.com/) for modules and dependency injection, or Express when routing and middleware suffice. | Static checks, shared tooling, or the existing stack favor TypeScript. | Build and runtime compatibility, external payload validation, and framework conventions. |
| Python | [FastAPI](https://fastapi.tiangolo.com/) for typed HTTP APIs, or [Django](https://docs.djangoproject.com/en/stable/intro/overview/) when integrated data models and admin tools are needed. | Required data, scientific, automation, or service libraries are available in its ecosystem. | Worker and concurrency model, blocking dependencies, and deployment packaging. |
| Go | [Gin](https://gin-gonic.com/en/docs/) for routing and middleware helpers, or [`net/http`](https://pkg.go.dev/net/http) when the standard library covers the service. | Network services or operational tools benefit from Go's concurrency model and compiled deployment. | Required SDKs, driver coverage, and latency and resource behavior under load. |
| Rust | [Axum](https://docs.rs/axum/latest/axum/) for an async HTTP service in the Tokio ecosystem. | Native integration or tight memory, CPU, or latency budgets materially affect the workload. | Async runtime and library fit, build targets, diagnostics, and maintainability. |
| C++ | [Drogon](https://drogon.org/) for HTTP endpoints in a native C++ service. | Existing native code, required libraries, or platform constraints favor C++. | Compiler and dependency compatibility, observability, and memory safety practices. |
| Ruby | [Ruby on Rails](https://rubyonrails.org/) for an application that benefits from integrated routing, data models, and migrations. | Existing applications or domain libraries favor Ruby. | Supported runtime and framework versions, worker model, and workload performance. |
| PHP | [Laravel](https://laravel.com/docs) when integrated routing, data access, and job tooling fit the application. | Existing applications, hosting, or team expertise favor PHP. | PHP and extension compatibility, web and worker hosting, and workload performance. |

## Database Engine

- Identify the source of truth, data shape, important reads and writes, constraints, transaction boundaries, isolation, and consistency requirements. Use actual access patterns to compare relevant engine families.
- Check concurrency, growth, latency and throughput, availability, deployment restrictions, backup and restore, and data residency or licensing where applicable. For managed deployments, verify the features of the offered engine version and service tier.
- Compare the cost of operating and recovering each engine. For a change to an existing datastore, account for schema and data conversion, cutover, validation, and rollback. For multiple engines, record the authoritative owner, consistency boundaries, and recovery plan.

| Engine | Evaluate when | Query language or interface to verify |
|---|---|---|
| PostgreSQL | Relational constraints, joins, transactions, or a required PostgreSQL extension matter. | PostgreSQL SQL dialect and any required extension interfaces. |
| MySQL or MariaDB | The workload is relational and existing hosting, tools, or applications favor one of these engines. | The selected engine's SQL dialect. Check feature, driver, and migration differences. |
| SQL Server or Oracle Database | Existing integrations, operational standards, or required engine capabilities favor one of these platforms. | Transact-SQL for SQL Server or Oracle SQL for Oracle Database. Verify procedural extensions separately if needed. |
| SQLite | The application needs an embedded or local database with file-based deployment. | SQLite SQL dialect. Check concurrent writes, file placement, and recovery. |
| MongoDB | Document-shaped data and document-level access patterns match the workload. | MongoDB Query Language and aggregation pipelines. Verify required indexes and transaction scope. |
| Amazon DynamoDB | Key-based access patterns suit a managed key-value or document store. | Native DynamoDB operations or supported PartiQL operations. Check key design, consistency, and transaction limits. |
| Apache Cassandra | A wide-column model fits known partition-oriented reads and writes. | Cassandra Query Language (CQL). Check partition design, query restrictions, and required consistency. |
| Neo4j | Graph relationships and traversals are central to the workload. | Cypher. Verify traversal cost, transaction guarantees, and deployment requirements. |
| ClickHouse | Analytical scans and aggregations dominate the workload. | ClickHouse SQL dialect. Verify ingestion, data freshness, and update semantics. |

## Query Language and Interface

- Use the selected engine's row as the starting point. When it supports more than one interface, compare only those that can express the required operations and preserve their guarantees.
- Record the engine-supported language and dialect or its native query API. Treat the database driver, SDK, ORM, or query builder as an access mechanism with its own compatibility constraints.
- Verify critical operations against the actual engine and interface. Check required joins or traversals, aggregation, filtering, sorting and pagination, atomic writes, and access paths as applicable. Check parameter binding, data type and null semantics, and transaction support through the selected driver.
- Confirm that required schema changes and migrations are supported. If an abstraction cannot express a required operation, evaluate the engine's supported native path and its maintenance cost. Revisit the engine or backend choice when the combined stack cannot meet a hard requirement.
- Record portability claims only for operations and dialect features supported by the intended targets.
