!SLIDE subsection

## Blocks

!SLIDE

> the Highly Sparkling Glint on the Edge of Ruby

The real power of blocks is when dealing with things that are more complicated than lists.

Beyond handling simple housekeeping details within the method,

you can also handle setup, teardown, and errors—all hidden away from the cares of the user.

!SLIDE

## Blocks are Objects, they just don’t know it yet

Blocks (closures, really) are heavily used by the standard library. To call a block, you can either use yield, or make it a Proc by appending a special argument to the argument list, like so:

	@@@ ruby
	def adder(&the_block)
	  # Inside here, the_block is the
	  # block passed to the method
	  the_block # return the block
	end
	adr = adder { |a, b| a + b }
	# adr is now a Proc object
	adr.class # => Proc

!SLIDE
	@@@ ruby
	adr.call(10, 5)

You can create blocks outside of method calls, too, by calling Proc.new with a block or calling the lambda method.

Similarly, methods are also Objects in the making:

	@@@ ruby
	method(:puts).call "puts is an object!"
	# => puts is an object!

!SLIDE

Within a method the block may be invoked using the yield statement (Python 3000 will also have one)
- Whenever a yield is executed it invokes the block
- You can pass parameters to them and receive values

from them e.g.,

	@@@ ruby
	def two_times
	    yield
	    yield
	End
	two_times {puts “Hello”}

!SLIDE

## Classes are open
Ruby classes are open. You can open them up, add to them, and change them at any time. Even core classes, like Fixnum or even Object, the parent of all objects. Ruby on Rails defines a bunch of methods for dealing with time on Fixnum. Watch:

	@@@ ruby
	class Fixnum
	  def hours
	  	# number of seconds in an hour
	    self * 3600
	  end
	  alias hour hours
	end

!SLIDE

	@@@ ruby
	# 14 hours from 00:00 January 1st
	# (aka when you finally wake up ;)
	Time.mktime(2006, 01, 01) + 14.hours
	# => Sun Jan 01 14:00:00

!SLIDE

### Altering Classes—It’s Never Too Late
But what if you want to be able to view or change the name?

Ruby provides an easy way of providing access to an object’s variables.

	@@@ ruby
	class Greeter
	    attr_accessor :name
	end

In Ruby, you can open a class up again and modify it.

!SLIDE

	> g.respond_to?("name")
	=> true
	> g.respond_to?("name=")
	=> true

Using the attr_accessor defined two new methods (as opposed to doing it manually) for the existing Greeter class which became available to the instantiated g object!

!SLIDE

### Altering Classes ***"Monkey Patching"***

> With great power comes great responsibility

	- Uncle Ben

!SLIDE

## Missing methods
Ruby doesn’t give up if it can’t find a method that responds to a particular message.

It calls the `method_missing` method with the name of the method it couldn’t find and the arguments.

By default, `method_missing` raises a `NameError` exception, but you can redefine it to better fit your application, and many libraries do.

!SLIDE

 Here is an example:

	@@@ ruby
	# id is the name of the method called,
	# the * syntax collects all the
	#  arguments in an array named 'arguments'
	def method_missing(id, *args)
	  puts "Method #{id} was called, " +
	  		"but not found. It has " +
	       "these arguments: " +
		   "#{args.join(", ")}"
	end
	__ :a, :b, 10
	# => Method __ was called, but not found.
	# It has these arguments: a, b, 10

 you are free to handle the message in any way that is appropriate.

!SLIDE small

## Closures
A closure is a function that remembers the context in which it was created
They can be useful to implement callbacks

	@@@ ruby
	class ButtonController
	  def initialize(label, &action)
	    @label = label
	    @action = action
	  end
	  def press
	    @action.call @label
	  end
	end
	# ...
	start = ButtonController.new "Start" { thrd.start }
	pause = ButtonController.new "Pause" { thrd.pause }

!SLIDE small

Closure's environment is a reference, not a copy (more on this later)
Most commonly created with blocks or lambda method

	@@@ ruby
	def mkcounter(a)
	  lambda { a += 1; puts "#{a}" }
	end

lambda creates a Proc object with the associated block

	@@@ ruby
	c1 = mkcounter(10)
	c1.call
	# => 11

Blocks are not objects, but they can be converted into objects of class Proc. This can be done by calling the lambda method of the class Object. A block created with lambda acts like a Ruby method.

!SLIDE

Ruby 1.9 now introduces an new, more concise syntax for creating lambda functions:

	@@@ ruby
	x = ->{puts "Hello Lambda"}

!SLIDE

## Message passing, not function calls
A method call is really a message to another object:

	@@@ ruby
	# This
	1 + 2
	# Is the same as this ...
	1.+(2)
	# Which is the same as this:
	1.send "+", 2

!SLIDE

## Operators are syntactic sugar
Most operators in Ruby are just syntactic sugar (with some precedence rules) for method calls.

You can, for example, override Fixnums + method:

	@@@ ruby
	class Fixnum
	  # You can, but please don't do this
	  def +(other)
	    self - other
	  end
	end

!SLIDE

You don’t need C++’s operator+, etc.

You can even have array-style access if you define the [] and []= methods.

To define the unary + and - (think +1 and -2), you must define the +@ and -@ methods, respectively.

The operators below are not syntactic sugar, though. They are not methods, and cannot be redefined:

=, .., ..., !, not, &&, and, ||, or, !=, !~, ::

!SLIDE

## Exceptions
Catch exceptions with begin and rescue

	@@@ ruby
	begin
	  File.open("/etc/passwd") do |f|
	    puts f.gets
	  end
	rescue => e
	  $stderr.puts "error: #{e.message}"
	end

!SLIDE

`ensure` makes sure code is called regardless of outcome

	@@@ ruby
	f = nil
	begin
	  f = File.open "/etc/passwd"
	  # ... process f here ...
	rescue => e
	  $stderr.puts "error: #{e.message}"
	ensure
	  f.close unless f.nil?
	end

!SLIDE

# Regular Expressions
Ruby has first-class support for regexps
Syntax was largely lifted from Perl

	@@@ ruby
	if "hello" =~ /ell/
	  puts "Yea! my regexp matched!"
	end

!~ is the compliment to =~ operator

