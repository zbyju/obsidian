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

# Code features
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

## Automating updating dependencies
`nx migrate` helps with the process of updating:
- package versions in package.json
- configuration files (Jest, ESLint, Nx config)
- source code (fixing breaking changes, migrating to new best practices)

It happens in three steps:
1. Dependencies gets updated (including package.json, node_modules)
2. The source code gets updated to match the new versions according to the set of instructions in `migrations.json`
3. Optionally remove the `migrations.json` or rerun them in different git branches.
### Step 1
`nx migrate latest` (you can also specify exact version by replacing `latest` with `nx@<version>`)

This step package.json and generates `migrations.json`

Now, you can inspect the package.json and inspect the changes that are about to happen.
### Step 2
To confirm the migrations: `nx migrate --run-migrations` - this will upgrade the source code.
### Step 3
You can remove migrations.json and commit the changes.

## Enforce module boundaries
You can impose constraints on how projects depend on each other to prevent chaos.

## Manage releases
`nx release` can be used to manage releases.

1. Versioning - process of determining the next version of your projects and updating any projects that depend on them to use the new version.
2. Changelog - process of deriving a changelog from the commit messages
3. Publishing - process of publishing projects to a registry

# Plugin features

## Task executors
They perform an action on your code - building, linting, testing, serving, etc.

### Executor vs Shell script/npm script
1. Executors encourage consistent methodology for similar tasks (`nx build project1` and `nx build project2` will do very similar things which gives confidence and removes mental overhead)
2. This consistency can then be leveraged when running for multiple projects (one can expect `build`, `test`, ... to exist for each project) - `nx affected` will run tests for all affected projects for example.
3. Nx integrates with the editor and using the metadata of each executor the developer gets more information.

## Code generators
There are 3 types of generators:
1. Plugin Generator - they are available as an Nx Plugin
2. Local Generators - generators created for your own workspace. They allow you to codify the processes that are unique to your organization.
3. Update Generators - invoked by Nx plugins when you update Nx to keep your config files in sync with the latest versions of 3rd party tools.

### Plugin generators
`nx generate [plugin]:[generator-name] [options]`
`nx generate @nx/react:component mycmp --project=myapp`

It's recommended to have a clean git working dir before invoking a generator to easily revert changes.
