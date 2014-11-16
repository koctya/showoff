!SLIDE subsection

# Ruby Basics #

!SLIDE
- Why Learn Ruby
	- Ruby is easy to read
	- Completely object-oriented
	- Ruby follows POLS (Principle of Least Surprise)
	- Ruby has a REPL

!SLIDE small

Ruby was first released to the public in 1995 by Matz (Yukihiro Matzimoto)

- Ruby was more popular than Python in Japan already by 2000 arnd allegedly almost as popular as Perl by 2004
- Ruby was designed to be beautiful, fun
- It comes with a standard documentation system ‘RDoc’,
	- a standard packaging system ‘RubyGems’,
	- an interactive shell ‘irb’,
	- the Ruby VM and a lot of frameworks and a standard library.

!SLIDE small

- Objects are garbage collected
-  Like with Smalltalk and Objective-C, objects respond to messages
	 - Such messages contain a method’s name together with the parameters that the method may need
-  Ruby is a single inheritance language
	- provides Mixin's

!SLIDE

A key point in the spread of Ruby was the release of “Programming Ruby,” also called the “Pickaxe” (a reference to its cover illustration), by the Pragmatic Programmers. “Programming Ruby” was the first comprehensive English guide to the language and API.

!SLIDE

# Ruby has a REPL
(Read-Eval-Print Loop), which makes prototyping very fast
## Interactive Ruby - IRB #

	➜  ~  irb
	>> 1 + 2
	=> 3
	>>

### [Pry](http://pryrepl.org) a better irb

!SLIDE small

# Files
Ruby files end in `.rb`

!SLIDE small

## Single Line Ruby Comments

Single line comments in a Ruby script are defined with the '#' character.

	@@@ ruby
	# I am a single line comment

!SLIDE small

## Multi Line or Block Ruby Comments
Multiple lines of text or code can be defined as comments using the Ruby =begin and =end comment markers.

	@@@ ruby
	=begin
	This is a comment line
	it explains that the next line of code displays
	a welcome message
	=end

!SLIDE small

### Constants
Constants are declared by beginning the variable name with a capital letter

	@@@ ruby
	MYCONSTANT = "hello"
	#=> "hello"


!SLIDE small


## Ruby Variables


### Identifying a Ruby Variable Type

Once a Ruby variable has been declared it can often be helpful to find out the variable type.
This can be achieved using the kind_of? method of the Object class.

	@@@ ruby
	y.kind_of? Integer
	# => true


!SLIDE small

## Variable Scope?


	|Name Begins With	| Variable Scope		|
	| $					| A global variable		|
	| @	 				| An instance variable	|
	| [a-z] or _		| A local variable		|
	| [A-Z]				| A constant			|
	| @@				| A class variable		|

!SLIDE


Ruby provides a number of built-in number classes.

- Number Classes
	 - Integer
	 	- The base class from which the following number classes are derived.

	 - Fixnum
	 	- A Fixnum holds Integer values that can be represented in a native machine word (minus 1 bit).

!SLIDE small

- Number Classes (Cont)
	 - Bignum
	 	- Bignum objects hold integers that fall outside the range of the Ruby Fixnum class.

	 - Float
	 	- The Float object represents real numbers based on the native architecture‘s
	 double-precision floating point representation.

	 - Rational
		- Rational implements a rational class for numbers.

!SLIDE small

## Ruby Operators

	Operator	Description
	+			Addition
	-			Subtraction
	*			Multiplication
	/			Division
	%			Modulus - returns remainder
	**			Exponent

!SLIDE small

### Parallel Assignment

	@@@ ruby
	a, b, c = 10, 20, 30
	# => [10, 20, 30]
	a
	# => 10
	b
	# => 20
	c
	# => 30

Want to swap two values?

	@@@ ruby
	x, y = y, x

!SLIDE small

Comparison Operators

	Comparison 	Operator	Description
	==			Tests for equality.
	.eql?					Same as ==.
	!=			Tests for inequality.
	<			Less than.
	>			Greater than. R
	>=			Greater than or equal to.
	<=			Less than or equal to.
	<=>			Combined comparison operator.

`<=>` Returns 0 if first operand equals second, 1 if first operand is greater than the second and -1 if first operand is less than the second.

!SLIDE small

### Bitwise Operators


	Combined Operator	Equivalent
	~					Bitwise NOT (Complement)
	|					Bitwise OR
	&					Bitwise AND
	^					Bitwise Exclusive OR
	<<					Bitwise Shift Left
	>>					Bitwise Shift Right



!SLIDE small

## Logical Operators

### `and &&`

	@@@ ruby
	var1 = 20
	var2 = 60
	var1 < 25 and var2 > 45
	=> true

###  `or ||`

	@@@ ruby
	var1 < 25 or var2 > 45
	=> true

 `not !`

	@@@ ruby
	>> 10 == 10
	=> true
	>> not 10 == 10
	=> false

!SLIDE small

### Ruby Sequence Ranges

Sequence ranges in Ruby are used to create a range of successive values - consisting of a start value, an end value and a range of values in between.

Two operators are available for creating ranges

`-` inclusive two-dot operator (..)
`-` exclusive three-dot operator (...)

	@@@ ruby
	1..10    # Creates a range from 1 to 10 inclusive
	1...10   # Creates a range from 1 to 9


!SLIDE small

## Ruby Array

A Ruby array is an object that contains a number of items.
Those items can be variables (such as String, Integer, Fixnum Hash etc) or even other objects (including other arrays to make a multidimensional array)

	@@@ ruby
	days_of_week = Array.new
	days_of_week.empty?
	#=> true

!SLIDE small
##  Array (Cont)
Another option is to use the [] method of the Array class to specify the elements one by one:

	@@@ ruby
	days_of_week = Array[ "Mon", "Tues", "Wed",
		"Thu", "Fri", "Sat", "Sun" ]
	# => ["Mon", "Tues", "Wed",
	#     "Thu", "Fri", "Sat", "Sun"]

	days_of_week.size
	# => 7

!SLIDE small

### Accessing Array Elements with the [] method

	@@@ ruby
	days_of_week[0]
	# => "Mon"

	days_of_week[1]
	# => "Tues"

	days_of_week.each {|day| puts day}

### Finding the Index of an Element

	@@@ ruby
	days_of_week.index("Wed")
	# => 2

!SLIDE small

### Specify a range.

	@@@ ruby
	days_of_week[1..3]
	# => ["Tues", "Wed", "Thu"]

!SLIDE
## Ruby Hash
	@@@ ruby
	h1 = Hash.new
	h1["a"] = 100
	h1["b"] = 200


!SLIDE

##  Hash (cont)
Create a hash directly

	@@@ ruby
	h2 = {a: 100, b: 200, c: 300}
	h2.each_key {|key| puts key}

	puts h1["c"]
	# => 300