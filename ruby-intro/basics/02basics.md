!SLIDE subsection

## Ruby Object Oriented Programming

### What is an Object?

An object is a self-contained piece of functionality that can be easily used,
and re-used as the building blocks for a software application.

### Everything in Ruby is an object, including nil
No wrappers needed!

	>> nil.inspect
	=> "nil"
	>> 3.inspect
	=> "3"

!SLIDE execute

## Declaring and Calling a Ruby Method

The following simple example shows a method defined and called.

	@@@ ruby
	def saysomething()
	    puts "Hello"
	end

!SLIDE execute
.notes What’s the #{name} bit? That’s Ruby’s way of inserting something into a string.

### Passing Arguments to a Method

	@@@ ruby
	def h(name)
		puts "Hello #{name}"
	end

	result = h "Matz"


!SLIDE

### Variable Number of Arguments to a Method

This achieved by using *args when declaring the method.
The arguments passed to the method are then placed in an array

	@@@ ruby
	def displaystrings( *args )
		args.each {|string| puts string}
	end

!SLIDE

### Defining a Ruby Class

	@@@ ruby
	class Greeter
	    def initialize(name = “world”)
			@name = name
		end

		def say_hi
		    puts “Hi #{@name.capitalize}”
		end
	end

!SLIDE

### Creating an Object from a Class

An object is created from a class using the new method.

	@@@ ruby
	g = Greeter.new(“john”)

Let’s see what is inside the object:

	> Greeter.instance_methods

	> g.respond_to?("name") => false
	> g.respond_to?("say_hi") => true
	> g.respond_to?("to_s") => true

!SLIDE small
.notes

## Ruby Class Inheritance

	@@@ ruby
	class X
	  # ...
	end

	class Y < X
	  # ...
	end

!SLIDE small

## Modules And Mix-Ins
Ruby has single inheritance only, so instead, they have "mix-ins"
Modules can't be instantiated, but their methods and data can be made available to other classes and objects
Defining a module is very similar to a class

	@@@ ruby
	module X
	  # ...
	end

	class Y
	  include X
	  # ...
	end

Notice I said classes and objects; here's how to mix-in a Module to an object...

	@@@ ruby
	obj.extend MyModule

!SLIDE

## Modules Group Code by Topic
Math is a built-in module for mathematics. Modules serve two roles in Ruby.
This shows one role: grouping similar methods together under a familiar name.

	>> Math.sqrt(9+16)
	=> 5.0

!SLIDE small

## Mixins

### we simply inherit from BankAccount and add new instance variable:

	@@@ ruby
	# if BankAccount is in external source file.
	require 'BankAccount'

	class NewBankAccount < BankAccount
	   def customerPhone
	        @customerPhone
	   end

	   def customerPhone=( value )
	        @customerPhone = value
	   end
	end

!SLIDE

## Symbols are not lightweight Strings
Many Ruby newbies struggle with understanding what Symbols are, and what they can be used for.

Symbols can best be described as identities. A symbol is all about who it is, not what it is.
Fire up irb and see the difference:

	@@@ ruby
	:mike.object_id == :mike.object_id
	# => true
	"mike".object_id == "mike".object_id
	# => false

!SLIDE

## Keyword arguments
Like in Python, since Ruby 2.0 methods can be defined using keyword arguments:

	@@@ ruby
	def deliver(from: "A", to: nil, via: "mail")
	  "Sending from #{from} to #{to} via #{via}."
	end
	deliver(to: "B")
	# => "Sending from A to B via mail."
	deliver(via: "Pony Express", from: "B", to: "A")
	# => "Sending from B to A via Pony Express."

!SLIDE execute

!SLIDE small

## Conditionals if, else Statement

	@@@ ruby
	if i < 10
	   puts "Student failed"
	else
	   puts "Student passed"
	end

!SLIDE small

## unless statement
**unless** works like **if not**

	@@@ ruby
	unless i >= 10 puts "Student failed"

