# PHP Style Guide

This is North McCormicks's PHP Style Guide.

It was inspired by Digitpaint's/Framework Interop Group's guide:
[PSR-1-basic-coding-standard](https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-1-basic-coding-standard.md),  [PSR-2-coding-style-guide](https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-2-coding-style-guide.md), 
and [DigitPaint/php-style-guide](https://github.com/DigitPaint/php-style-guide).

## Table of Contents
  1.  [Tools](#tools)
  1.  [Keywords](#keywords)
  1.  [PHP Tags](#php-tags)
  1.  [Character Encoding](#character-encoding)
  1.  [Side Effects](#side-effects)
  1.  [Namespace and Class Names](#namespace-and-class-names)
  1.  [Class Constants, Properties, and Methods](#class-constants-properties-and-methodes)
      1. [Constants](#constants)
      1. [Properties](#properties)
      1. [Methods](#methods)
  1.  [Files](#files)
  1.  [Lines](#lines)
  1.  [Indenting](#indenting)
  1.  [Keywords and True/False/Null](#keywords-and-true-false-null)
  1.  [Namespace and Use Declarations](#namespace-and-use-declarations)
  1.  [Classes, Properties, and Methods](#classes-properties-and-methods)
      1. [Extends and Implements](#extends-and-implements)
      1. [Properties](#properties)
      1. [Methods](#methods)
      1. [Method Arguments](#method-arguments)
      1. [`abstract`, `final`, and `static`](#abstract-final-static)
      1. [Method and Function Calls](#method-and-function-calls)
  1.  [Control Structures](#control-structures)
      1. [`if`, `elseif`, `else`](#if-elseif-else)
      1. [`switch`, `case`](#switch-case)
      1. [`while`, `do while`](#while-do-while)
      1. [`for`](#for)
      1. [`foreach`](#foreach)
      1. [`try`, `catch`](#try-catch)
  1.  [Closures](#closures)

## Keywords

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD",
"SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be
interpreted as described in [RFC 2119].

[RFC 2119]: http://www.ietf.org/rfc/rfc2119.txt

## PHP Tags

PHP code MUST use the long `<?php ?>` tags; it
MUST NOT use the other tag variations.

## Character Encoding

PHP code MUST use only UTF-8 without BOM.

## Side Effects

A file SHOULD declare new symbols (classes, functions, constants,
etc.) and cause no other side effects, or it SHOULD execute logic with side
effects, but SHOULD NOT do both.

The phrase "side effects" means execution of logic not directly related to
declaring classes, functions, constants, etc., *merely from including the
file*.

"Side effects" include but are not limited to: generating output, explicit
use of `require` or `include`, connecting to external services, modifying ini
settings, emitting errors or exceptions, modifying global or static variables,
reading from or writing to a file, and so on.

The following is an example of a file with both declarations and side effects;
i.e, an example of what to avoid:

```php
<?php
  // side effect: change ini settings
  ini_set('error_reporting', E_ALL);

  // side effect: loads a file
  include "file.php";

  // side effect: generates output
  echo "<html>\n";

  // declaration
  function foo() {
    // function body
  }
```

The following example is of a file that contains declarations without side
effects; i.e., an example of what to emulate:

```php
<?php
  // declaration
  function foo() {
    // function body
  }

  // conditional declaration is *not* a side effect
  if (!function_exists('bar')) {
    function bar() {
      // function body
    }
  }
```

## Namespace and Class Names

Namespaces and classes MUST follow an "autoloading" PSR:
[PSR-0](https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-0.md) and
[PSR-4](https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-4-autoloader-meta.md).

This means each class is in a file by itself, and is in a namespace of at
least one level: a top-level vendor name.

Class names MUST be declared in `StudlyCaps`.

Code written for PHP 5.3 and after MUST use formal namespaces.

For example:

```php
<?php
  // PHP 5.3 and later:
  namespace Vendor\Model;

  class Foo {
  }
```

Code written for 5.2.x and before SHOULD use the pseudo-namespacing convention
of `Vendor_` prefixes on class names.

```php
<?php
  // PHP 5.2.x and earlier:
  class Vendor_Model_Foo {
  }
```

## Class Constants, Properties, and Methods

The term "class" refers to all classes, interfaces, and traits.

### Constants

Class constants MUST be declared in all upper case with underscore separators.
For example:

```php
<?php
  namespace Vendor\Model;

  class Foo {
    const VERSION = '1.0';
    const DATE_APPROVED = '2012-06-01';
  }
```

### Properties

This guide intentionally avoids any recommendation regarding the use of
`$StudlyCaps`, `$camelCase`, or `$under_score` property names.

Whatever naming convention is used SHOULD be applied consistently within a
reasonable scope. That scope may be vendor-level, package-level, class-level,
or method-level.

### Methods

Method names MUST be declared in `camelCase()`.

## Files

All PHP files MUST use the Unix LF (linefeed) line ending.

All PHP files MUST end with a single blank line.

**The closing `?>` tag MUST be omitted from files containing only PHP.**

## Lines

There MUST NOT be a hard limit on line length.

The soft limit on line length MUST be 120 characters; automated style checkers
MUST warn but MUST NOT error at the soft limit.

Lines SHOULD NOT be longer than 80 characters; lines longer than that SHOULD
be split into multiple subsequent lines of no more than 80 characters each.

There MUST NOT be trailing whitespace at the end of non-blank lines.

Blank lines MAY be added to improve readability and to indicate related
blocks of code.

There MUST NOT be more than one statement per line.

## Indenting

Code MUST use an indent of 2 spaces, and MUST NOT use tabs for indenting.

> N.b.: Using only spaces, and not mixing spaces with tabs, helps to avoid
> problems with diffs, patches, history, and annotations. The use of spaces
> also makes it easy to insert fine-grained sub-indentation for inter-line
> alignment.

## Keywords and True/False/Null

PHP [keywords] MUST be in lower case.

The PHP constants `true`, `false`, and `null` MUST be in lower case.

[keywords]: http://php.net/manual/en/reserved.keywords.php

## Namespace and Use Declarations

When present, there MUST be one blank line after the `namespace` declaration.

When present, all `use` declarations MUST go after the `namespace`
declaration.

There MUST be one `use` keyword per declaration.

There MUST be one blank line after the `use` block.

For example:

```php
<?php
  namespace Vendor\Package;

  use FooClass;
  use BarClass as Bar;
  use OtherVendor\OtherPackage\BazClass;

  // ... additional PHP code ...
```

## Classes, Properties, and Methods

The term "class" refers to all classes, interfaces, and traits.

### Extends and Implements

The `extends` and `implements` keywords MUST be declared on the same line as
the class name.

The opening brace for the class MUST go on its own line; the closing brace
for the class MUST go on the next line after the body.

```php
<?php
  namespace Vendor\Package;

  use FooClass;
  use BarClass as Bar;
  use OtherVendor\OtherPackage\BazClass;

  class ClassName extends ParentClass implements \ArrayAccess, \Countable {
    // constants, properties, methods
  }
```

Lists of `implements` MAY be split across multiple lines, where each
subsequent line is indented once. When doing so, the first item in the list
MUST be on the next line, and there MUST be only one interface per line.

```php
<?php
  namespace Vendor\Package;

  use FooClass;
  use BarClass as Bar;
  use OtherVendor\OtherPackage\BazClass;

  class ClassName extends ParentClass implements
    \ArrayAccess,
    \Countable,
    \Serializable {
    // constants, properties, methods
  }
```

### Properties

Visibility MUST be declared on all properties.

The `var` keyword MUST NOT be used to declare a property.

There MUST NOT be more than one property declared per statement.

Property names SHOULD NOT be prefixed with a single underscore to indicate
protected or private visibility.

A property declaration looks like the following.

```php
<?php
  namespace Vendor\Package;

  class ClassName {
    public $foo = null;
  }
```

### Methods

Visibility MUST be declared on all methods.

Method names SHOULD NOT be prefixed with a single underscore to indicate
protected or private visibility.

Method names MUST NOT be declared with a space after the method name. The
opening brace MUST go on the same line, and the closing brace MUST go on the
next line following the body. There MUST NOT be a space after the opening
parenthesis, and there MUST NOT be a space before the closing parenthesis.

A method declaration looks like the following. Note the placement of
parentheses, commas, spaces, and braces:

```php
<?php
  namespace Vendor\Package;

  class ClassName {
    public function fooBarBaz($arg1, &$arg2, $arg3 = []) {
      // method body
    }
  }
```

### Method Arguments

In the argument list, there MUST NOT be a space before each comma, and there
MUST be one space after each comma.

Method arguments with default values MUST go at the end of the argument
list.

```php
<?php
  namespace Vendor\Package;

  class ClassName {
    public function foo($arg1, &$arg2, $arg3 = []) {
      // method body
    }
  }
```

Argument lists MAY be split across multiple lines, where each subsequent line
is indented once. When doing so, the first item in the list MUST be on the
next line, and there MUST be only one argument per line.

When the argument list is split across multiple lines, the closing parenthesis
and opening brace MUST be placed together on their own line with one space
between them.

```php
<?php
  namespace Vendor\Package;

  class ClassName {
    public function aVeryLongMethodName(
      ClassTypeHint $arg1,
      &$arg2,
      array $arg3 = []
    ) {
        // method body
    }
  }
```

### `abstract`, `final`, and `static`

When present, the `abstract` and `final` declarations MUST precede the
visibility declaration.

When present, the `static` declaration MUST come after the visibility
declaration.

```php
<?php
  namespace Vendor\Package;

  abstract class ClassName {
    protected static $foo;

    abstract protected function zim();

    final public static function bar() {
      // method body
    }
  }
```

### Method and Function Calls

When making a method or function call, there MUST NOT be a space between the
method or function name and the opening parenthesis, there MUST NOT be a space
after the opening parenthesis, and there MUST NOT be a space before the
closing parenthesis. In the argument list, there MUST NOT be a space before
each comma, and there MUST be one space after each comma.

```php
<?php

  bar();
  $foo->bar($arg1);
  Foo::bar($arg2, $arg3);
```

Argument lists MAY be split across multiple lines, where each subsequent line
is indented once. When doing so, the first item in the list MUST be on the
next line, and there MUST be only one argument per line.

```php
<?php
  $foo->bar(
    $longArgument,
    $longerArgument,
    $muchLongerArgument
  );
```

## Control Structures

The general style rules for control structures are as follows:

- There MUST be one space after the control structure keyword
- There MUST NOT be a space after the opening parenthesis
- There MUST NOT be a space before the closing parenthesis
- There MUST be one space between the closing parenthesis and the opening
  brace
- The structure body MUST be indented once
- The closing brace MUST be on the next line after the body

The body of each structure MUST be enclosed by braces. This standardizes how
the structures look, and reduces the likelihood of introducing errors as new
lines get added to the body.


### `if`, `elseif`, `else`

An `if` structure looks like the following. Note the placement of parentheses,
spaces, and braces; and that `else` and `elseif` are on the same line as the
closing brace from the earlier body.

```php
<?php
if ($expr1) {
  // if body
} elseif ($expr2) {
  // elseif body
} else {
  // else body;
}
```

The keyword `elseif` SHOULD be used instead of `else if` so that all control
keywords look like single words.


### `switch`, `case`

A `switch` structure looks like the following. Note the placement of
parentheses, spaces, and braces. The `case` statement MUST be indented once
from `switch`, and the `break` keyword (or other terminating keyword) MUST be
indented at the same level as the `case` body. There MUST be a comment such as
`// no break` when fall-through is intentional in a non-empty `case` body.

```php
<?php
  switch ($expr) {
    case 0:
      echo 'First case, with a break';
    break;
    
    case 1:
      echo 'Second case, which falls through';
      // no break
    case 2:
    case 3:
    case 4:
      echo 'Third case, return instead of break';
      return;
      
    default:
      echo 'Default case';
    break;
  }
```


### `while`, `do while`

A `while` statement looks like the following. Note the placement of
parentheses, spaces, and braces.

```php
<?php
  while ($expr) {
    // structure body
  }
```

Similarly, a `do while` statement looks like the following. Note the placement
of parentheses, spaces, and braces.

```php
<?php
  do {
    // structure body;
  } while ($expr);
```

### `for`

A `for` statement looks like the following. Note the placement of parentheses,
spaces, and braces.

```php
<?php
  for ($i = 0; $i < 10; $i++) {
    // for body
  }
```

### `foreach`

A `foreach` statement looks like the following. Note the placement of
parentheses, spaces, and braces.

```php
<?php
  foreach ($iterable as $key => $value) {
    // foreach body
  }
```

### `try`, `catch`

A `try catch` block looks like the following. Note the placement of
parentheses, spaces, and braces.

```php
<?php
  try {
    // try body
  } catch (FirstExceptionType $e) {
    // catch body
  } catch (OtherExceptionType $e) {
    // catch body
  }
```

## Closures

Closures MUST be declared with a space after the `function` keyword, and a
space before and after the `use` keyword.

The opening brace MUST go on the same line, and the closing brace MUST go on
the next line following the body.

There MUST NOT be a space after the opening parenthesis of the argument list
or variable list, and there MUST NOT be a space before the closing parenthesis
of the argument list or variable list.

In the argument list and variable list, there MUST NOT be a space before each
comma, and there MUST be one space after each comma.

Closure arguments with default values MUST go at the end of the argument
list.

A closure declaration looks like the following. Note the placement of
parentheses, commas, spaces, and braces:

```php
<?php
  $closureWithArgs = function ($arg1, $arg2) {
    // body
  };

  $closureWithArgsAndVars = function ($arg1, $arg2) use ($var1, $var2) {
    // body
  };
```

Argument lists and variable lists MAY be split across multiple lines, where
each subsequent line is indented once. When doing so, the first item in the
list MUST be on the next line, and there MUST be only one argument or variable
per line.

When the ending list (whether or arguments or variables) is split across
multiple lines, the closing parenthesis and opening brace MUST be placed
together on their own line with one space between them.

The following are examples of closures with and without argument lists and
variable lists split across multiple lines.

```php
<?php
  $longArgs_noVars = function (
    $longArgument,
    $longerArgument,
    $muchLongerArgument
  ) {
    // body
  };

  $noArgs_longVars = function () use (
    $longVar1,
    $longerVar2,
    $muchLongerVar3
  ) {
    // body
  };

  $longArgs_longVars = function (
    $longArgument,
    $longerArgument,
    $muchLongerArgument
  ) use (
    $longVar1,
    $longerVar2,
    $muchLongerVar3
  ) {
    // body
  };

  $longArgs_shortVars = function (
    $longArgument,
    $longerArgument,
    $muchLongerArgument
  ) use ($var1) {
    // body
  };

  $shortArgs_longVars = function ($arg) use (
    $longVar1,
    $longerVar2,
    $muchLongerVar3
  ) {
    // body
  };
```

Note that the formatting rules also apply when the closure is used directly
in a function or method call as an argument.

```php
<?php
  $foo->bar(
    $arg1,
    function ($arg2) use ($var1) {
      // body
    },
    $arg3
  );
```