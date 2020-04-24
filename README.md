# spec2ts

[![Build Status](https://travis-ci.org/touchifyapp/spec2ts.svg?branch=master)](https://travis-ci.org/touchifyapp/spec2ts)

`spec2ts` is an utility to create TypeScript types from JSON schemas and OpenAPI v3 specifications. Unlike other code generators `spec2ts` does not use templates to generate code but uses TypeScript's built-in API to generate and pretty-print an abstract syntax tree (AST).

## Features

* **AST-based:** Unlike other code generators `spec2ts` does not use templates to generate code but uses TypeScript's built-in API to generate and pretty-print an abstract syntax tree.
* **Tree-shakeable:** Individually exported types allows you to bundle only the ones you actually use.
* **YAML or JSON:** Use YAML or JSON for your or OpenAPI Specifications and JSON Schemas.
* **External references:** Resolves automatically external references and bundle or import them in generated files.
* **Implementation agnostic:** Use generated types in any projet or framework.

## Components

- `@spec2ts/core`: Helpers methods to generate TypeScript code.
- `@spec2ts/jsonschema`: Utility to generate types from JSON schemas. [More details](https://github.com/touchifyapp/spec2ts/blob/master/packages/jsonschema/README.md).
- `@spec2ts/openapi`: Utility to generate types from Open API v3 specifications. [More details](https://github.com/touchifyapp/spec2ts/blob/master/packages/openapi/README.md).
- `@spec2ts/cli`: CLI wrapper to generate types from Open API v3 specifications and JSON schemas. [More details](https://github.com/touchifyapp/spec2ts/blob/master/packages/cli/README.md).

## Installation

Install in your project:
```bash
npm install @spec2ts/cli
```

## CLI Usage

```bash
# Generate TypeScript types from JSON Schemas
spec2ts jsonschema -o path/to/output path/to/my/*.schema.json

# Generate TypeScript types from Open API specification
spec2ts openapi -o path/to/output path/to/my/specification.yml
```

You can find more details in the `@spec2ts` [documentation](https://github.com/touchifyapp/spec2ts/blob/master/packages/jsonschema/README.md).

## Programmatic Usage

#### Generate TypeScript types from JSON Schemas

```typescript
import { printer } from "@spec2ts/core";
import { parseSchema, JSONSchema } from "@spec2ts/jsonschema";

async function generateSchema(schema: JSONSchema): Promise<string> {
    const result = await parseSchema(schema);
    return printer.printNodes(result);
}
```

#### Generate TypeScript types from OpenAPI Specifications

```typescript
import { printer } from "@spec2ts/core";
import { parseOpenApiFile } from "@spec2ts/openapi";

async function generateSpec(path: string): Promise<string> {
    const result = await parseOpenApiFile(path);
    return printer.printNodes(result);
}
```

## License

This project is under MIT License. See the [LICENSE](LICENSE) file for the full license text.
