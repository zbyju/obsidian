Open-source build system that provides tools and tehcniques for enhancing productivity, optimizes CI performance, maintains code quality and more.

Features:
- Running tasks effectively
	- They are ran in parallel
- Cache locally + remotely
	- Preventing unnecessary reruns of tasks, saving time
- Automatization of dependency updates
	- Code generation features and tools that upgrade the codebase automatically
- Highly customizable + extensible
	- Many different plugins that are official or maintained by community
- Integration of tooling

## How does Nx work?

Nx is technology agnostic. The main capabilities are for any project, using any technology/language:
- worksapce analysis
- task running
- caching
- distribution
- code generation
- automated code migrations

Plugins are technology specific - they build on top of the fundamental capabilities. 

Devkit is a set of utilities

Nx cloud helps scale the project by adding remote caching and distributed task execution; integrates with github, gitlab and bitbucket to provide searchable and structured logs.

Nx console is an extension for IDEs to provide autocompletion, interactive generators, workspace visualizations, refactoring, etc.

## Run tasks

- **Command** - anything developer types into terminal (`nx run header:build`)
- **Target** - the name of the action (`build`)
- **Task** - invocation of a target on a specific project (`header:build`)

Nx uses the following syntax:
![[run-target-syntax.svg]]

You can also do `nx run-many`, this will run multiple tasks for multiple projects. It will run them in parallel, but you can specify a pipeline to describe the order and dependencies of these tasks.

Using `nx affected` you can run tasks for only projects that are affected by your PR.

Nx can understand the dependecies of the project (project graph), but you need to define for which tasks this ordering actually matters.

## Explore the graph

`npx nx graph`

Generates a project graph visualization. This is good for debugging and understanding what nx is thinking when executing tasks.

