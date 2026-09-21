# NationStates Dispatch Tools

This is a monorepo of libraries and apps to help managing dispatches in [NationStates](https://www.nationstates.net/).

## 📦 Project Overview

This repository demonstrates a production-ready TypeScript monorepo with:

- **3 Publishable Packages** - Ready for pnpm publishing

  - `@the-south-pacific/strings` - String manipulation utilities
  - `@the-south-pacific/async` - Async utility functions with retry logic
  - `@the-south-pacific/colors` - Color conversion and manipulation utilities

- **1 Internal Library**
  - `@the-south-pacific/utils` - Shared utilities (private, not published)

## 🚀 Quick Start

```bash
# Clone the repository
git clone <your-fork-url>
cd typescript-template

# Install dependencies
pnpm install

# Build all packages
pnpm nx run-many -t build

# Run tests
pnpm nx run-many -t test

# Lint all projects
pnpm nx run-many -t lint

# Run everything in parallel
pnpm nx run-many -t lint test build --parallel=3

# Visualize the project graph
pnpm nx graph
```

## ⭐ Features

### 1. 🛠️ See available targets

```bash

# See all available targets for a project
pnpm nx show project @the-south-pacific/strings
```

### 2. 📦 Package Publishing

Manage releases and publishing with Nx Release:

```bash
# Dry run to see what would be published
pnpm nx release --dry-run

# Version and release packages
pnpm nx release

# Publish only specific packages
pnpm nx release publish --projects=@the-south-pacific/strings,@the-south-pacific/colors
```

[Learn more about Nx Release →](https://nx.dev/docs/features/manage-releases)

## 📁 Project Structure

```
├── packages/
│   ├── strings/     [scope:strings] - String utilities (publishable)
│   ├── async/       [scope:async]   - Async utilities (publishable)
│   ├── colors/      [scope:colors]  - Color utilities (publishable)
│   └── utils/       [scope:shared]  - Shared utilities (private)
├── nx.json          - Nx configuration
├── tsconfig.json    - TypeScript configuration
└── eslint.config.mjs - ESLint with module boundary rules
```

## 🏷️ Understanding Tags

This repository uses tags to enforce module boundaries:

| Package                      | Tag             | Can Import From        |
| ---------------------------- | --------------- | ---------------------- |
| `@the-south-pacific/utils`   | `scope:shared`  | Nothing (base library) |
| `@the-south-pacific/strings` | `scope:strings` | `scope:shared`         |
| `@the-south-pacific/async`   | `scope:async`   | `scope:shared`         |
| `@the-south-pacific/colors`  | `scope:colors`  | `scope:shared`         |

The ESLint configuration enforces these boundaries, preventing circular dependencies and maintaining clean architecture.

## 🧪 Testing Module Boundaries

To see module boundary enforcement in action:

1. Try importing `@the-south-pacific/colors` into `@the-south-pacific/strings`
2. Run `pnpm nx run @the-south-pacific/strings:lint`
3. You'll see an error about violating module boundaries

## 📚 Useful Commands

```bash
# Project exploration
pnpm nx graph                                    # Interactive dependency graph
pnpm nx list                                     # List installed plugins
pnpm nx show project @the-south-pacific/strings --web              # View project details

# Development
pnpm nx run @the-south-pacific/strings:build                           # Build a specific package
pnpm nx run @the-south-pacific/async:test                              # Test a specific package
pnpm nx run @the-south-pacific/colors:lint                             # Lint a specific package

# Running multiple tasks
pnpm nx run-many -t build                       # Build all projects
pnpm nx run-many -t test --parallel=3          # Test in parallel
pnpm nx run-many -t lint test build            # Run multiple targets

# Affected commands (great for CI)
pnpm nx affected -t build                       # Build only affected projects
pnpm nx affected -t test                        # Test only affected projects

# Release management
pnpm nx release --dry-run                       # Preview release changes
pnpm nx release                                 # Create a new release
```

## Install Nx Console

Nx Console is an editor extension that enriches your developer experience. It lets you run tasks, generate code, and improves code autocompletion in your IDE. It is available for VSCode and IntelliJ.

[Install Nx Console &raquo;](https://nx.dev/docs/getting-started/editor-setup?utm_source=nx_project&utm_medium=readme&utm_campaign=nx_projects)