!SLIDE small

	@@@ ruby
	def greets(name)
		puts "Hello #{name}" if name
		puts "Hello" unless name
	end

!SLIDE small

## Dynamic Typing “Duck Typing”
Many languages such as Java and C use what is known as strong or static variable typing.
This means that when you declare a variable in your application code you must define the variable type.

 	“if it walks like a duck and quacks like a duck…”.

The benefit of this is that it doesn’t unnecessarily restrict the types of variables that are supported.
If someone comes up with a new kind of list class, as long as it implements the join method with the same semantics as other lists, everything will work as planned.

!SLIDE small

# Duck Typing (cont)
Calling methods on objects based on desired behavior, not class
For this to work, need consistent method naming and behavior
<< is a good example

x << "yet another line"

This code works whether x is a String, Array or IO

!SLIDE small
Don't use `instance_of?`; use `respond_to?`

	@@@ ruby
	if x.respond_to? :<<
	  x << y
	elsif x.respond_to? :append
	  x.append y
	else
	  raise "no way to append"
	end


!SLIDE small

## **case** Statement

	@@@ ruby
	car = "Miata"
	manufacturer = case car
	   when "Mustang" 	then "Ford"
	   when "911" 		then "Porsche"
	   when "Miata" 	then "Mazda"
	   when "Civic" 	then "Honda"
	   else "Unknown"
	end

!SLIDE small

## Looping

Java, other imperative languages

	@@@ Java
	for (i=0; i<number_of_elements; i++)
	{
	  do_something_with(element[i]);
	}

This works, but isn’t very elegant.
You need a throw-away variable like i, have to figure out how long the list is,
and have to explain how to walk over the list.

!SLIDE small

## The Ruby for Loop

	@@@ ruby
	for i in (1..10)
	  puts i
	end

!SLIDE small
.notes ### We don't need no stinking For!

### The Ruby times Method

The times method provides an extremely convenient alternative to the for loop.

	@@@ ruby
	5.times { |i| puts i }

### The Ruby `upto` Method (also `downto`)

	@@@ ruby
	5.upto(10) do
	   puts "hello"
	end

!SLIDE small

## The Ruby While Loop

	@@@ ruby
	while expression do
		# ruby code here ...
	end

### until

	@@@ ruby
	i = 0
	until i == 5
	   puts i
	   i += 1
	end

!SLIDE small

## The Ruby way is much more elegant
All the housekeeping details are hidden within the each method,

	@@@ ruby
	@names = ["Kurt", "Teja", "Michael", "Reita"]

	@names.each do |name|
	  puts "Hello #{name}!"
	end

If the @names object responds to each, it is something that you can iterate over,
so iterate over it and greet each person in turn.

For more info on each (and its friends collect, find, inject, sort, etc.), see ri Enumerable
!SLIDE

	@@@ ruby
	["rantanplan", "milu"].include?("scooby") #=> false

!SLIDE

## Ruby Strings

	@@@ ruby
	myString = String.new("This a my string.")

	myString = "This is also my string"

Strings can be delimited using either double quotes *"* or single quotes *'*.

The double quotes are designed to interpret escaped characters such as new lines and tabs so that they appear as actual new lines and tabs when the string is rendered for the user.

Single quotes, however, display the actual escape sequence, for example displaying \n instead of a new line.

!SLIDE small

Ruby Here Documents

A Here Document (or heredoc as it is more commonly referred to) provides a mechanism for creating free format strings

	@@@ ruby
	myText = <<DOC
	Please Detach and return this coupon
	with your payment.
	Do not send cash or coins.

	Please write your name and account number
	on the check and
	make checks payable to:

	        Acme Corporation

	Thank you for your business.
	DOC

!SLIDE
## Ruby Symbols

Symbols make good hash keys for a few reasons:

- They're immutable, meaning they can't be changed once they're created;
- Only one copy of any symbol exists at a given time, so they save memory;
- Symbol-as-keys are faster than strings-as-keys because of the above two reasons.