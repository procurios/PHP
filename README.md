# PHP style guide

## Why does style matter

At Procurios we design, build and maintain our own platform with more than 20 developers, pushing hundreds of commits to our central git repository every day. At this moment (2015) our codebase contains about 3 million [lines of code](http://www.informationisbeautiful.net/visualizations/million-lines-of-code/).

A significant part of our work is [tending our software garden](http://blog.codinghorror.com/tending-your-software-garden/): weeding, pruning and tidying up our code, to keep it healthy and allow new features to grow.

We read and improve our code frequently. It must be readable, debuggable, maintainable. A consistent code style helps a lot.

Our style guide consists of two parts, code style and coding habits.

## Code style

### PSR standards

We basically follow the coding style related [PSR standards](http://www.php-fig.org/psr/) issued by the PHP Framework Interoperability Group:

* [PSR-1: Basic Coding Standard](http://www.php-fig.org/psr/psr-1/)
* [PSR-2: Coding Style Guide](http://www.php-fig.org/psr/psr-2/)
* [PSR-12: Extended Coding Style Guide](https://github.com/php-fig/fig-standards/blob/master/proposed/extended-coding-style-guide.md) (draft)

### Differences from PSR

#### Objects vs. Primitive types

The name of a variable or property that is an object MUST be declared in PascalCase.
The name of a variable or property that is a primitive type MUST be declared in camelCase.

```php
// bad
$date = new DateTime();
$Count = 1;

// good
$Date = new DateTime();
$count = 1;
```

#### Spaces around concatenation

The string concatenation operator MUST be preceded and followed by a space.

```php
// bad
$string = 'Hello '.$name;

// good
$string = 'Hello ' . $name;
```

#### Naming

About the names of identifiers like classes, functions, methods, variables:

* A name SHOULD be descriptive, distinctive, precise and readable.
* A name SHOULD NOT be abbreviated.
* A name SHOULD NOT be pre- or postfixed with Interface, Trait or Abstract.

A long name is not a problem, since our IDE has auto completion.

#### Inter-line alignment

Consecutive assignments or declarations SHOULD NOT be aligned. Adding one item may require you to re-align the other items, resulting in unnecessary changes in your commit.

```php
// bad
$short        = 1;
$veryLongItem = 2;

// good
$short = 1;
$veryLongItem = 2;
```

### DocBlock documentation

Every class, property and method MUST be preceded by a DocBlock comment.

Class DocBlocks:

* It MUST contain an @author tag.
* It MAY contain documentation about the class.

Property DocBlocks:

* It MUST contain a @var tag indicating the type of the property.
* It MAY contain documentation about the property.

Method DocBlocks:

* It MUST contain @param tags for every parameter of the method.
* It MUST contain a @return tag if the method returns something.
* It SHOULD contain a @throws tag if the method throws an Exception.
* It MAY contain documentation about the method.

Example:

```php
/**
 * @author John Doe
 */
class Foo
{
	/**
	 * @var array
	 */
	private $foo = [];

	/**
	 * @param array $foo
	 * @return int
	 */
	private function setFooAndReturnNumberOfItems(array $foo)
	{
		$this->foo = $foo;
		return count($this->foo);
	}
}
```


## Coding practices

What makes good code?

There isn't one answer, nor one authoritative list of criteria. It depends on the language, the requirements, the purpose of the code, and a bit on personal taste.

Many great books have been written about good code and being a good coder. This is our list of recommended reads:

* [Robert C. Martin - Clean Code](http://www.amazon.com/dp/0132350882)
* [Robert C. Martin - The Clean Coder](http://www.amazon.com/dp/0137081073)
* [Martin Fowler - Patterns of Enterprise Application Architecture](http://www.amazon.com/dp/0321127420)
* [Martin Fowler - Refactoring: Improving the Design of Existing Code](http://www.amazon.com/dp/0201485672)
* [Steve McConnell - Code Complete 2](http://www.amazon.com/dp/0735619670)
* [Eric Evans - Domain-Driven Design](http://www.amazon.com/dp/0321125215)

We have gathered some of the rules of thumb that help us write better code.

### Be strict

PHP is a dynamically typed language. Careless [type juggling](http://php.net/manual/en/language.types.type-juggling.php) can lead to unpredictable code behaviour and hard-to-find bugs.

Be as strict as possible:

* Use type hints
* Use strict comparisons (=== and !==)
* Use value objects that check their arguments
* Use constants for values that are used more than once

### Optimize for code completion

If your editor can complete your code, you'll likely make less mistakes. And your editor can refactor your code later on.

* Use constants instead of string values
* Use value objects instead of associative arrays
* Use exceptions instead of return types

### Optimize for readability

You write code only once, but it is read (and changed) many times. Write your code so that other developers can easily understand it.

Quoting Martin Fowler:

> Any fool can write code that a computer can understand.<br />
> Good programmers write code that humans can understand.

* Prefer simple solutions over complex solutions. No over-engineering. No premature optimization. No premature abstraction.
* Be consistent in approach, naming and structure with the rest of the codebase. Do not reinvent the wheel.
* Write documentation explaining why the code exists, not what it does. Don't state the obvious.
* Use [object calisthenics](http://williamdurand.fr/2013/06/03/object-calisthenics/).

Not only on the scale of a method should your code be readable. Let the methods of a class tell the story of the class.

### No assumptions

Do not assume that:

* input will be sane
* all users are benevolent
* other developers don't make mistakes
* external services are always available and don't change

Don't ignore errors, edge cases or faulty input. If something is really wrong, stop immediately with a descriptive and distinctive error.

## Conventions

### Example data

##### URLs
Use example.com, example.org and example.net for all example URLs and email addresses, per [RFC 2606](http://www.faqs.org/rfcs/rfc2606).

##### Names
Use english names like John Doe, Alice or Bob. Never use customer names.

##### Identifiers
For sample or temporary code, always use [meta syntactic variables](http://www.jargon.net/jargonfile/m/metasyntacticvariable.html) like `$foo`, `$bar`, `$baz` and `$quux`.
