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

Nx cloud helps scale the project by adding remote caching and distributed task execution; integrates with github, gitlab and bitbucket to provide searchable and 