<!-- permalink: d48661e13dd2cbf9222d29beb4662bef DO NOT DELETE OR EDIT THIS LINE -->
# PHP OOP

Notes taken at a conference - incomplete

* method and properties
	* `private` is accessible only within class
	* `public` is accessible anywhere
	* `protected` is available only to descendent

* constants:
	* `const PI = 3.14159;`

* static methods
	* analogous to *class method* in swift/objc
		* `classname::method`
		* `Math::circularArea(5)`


## Inheritance

```
class Person {
	public $first;
	public $last;
}

class Employee extends Person {
	public $title;
}
```

* accessing parent
	* `parent::[methodnamenobrackets]`

* stopping Inheritance
	* `final` keyword
		* works on both classes and methods

## Abstract classes

```
abstract class DataStore {
	//These methods must be defined in the child class
	abstract public function save();
	abstract public function load($id);

}
```

* abstract contract
	* all abstract methods must be implemented
	* method signatures must match exactly

* interfaces
	* interface defines method signatures that an implementing class must provide
	* similar to abstract methods but sharable between classes
	* no code, no properties, just an interoperability framework

```
interface Rateable {
	public function rate( int $stars, $user);
	public function getRating();
}
```

* interface implementation

```
class StatusUpdate implements Rateable, Searchable {
	protected $ratings[];

	public function rate(int $stars, $user) {
		$this->ratings[$user] = $stars;
	}

	public function search($query) {
		// search stuff
	}
}
```

## Traits

```
trait Counter {
	protected $counter;

	public function increment() {
		$counter ++;
	}

	public funciton getCounter() {
		return $counter;
	}
}

class MyCounter {
	use Counter;
}

$counter = new MyCounter();
$counter->increment();
echo $counter->getCount(); //1
```

## Late Static Binding

* insert stuff here


## Namespaces
```
<?php
namespace WorkLibrary;

class Database {
	//stuff
}

.....

<?php
namespace MyLibrary;

class Database {
	// stuff
}
```
* usage:
	* `$db = MyLibrary\Database::connect();`
	* `use MyLibrary\Database;`
		* `$db = Database::connect();`
	* `use MyLibrary\Database as MyD;`;
		* `$model = new MyD();`
	* using built in classes with toplevel
		* `$images = new \DateTime();`

* backslash `\` allows for sub-namespaces as a separator


## Magic Methods
* magic methods start with `__`
* allow for code that is not directly called to run
* often have counterparts:
	* `__construct()` and `__destruct()`
	* `__set()` and `__get()`
