# Prerequisite

- Visual studio, Rider, or VS Code with C# Dev Kit
- DotNET 9
- Podman
- Azurite?

# Presentation

# Workshop flow

- Tooling
- new project
- dashboard
 	- Show cache hit
- Commands
 	- Swagger
 	- Scalar
 	- ReDoc
- messaging

# Notes

```shell
dotnet add package Swashbuckle.AspNetCore.SwaggerUI
dotnet add package Swashbuckle.AspNetCore.ReDoc
dotnet add package Scalar.AspNetCore

```

```csharp
app.UseSwaggerUI(options => options.SwaggerEndpoint("/openapi/v1.json", "OpenAPI v1"));  
app.UseReDoc(options => options.SpecUrl("/openapi/v1.json"));  
app.MapScalarApiReference();
```

/swagger
/api-docs
/scalar

add messaging nugets

# Message

intro

Dotnet 9

```shell
winget install Microsoft.DotNet.SDK.9
```

Aspire templates

```shell
dotnet new install Aspire.ProjectTemplates
```
