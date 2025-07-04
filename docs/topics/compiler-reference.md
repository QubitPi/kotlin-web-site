[//]: # (title: Kotlin compiler options)

Each release of Kotlin includes compilers for the supported targets: 
JVM, JavaScript, and native binaries for [supported platforms](native-overview.md#target-platforms).

These compilers are used by:
* The IDE, when you click the __Compile__ or __Run__ button for your Kotlin project.
* Gradle, when you call `gradle build` in a console or in the IDE.
* Maven, when you call `mvn compile` or `mvn test-compile` in a console or in the IDE.

You can also run Kotlin compilers manually from the command line as described 
in the [Working with command-line compiler](command-line.md) tutorial. 

## Compiler options

Kotlin compilers have a number of options for tailoring the compiling process.
Compiler options for different targets are listed on this page together with a description of each one.

There are several ways to set the compiler options and their values (_compiler arguments_):
* In IntelliJ IDEA, write in the compiler arguments in the **Additional command line parameters** text box in
  **Settings/Preferences** | **Build, Execution, Deployment** | **Compiler** | **Kotlin Compiler**.
* If you're using Gradle, specify the compiler arguments in the `compilerOptions` property of the Kotlin compilation task.
For details, see [Gradle compiler options](gradle-compiler-options.md#how-to-define-options).
* If you're using Maven, specify the compiler arguments in the `<configuration>` element of the Maven plugin node. 
For details, see [Maven](maven.md#specify-compiler-options).
* If you run a command-line compiler, add the compiler arguments directly to the utility call or write them into an [argfile](#argfile).

  For example:

  ```bash
  $ kotlinc hello.kt -include-runtime -d hello.jar
  ```

  > On Windows, when you pass compiler arguments that contain delimiter characters (whitespace, `=`, `;`, `,`),
  > surround these arguments with double quotes (`"`).
  > ```
  > $ kotlinc.bat hello.kt -include-runtime -d "My Folder\hello.jar"
  > ```
  {style="note"}

## Common options

The following options are common for all Kotlin compilers.

### -version

Display the compiler version.

### -verbose

Enable verbose logging output which includes details of the compilation process.

### -script

Evaluate a Kotlin script file. When called with this option, the compiler executes the first Kotlin script (`*.kts`) 
file among the given arguments.

### -help (-h)

Display usage information and exit. Only standard options are shown.
To show advanced options, use `-X`.

### -X

<primary-label ref="experimental-general"/>

Display information about the advanced options and exit. These options are currently unstable: 
their names and behavior may be changed without notice.

### -kotlin-home _path_

Specify a custom path to the Kotlin compiler used for the discovery of runtime libraries.
  
### -P plugin:pluginId:optionName=value

Pass an option to a Kotlin compiler plugin.
Core plugins and their options are listed in the [Core compiler plugins](components-stability.md#core-compiler-plugins) section of the documentation.
  
### -language-version _version_

Provide source compatibility with the specified version of Kotlin.

### -api-version _version_

Allow using declarations only from the specified version of Kotlin bundled libraries.

### -progressive

Enable the [progressive mode](whatsnew13.md#progressive-mode) for the compiler.

In the progressive mode, deprecations and bug fixes for unstable code take effect immediately,
instead of going through a graceful migration cycle.
Code written in the progressive mode is backwards compatible; however, code written in
a non-progressive mode may cause compilation errors in the progressive mode.

### @argfile

Read the compiler options from the given file. Such a file can contain compiler options with values 
and paths to the source files. Options and paths should be separated by whitespaces. For example:

```
-include-runtime -d hello.jar hello.kt
```

To pass values that contain whitespaces, surround them with single (**'**) or double (**"**) quotes. If a value contains 
quotation marks in it, escape them with a backslash (**\\**).
```
-include-runtime -d 'My folder'
```

You can also pass multiple argument files, for example, to separate compiler options from source files.

```bash
$ kotlinc @compiler.options @classes
```

If the files reside in locations different from the current directory, use relative paths.

```bash
$ kotlinc @options/compiler.options hello.kt
```

### -opt-in _annotation_

Enable usages of API that [requires opt-in](opt-in-requirements.md) with a requirement annotation with the given 
fully qualified name.

### -Xrepl

<primary-label ref="experimental-general"/>

Activates the Kotlin REPL.

```bash
kotlinc -Xrepl
```

### -Xannotation-target-all

<primary-label ref="experimental-general"/>

Enables the experimental [`all` use-site target for annotations](annotations.md#all-meta-target):

```bash
kotlinc -Xannotation-target-all
```

### -Xannotation-default-target=param-property

<primary-label ref="experimental-general"/>

Enables the new experimental [defaulting rule for annotation use-site targets](annotations.md#defaults-when-no-use-site-targets-are-specified):

```bash
kotlinc -Xannotation-default-target=param-property
```

### Warning management

#### -nowarn

Suppress all warnings during compilation.

#### -Werror

Treat all warnings as compilation errors.

#### -Wextra

Enable [additional declaration, expression, and type compiler checks](whatsnew21.md#extra-compiler-checks) that
emit warnings if true.

#### -Xwarning-level
<primary-label ref="experimental-general"/>

Configure the severity level of specific compiler warnings:

```bash
kotlinc -Xwarning-level=DIAGNOSTIC_NAME:(error|warning|disabled)
```

* `error`: raises only the specified warning to an error.
* `warning`: emits a warning for the specified diagnostic and is enabled by default.
* `disabled`: suppresses only the specified warning module-wide.

You can adjust warning reporting in your project by combining module-wide rules with specific ones:

| Command                                            | Description                                                 |
|----------------------------------------------------|-------------------------------------------------------------|
| `-nowarn -Xwarning-level=DIAGNOSTIC_NAME:warning`  | Suppress all warnings except for the specified ones.        |
| `-Werror -Xwarning-level=DIAGNOSTIC_NAME:warning`  | Raise all warnings to errors except for the specified ones. |
| `-Wextra -Xwarning-level=DIAGNOSTIC_NAME:disabled` | Enable all additional checks except for the specified ones. |

If you have many warnings to exclude from the general rules, you can list them in a separate file using [`@argfile`](#argfile).

## Kotlin/JVM compiler options

The Kotlin compiler for JVM compiles Kotlin source files into Java class files. 
The command-line tools for Kotlin to JVM compilation are `kotlinc` and `kotlinc-jvm`.
You can also use them for executing Kotlin script files.

In addition to the [common options](#common-options), Kotlin/JVM compiler has the options listed below.

### -classpath _path_ (-cp _path_)

Search for class files in the specified paths. Separate elements of the classpath with system path separators (**;** on Windows, **:** on macOS/Linux).
The classpath can contain file and directory paths, ZIP, or JAR files.

### -d _path_

Place the generated class files into the specified location. The location can be a directory, a ZIP, or a JAR file.

### -include-runtime

Include the Kotlin runtime into the resulting JAR file. Makes the resulting archive runnable on any Java-enabled 
environment.

### -jdk-home _path_

Use a custom JDK home directory to include into the classpath if it differs from the default `JAVA_HOME`.

### -Xjdk-release=version

<primary-label ref="experimental-general"/>

Specify the target version of the generated JVM bytecode. Limit the API of the JDK in the classpath to the specified Java version. 
Automatically sets [`-jvm-target version`](#jvm-target-version).
Possible values are `1.8`, `9`, `10`, ..., `24`.

> This option is [not guaranteed](https://youtrack.jetbrains.com/issue/KT-29974) to be effective for each JDK distribution.
>
{style="note"}

### -jvm-target _version_

Specify the target version of the generated JVM bytecode. Possible values are `1.8`, `9`, `10`, ..., `24`.
The default value is `%defaultJvmTargetVersion%`.

### -java-parameters

Generate metadata for Java 1.8 reflection on method parameters.

### -module-name _name_ (JVM)

Set a custom name for the generated `.kotlin_module` file.
  
### -no-jdk

Don't automatically include the Java runtime into the classpath.

### -no-reflect

Don't automatically include the Kotlin reflection (`kotlin-reflect.jar`) into the classpath.

### -no-stdlib (JVM)

Don't automatically include the Kotlin/JVM stdlib (`kotlin-stdlib.jar`) and Kotlin reflection (`kotlin-reflect.jar`)
into the classpath. 
  
### -script-templates _classnames[,]_

Script definition template classes. Use fully qualified class names and separate them with commas (**,**).

### -Xjvm-expose-boxed

<primary-label ref="experimental-general"/>

Generate boxed versions of all inline value classes in the module, along with boxed variants of functions that use them,
making both accessible from Java. For more information, see [Inline value classes](java-to-kotlin-interop.md#inline-value-classes)
in the guide to calling Kotlin from Java.

### -jvm-default _mode_

Control how functions declared in interfaces are compiled to default methods on the JVM.

| Mode               | Description                                                                                                                       |
|--------------------|-----------------------------------------------------------------------------------------------------------------------------------|
| `enable`           | Generates default implementations in interfaces and includes bridge functions in subclasses and `DefaultImpls` classes. (Default) |
| `no-compatibility` | Generates only default implementations in interfaces, skipping compatibility bridges and `DefaultImpls` classes.                  |
| `disable`          | Generates only compatibility bridges and `DefaultImpls` classes, skipping default methods.                                        |

## Kotlin/JS compiler options

The Kotlin compiler for JS compiles Kotlin source files into JavaScript code. 
The command-line tool for Kotlin to JS compilation is `kotlinc-js`.

In addition to the [common options](#common-options), Kotlin/JS compiler has the options listed below.

### -target {es5|es2015}

Generate JS files for the specified ECMA version.

### -libraries _path_

Paths to Kotlin libraries with `.meta.js` and `.kjsm` files, separated by the system path separator.

### -main _{call|noCall}_

Define whether the `main` function should be called upon execution.

### -meta-info

Generate `.meta.js` and `.kjsm` files with metadata. Use this option when creating a JS library.

### -module-kind {umd|commonjs|amd|plain}

The kind of JS module generated by the compiler:

- `umd` - a [Universal Module Definition](https://github.com/umdjs/umd) module
- `commonjs` - a [CommonJS](http://www.commonjs.org/) module
- `amd` - an [Asynchronous Module Definition](https://en.wikipedia.org/wiki/Asynchronous_module_definition) module
- `plain` - a plain JS module
    
To learn more about the different kinds of JS module and the distinctions between them,
see [this](https://www.davidbcalhoun.com/2014/what-is-amd-commonjs-and-umd/) article.

### -no-stdlib (JS)

Don't automatically include the default Kotlin/JS stdlib into the compilation dependencies.

### -output _filepath_

Set the destination file for the compilation result. The value must be a path to a `.js` file including its name.

### -output-postfix _filepath_

Add the content of the specified file to the end of the output file.

### -output-prefix _filepath_

Add the content of the specified file to the beginning of the output file.

### -source-map

Generate the source map.

### -source-map-base-dirs _path_

Use the specified paths as base directories. Base directories are used for calculating relative paths in the source map.

### -source-map-embed-sources _{always|never|inlining}_

Embed source files into the source map.

### -source-map-names-policy _{simple-names|fully-qualified-names|no}_

Add variable and function names that you declared in Kotlin code into the source map.

| Setting | Description | Example output |
|---|---|---|
| `simple-names` | Variable names and simple function names are added. (Default) | `main` |
| `fully-qualified-names` | Variable names and fully qualified function names are added. | `com.example.kjs.playground.main` |
| `no` | No variable or function names are added. | N/A |


### -source-map-prefix

Add the specified prefix to paths in the source map.

## Kotlin/Native compiler options

Kotlin/Native compiler compiles Kotlin source files into native binaries for the [supported platforms](native-overview.md#target-platforms). 
The command-line tool for Kotlin/Native compilation is `kotlinc-native`.

In addition to the [common options](#common-options), Kotlin/Native compiler has the options listed below.

### -enable-assertions (-ea)

Enable runtime assertions in the generated code.

### -g

Enable emitting debug information. This option lowers the optimization level and should not be combined with
the [`-opt`](#opt) option.
    
### -generate-test-runner (-tr)

Produce an application for running unit tests from the project.

### -generate-no-exit-test-runner (-trn)

Produce an application for running unit tests without an explicit process exit.

### -include-binary _path_ (-ib _path_)

Pack external binary within the generated klib file.

### -library _path_ (-l _path_)

Link with the library. To learn about using libraries in Kotlin/native projects, see 
[Kotlin/Native libraries](native-libraries.md).

### -library-version _version_ (-lv _version_)

Set the library version.
    
### -list-targets

List the available hardware targets.

### -manifest _path_

Provide a manifest addend file.

### -module-name _name_ (Native)

Specify a name for the compilation module.
This option can also be used to specify a name prefix for the declarations exported to Objective-C:
[How do I specify a custom Objective-C prefix/name for my Kotlin framework?](native-faq.md#how-do-i-specify-a-custom-objective-c-prefix-name-for-my-kotlin-framework)

### -native-library _path_ (-nl _path_)

Include the native bitcode library.

### -no-default-libs

Disable linking user code with the prebuilt [platform libraries](native-platform-libs.md) distributed with the compiler.

### -nomain

Assume the `main` entry point to be provided by external libraries.

### -nopack

Don't pack the library into a klib file.

### -linker-option

Pass an argument to the linker during binary building. This can be used for linking against some native library.

### -linker-options _args_

Pass multiple arguments to the linker during binary building. Separate arguments with whitespaces.

### -nostdlib

Don't link with stdlib.

### -opt

Enable compilation optimizations and produce a binary with better runtime performance. It's not recommended to combine it
with the [`-g`](#g) option, which lowers the optimization level.

### -output _name_ (-o _name_)

Set the name for the output file.

### -entry _name_ (-e _name_)

Specify the qualified entry point name.

### -produce _output_ (-p _output_)

Specify output file kind:

- `program`
- `static`
- `dynamic`
- `framework`
- `library`
- `bitcode`

### -repo _path_ (-r _path_)

Library search path. For more information, see [Library search sequence](native-libraries.md#library-search-sequence).

### -target _target_

Set hardware target. To see the list of available targets, use the [`-list-targets`](#list-targets) option.
