# Nim binding generator for Java
java-nim-bind takes source code and wraps it in a way that allows the library to mostly work as if it was written in Nim (implementation yet to be done/decided)!
It is meant to be used with my project, [CodeGeLib](https://github.com/Mythical-Forest-Collective/CodeGenLib)
to provide a convenient, idiomatic way to generate Java code from Nim!

This project is a fork of [java-ts-bind](https://github.com/MercerK/java-ts-bind), which is a fork of [bensku/java-ts-bind](https://github.com/bensku/java-ts-bind), which has the goal of generating TypeScript types for Java libraries for use with GraalJS!

## Unmodified parts of the README.md

### Usage
This is a command-line application.

* --format: output format
  * Currently only TS_TYPES is supported
* --in: input directory or source jar
* --symbols: symbol sources (compiled jars)
* --repo: Maven repo to fetch the source jar from
* --artifact: Artifact to fetch from given repo
  * tld.domain:artifact:version (Gradle-style)
* --offset: path offset inside the input
  * Mainly used for Java core types; see .github/workflows for an example
* --include: prefixes for included paths
  * By default, everything is included
* --exclude: prefixes for excluded paths
  * Processed after includes; nothing is excluded by default
* --blacklist: blacklisted type fragments
  * Types that have names which contain any of these are omitted
  * Methods and fields that would use them are also omitted!
* --packageJson: read these options from a JSON file
  * The options should be placed under `tsbindOptions` object
  * Names of options lack -- prefixes but are otherwise same
  * Handy when you already have package.json for publishing
* --index: generate index.d.ts that references other generated files

### Limitations
java-ts-bind does not necessarily generate *valid* TypeScript declarations.
The results are good enough to allow strongly-typed scripts, but it is
recommended that `noLibCheck` is used.

Please also note that java-ts-bind provides *only the types*. Implementing
a module loading system for importing them is left as an exercise for the
reader. For pointers, see [CraftJS](https://github.com/Valtakausi/craftjs)
which (at time of writing) implements a CommonJS module loader with
Java and TypeScript.
