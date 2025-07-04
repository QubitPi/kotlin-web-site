[//]: # (title: Keywords and operators)

## Hard keywords

The following tokens are always interpreted as keywords and cannot be used as identifiers:

 * `as`
     - is used for [type casts](typecasts.md#unsafe-cast-operator).
     - specifies an [alias for an import](packages.md#imports)
 * `as?` is used for [safe type casts](typecasts.md#safe-nullable-cast-operator).
 * `break` [terminates the execution of a loop](returns.md).
 * `class` declares a [class](classes.md).
 * `continue` [proceeds to the next step of the nearest enclosing loop](returns.md).
 * `do` begins a [do/while loop](control-flow.md#while-loops) (a loop with a postcondition).
 * `else` defines the branch of an [if expression](control-flow.md#if-expression) that is executed when the condition is false.
 * `false` specifies the 'false' value of the [Boolean type](booleans.md).
 * `for` begins a [for loop](control-flow.md#for-loops).
 * `fun` declares a [function](functions.md).
 * `if` begins an [if expression](control-flow.md#if-expression).
 * `in`
     - specifies the object being iterated in a [for loop](control-flow.md#for-loops).
     - is used as an infix operator to check that a value belongs to [a range](ranges.md),
       a collection, or another entity that [defines a 'contains' method](operator-overloading.md#in-operator).
     - is used in [when expressions](control-flow.md#when-expressions-and-statements) for the same purpose.
     - marks a type parameter as [contravariant](generics.md#declaration-site-variance).
 * `!in`
     - is used as an operator to check that a value does NOT belong to [a range](ranges.md),
       a collection, or another entity that [defines a 'contains' method](operator-overloading.md#in-operator).
     - is used in [when expressions](control-flow.md#when-expressions-and-statements) for the same purpose.
 * `interface` declares an [interface](interfaces.md).
 * `is`
     - checks that [a value has a certain type](typecasts.md#is-and-is-operators).
     - is used in [when expressions](control-flow.md#when-expressions-and-statements) for the same purpose.
 * `!is`
     - checks that [a value does NOT have a certain type](typecasts.md#is-and-is-operators).
     - is used in [when expressions](control-flow.md#when-expressions-and-statements) for the same purpose.
 * `null` is a constant representing an object reference that doesn't point to any object.
 * `object` declares [a class and its instance at the same time](object-declarations.md).
 * `package` specifies the [package for the current file](packages.md).
 * `return` [returns from the nearest enclosing function or anonymous function](returns.md).
 * `super`
     - [refers to the superclass implementation of a method or property](inheritance.md#calling-the-superclass-implementation).
     - [calls the superclass constructor from a secondary constructor](classes.md#inheritance).
 * `this`
     - refers to [the current receiver](this-expressions.md).
     - [calls another constructor of the same class from a secondary constructor](classes.md#constructors).
 * `throw` [throws an exception](exceptions.md).
 * `true` specifies the 'true' value of the [Boolean type](booleans.md).
 * `try` [begins an exception-handling block](exceptions.md).
 * `typealias` declares a [type alias](type-aliases.md).
 * `typeof` is reserved for future use.
 * `val` declares a read-only [property](properties.md) or [local variable](basic-syntax.md#variables).
 * `var` declares a mutable [property](properties.md) or [local variable](basic-syntax.md#variables).
 * `when` begins a [when expression](control-flow.md#when-expressions-and-statements) (executes one of the given branches).
 * `while` begins a [while loop](control-flow.md#while-loops) (a loop with a precondition).

## Soft keywords

The following tokens act as keywords in the context in which they are applicable, and they can be used
as identifiers in other contexts:

 * `by`
     - [delegates the implementation of an interface to another object](delegation.md).
     - [delegates the implementation of the accessors for a property to another object](delegated-properties.md).
 * `catch` begins a block that [handles a specific exception type](exceptions.md).
 * `constructor` declares a [primary or secondary constructor](classes.md#constructors).
 * `delegate` is used as an [annotation use-site target](annotations.md#annotation-use-site-targets).
 * `dynamic` references a [dynamic type](dynamic-type.md) in Kotlin/JS code.
 * `field` is used as an [annotation use-site target](annotations.md#annotation-use-site-targets).
 * `file` is used as an [annotation use-site target](annotations.md#annotation-use-site-targets).
 * `finally` begins a block that [is always executed when a try block exits](exceptions.md).
 * `get`
     - declares the [getter of a property](properties.md#getters-and-setters).
     - is used as an [annotation use-site target](annotations.md#annotation-use-site-targets).
 * `import` [imports a declaration from another package into the current file](packages.md).
 * `init` begins an [initializer block](classes.md#constructors).
 * `param` is used as an [annotation use-site target](annotations.md#annotation-use-site-targets).
 * `property` is used as an [annotation use-site target](annotations.md#annotation-use-site-targets).
 * `receiver` is used as an [annotation use-site target](annotations.md#annotation-use-site-targets).
 * `set`
     - declares the [setter of a property](properties.md#getters-and-setters).
     - is used as an [annotation use-site target](annotations.md#annotation-use-site-targets).
* `setparam` is used as an [annotation use-site target](annotations.md#annotation-use-site-targets).
* `value` with the `class` keyword declares an [inline class](inline-classes.md).
* `where` specifies the [constraints for a generic type parameter](generics.md#upper-bounds).

## Modifier keywords

The following tokens act as keywords in modifier lists of declarations, and they can be used as identifiers
in other contexts:

 * `abstract` marks a class or member as [abstract](classes.md#abstract-classes).
 * `actual` denotes a platform-specific implementation in [multiplatform projects](https://www.jetbrains.com/help/kotlin-multiplatform-dev/multiplatform-expect-actual.html).
 * `annotation` declares an [annotation class](annotations.md).
 * `companion` declares a [companion object](object-declarations.md#companion-objects).
 * `const` marks a property as a [compile-time constant](properties.md#compile-time-constants).
 * `crossinline` forbids [non-local returns in a lambda passed to an inline function](inline-functions.md#returns).
 * `data` instructs the compiler to [generate canonical members for a class](data-classes.md).
 * `enum` declares an [enumeration](enum-classes.md).
 * `expect` marks a declaration as [platform-specific](https://www.jetbrains.com/help/kotlin-multiplatform-dev/multiplatform-expect-actual.html), expecting an implementation in platform modules.
 * `external` marks a declaration as implemented outside of Kotlin (accessible through [JNI](java-interop.md#using-jni-with-kotlin) or in [JavaScript](js-interop.md#external-modifier)).
 * `final` forbids [overriding a member](inheritance.md#overriding-methods).
 * `infix` allows calling a function using [infix notation](functions.md#infix-notation).
 * `inline` tells the compiler to [inline a function and the lambdas passed to it at the call site](inline-functions.md).
 * `inner` allows referring to an outer class instance from a [nested class](nested-classes.md).
 * `internal` marks a declaration as [visible in the current module](visibility-modifiers.md).
 * `lateinit` allows initializing a [non-nullable property outside of a constructor](properties.md#late-initialized-properties-and-variables).
 * `noinline` turns off [inlining of a lambda passed to an inline function](inline-functions.md#noinline).
 * `open` allows [subclassing a class or overriding a member](classes.md#inheritance).
 * `operator` marks a function as [overloading an operator or implementing a convention](operator-overloading.md).
 * `out` marks a type parameter as [covariant](generics.md#declaration-site-variance).
 * `override` marks a member as an [override of a superclass member](inheritance.md#overriding-methods).
 * `private` marks a declaration as [visible in the current class or file](visibility-modifiers.md).
 * `protected` marks a declaration as [visible in the current class and its subclasses](visibility-modifiers.md).
 * `public` marks a declaration as [visible anywhere](visibility-modifiers.md).
 * `reified` marks a type parameter of an inline function as [accessible at runtime](inline-functions.md#reified-type-parameters).
 * `sealed` declares a [sealed class](sealed-classes.md) (a class with restricted subclassing).
 * `suspend` marks a function or lambda as suspending (usable as a [coroutine](coroutines-overview.md)).
 * `tailrec` marks a function as [tail-recursive](functions.md#tail-recursive-functions) (allowing the compiler to replace recursion with iteration).
 * `vararg` allows [passing a variable number of arguments for a parameter](functions.md#variable-number-of-arguments-varargs).

## Special identifiers

The following identifiers are defined by the compiler in specific contexts, and they can be used as regular
identifiers in other contexts:

 * `field` is used inside a property accessor to refer to the [backing field of the property](properties.md#backing-fields).
 * `it` is used inside a lambda to [refer to its parameter implicitly](lambdas.md#it-implicit-name-of-a-single-parameter).

## Operators and special symbols

Kotlin supports the following operators and special symbols:

 * `+`, `-`, `*`, `/`, `%` - mathematical operators
     - `*` is also used to [pass an array to a vararg parameter](functions.md#variable-number-of-arguments-varargs).
 * `=`
     - assignment operator.
     - is used to specify [default values for parameters](functions.md#parameters-with-default-values).
 * `+=`, `-=`, `*=`, `/=`, `%=` - [augmented assignment operators](operator-overloading.md#augmented-assignments).
 * `++`, `--` - [increment and decrement operators](operator-overloading.md#increments-and-decrements).
 * `&&`, `||`, `!` - logical 'and', 'or', 'not' operators (for bitwise operations, use the corresponding [infix functions](numbers.md#operations-on-numbers) instead).
 * `==`, `!=` - [equality operators](operator-overloading.md#equality-and-inequality-operators) (translated to calls of `equals()` for non-primitive types).
 * `===`, `!==` - [referential equality operators](equality.md#referential-equality).
 * `<`, `>`, `<=`, `>=` - [comparison operators](operator-overloading.md#comparison-operators) (translated to calls of `compareTo()` for non-primitive types).
 * `[`, `]` - [indexed access operator](operator-overloading.md#indexed-access-operator) (translated to calls of `get` and `set`).
 * `!!` [asserts that an expression is non-nullable](null-safety.md#not-null-assertion-operator).
 * `?.` performs a [safe call](null-safety.md#safe-call-operator) (calls a method or accesses a property if the receiver is non-nullable).
 * `?:` takes the right-hand value if the left-hand value is null (the [elvis operator](null-safety.md#elvis-operator)).
 * `::` creates a [member reference](reflection.md#function-references) or a [class reference](reflection.md#class-references).
 * `..`, `..<` create [ranges](ranges.md).
 * `:` separates a name from a type in a declaration.
 * `?` marks a type as [nullable](null-safety.md#nullable-types-and-non-nullable-types).
 * `->`
     - separates the parameters and body of a [lambda expression](lambdas.md#lambda-expression-syntax).
     - separates the parameters and return type declaration in a [function type](lambdas.md#function-types).
     - separates the condition and body of a [when expression](control-flow.md#when-expressions-and-statements) branch.
 * `@`
     - introduces an [annotation](annotations.md#usage).
     - introduces or references a [loop label](returns.md#break-and-continue-labels).
     - introduces or references a [lambda label](returns.md#return-to-labels).
     - references a ['this' expression from an outer scope](this-expressions.md#qualified-this).
     - references an [outer superclass](inheritance.md#calling-the-superclass-implementation).
 * `;` separates multiple statements on the same line.
 * `$` references a variable or expression in a [string template](strings.md#string-templates).
 * `_`
     - substitutes an unused parameter in a [lambda expression](lambdas.md#underscore-for-unused-variables).
     - substitutes an unused parameter in a [destructuring declaration](destructuring-declarations.md#underscore-for-unused-variables).

For operator precedence, see [this reference](https://kotlinlang.org/docs/reference/grammar.html#expressions) in Kotlin grammar.
