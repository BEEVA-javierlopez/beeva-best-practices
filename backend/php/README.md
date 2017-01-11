
![PHP logo](static/php-logo.png "PHP logo")

# PHP Basic Coding Standard, Style Guide & Best Practices

## INDEX

* [1. Introduction](#1-introduction)
* [2. Coding Standard](#2-coding-standard)
* [3. Style Guide](#3-style-guide)
* [4. Namespace and class names](#4-namespace-and-class-names)
* [5. Constants and methods](#5-Class-constants,-properties-and-methods)
* [6. Error Handling](#6-Error-handling)
* [7. Securize SQL query](#7-Securize-SQL-query)
* [8. References](#8-References)

## 1. Introduction

This guide contains procedures and advices, collected from different sources, our experience programming with PHP over time and documentation extracted from PSR1 / PSR2 standard [PHP Style Guide](http://www.php-fig.org/).


## 2. Coding Standard

* Files MUST use the long `<?php ?>` tags or the short-echo `<?= ?>` tags.

* Files MUST use only UTF-8 without BOM for PHP code.

* Files SHOULD either declare symbols (classes, functions, constants, etc.) or cause side-effects (e.g. generate output, change .ini settings, etc.) but SHOULD NOT do both.

* Class names MUST be declared in `StudlyCaps`.

* Class constants MUST be declared in all upper case with underscore separators.

* Method names MUST be declared in `camelCase`.


## 3. Style Guide

### General

* Code MUST use 4 spaces for indenting, not tabs.

* There MUST NOT be a hard limit on line length; the soft limit MUST be 120 characters; lines SHOULD be 80 characters or less.

* There MUST be one blank line after the `namespace` declaration, and there MUST be one blank line after the block of `use` declarations.

* Opening braces for classes MUST go on the next line, and closing braces MUST go on the next line after the body.

* Opening braces for methods MUST go on the next line, and closing braces MUST go on the next line after the body.

* Visibility MUST be declared on all properties and methods; `abstract` and `final` MUST be declared before the visibility; `static` MUST be declared after the visibility.

* Control structure keywords MUST have one space after them; method and function calls MUST NOT.

* Opening braces for control structures MUST go on the same line, and closing braces MUST go on the next line after the body.

* Opening parentheses for control structures MUST NOT have a space after them, and closing parentheses for control structures MUST NOT have a space before.


### Files

* All PHP files MUST use the Unix LF (linefeed) line ending.

* All PHP files MUST end with a single blank line.

* The closing `?>` tag MUST be omitted from files containing only PHP.


### Lines

* There MUST NOT be a hard limit on line length.

* The soft limit on line length MUST be 120 characters; automated style checkers MUST warn but MUST NOT error at the soft limit.

* Lines SHOULD NOT be longer than 80 characters; lines longer than that SHOULD be split into multiple subsequent lines of no more than 80 characters each.

* There MUST NOT be trailing whitespace at the end of non-blank lines.

* Blank lines MAY be added to improve readability and to indicate related blocks of code.

* There MUST NOT be more than one statement per line. 


### Indenting

* Code MUST use an indent of 4 spaces, and MUST NOT use tabs for indenting.

* Using only spaces and not mixing spaces with tabs.


### Lowercase

* The PHP constants `true`, `false`, and `null` MUST be in lower case.


### Style guide example:

```Php
  <?php
  namespace Vendor\Package;

  use FooInterface;
  use BarClass as Bar;
  use OtherVendor\OtherPackage\BazClass;

  class Foo extends Bar implements FooInterface
  {
      public function sampleMethod($a, $b = null)
      {
          if ($a === $b) {
              bar();
          } elseif ($a > $b) {
              $foo->bar($arg1);
          } else {
              BazClass::bar($arg2, $arg3);
          }
      }

      final public static function bar()
      {
          // method body
      }
  }

  ?>
```

## 4. Namespace and class names

* Class names MUST be declared in `StudlyCaps` for PHP 5.3 or later.

```Php
  <?php
  namespace Vendor\Model;

  class Foo
  {
  }

  ?>
```

## 5. Constants and methods

### Constants

* Class constants MUST be declared in all upper case with underscore separators.

```Php
  <?php
  namespace Vendor\Model;

  class Foo
  {
      const COMPANY = 'BEEVA';
      const DATE_APPROVED = '01-01-2017';
  }

  ?>
```

### Methods

* Method names MUST be declared in `camelCase()`.

## 6. Error handling

### Throw, Catch and Finally

* Exceptions can be `thrown` within a catch block.

* Normal execution (when no exception is thrown within the try block) will continue after that last `catch` block.

* When an exception is `thrown`, code following the statement will not be executed.

* A `finally` block may also be specified after or instead of catch blocks.

```Php
    <?php
    function inverse($x) {
        if (!$x) {
            throw new Exception('Division by zero.');
        }
        return 1/$x;
    }

    try {
        echo inverse(2) . "\n";
    } catch (Exception $e) {
        echo "Caught exception: ".$e->getMessage();
    } finally {
        echo "Finally";
    }

    ?>
```
## 7. Securize SQL querys

Use prepared statements and parameterized queries. These are SQL statements that are sent to and parsed by the database server separately from any parameters. This way it is impossible for an attacker to inject malicious SQL.

### Example using mysqli

```Php
    <?php

    $unsafe_variable = $_POST["email"];

    if($unsafe_variable != ""){
        $mysqli = new mysqli("localhost", "testdb", "1234", "user");

        $stmt = $mysqli->prepare("INSERT INTO emails (email) VALUES (?)");

        // "s" means the database expects a string
        $stmt->bind_param("s", $unsafe_variable);

        $stmt->execute();

        $stmt->close();

        $mysqli->close();

        echo "Email saved.";
    }

    ?>
```

## 8. References

Please follow the links in order to obtain further information regarding Ruby programming and best practices:

* http://www.php-fig.org/
* http://www.hongkiat.com/blog/php7/
* http://php.net/

___

[BEEVA](https://www.beeva.com) | Technology and innovative solutions for companies
