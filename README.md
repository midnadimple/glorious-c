# C! Glorious C!
This document is my personal C programming style that I try to refer back to often.
It's been used in projects such as:
- [CoffeeFx: A library and GUI for calculating math expressions](https://github.com/midnadimple/coffeefx)
- The Jackhammer Programming Language (Not yet released)

Here's the rules:
- For anything not mentioned here, fallback on [Dependable C](https://dependablec.org).
- Avoid the C standard library. See [here](https://nullprogram.com/blog/2023/02/11/) and [here](https://nullprogram.com/blog/2023/02/15/).
- `variable_a` = snake_case
- `CONST_A` = YELLING_SNAKE_CASE
- `functionA` = lowerPascalCase
- `TypeA` = PascalCase, for typedefs, enum types and module names
- macro names should mimic the data type they expand to.
> e.g. `S8()` is a macro that instantiates an `S8` type)
- symbols are namespaced to modules with the following format:
	- public: `<odule>_<type>_<symbol>`
	- private: `__<module>_<type>_<symbol>`
- modules names are all lowercase with no underscores and should preferably be one word.
> e.g. `mem`, `parse`, `engine`
- enum names should try to have the word `Kind`, then their names should increase precision.
> e.g. `Module_ObjectKind` -> `Module_ObjectPen`, `Module_ObjectRuler`. etc.
- Prefer [Zero Initialization](https://blog.xoria.org/zii/) when initializing structs.
I typically define a `zeroStruct` macro that uses a memset
- Use [Semantic Compression](https://caseymuratori.com/blog_0015) when writing functions.
- Write a test application for your platform wrapper. It should do the least amount possible to test all features of the wrapper.
- If possible, vendor libraries into your project.
- Seperate modules into:
	- Public header: `<module>.h`
	- Internal headers: `<m>_<header>_internal.h`
	- Source files: `<m>_<name>.h`
	- `<m>` in this case should be one or two letters from the module.
- Keep all source files related to a project in one folder. Only seperate for entirely sandboxed code.
> e.g. `core/` stores the main GUI, `plugin_nodes/` creates a plugin for linking nodes
- For libraries that are meant to be shared:
1. Write the code as a seperated module (see above)
2. Use a shell script or small program to fuse the source files and internal headers into one source file.
3. Distribute the library as the public header and the one source file.

This way, we get to seperate concerns during developments and we get a simple
distribution format that can act as both a single-header library (just include
the source file in another one) or as another translation unit.

