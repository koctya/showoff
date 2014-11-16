!SLIDE subsection
# Ruby Idioms #

!SLIDE

### Use expressions instead of statements
Instead of:

	@@@ ruby
	if hour > 10
	  greeting = "hello"
	else
	  greeting = "bye"
	end
You may write:

	@@@ ruby
	greeting = if hour > 10
	  "hello"
	else
	  "bye"
	end

!SLIDE

Use an script both as library or executable

	@@@ ruby
	if __FILE__ == $0
	  # this script was not imported
	  # but executed, do something
	  # interesting here
	end

`__FILE__` is the name of the current source file

`$0` at the top level is the name of the top-level program being executed

!SLIDE

`$:` is an array of paths to look for Ruby scripts to load

`$!` is the current Exception passed to raise

ENV is a Hash of environment variables

ARGV is an Array of command-line args (synonym for $*)

!SLIDE

Unpack enumerables in block arguments
No:

	@@@ ruby
	[[1, 2], [3, 5]].map do |array|
	  array[0] - array[1]
	end # [1, 2]
Yes:

	@@@ ruby
	[[1, 2], [3, 5]].map do |v1, v2|
	  v2 - v1
	end # [1, 2]

!SLIDE

Method arguments
No:

	@@@ ruby
	def method(arg1, arg2, arg3=1,
		arg4="hello", arg5="bye")
	  ...
	end
Yes:

	@@@ ruby
	def method(arg1, arg2, options = {})
	  options = {
	    :arg3 => 1,
	    :arg4 => "hello",
	    :arg5 => "bye",
	  }.merge(options)
	  ...
	end

!SLIDE
Ruby's objects are always truish except for nil and false,
so the only valid reason to write the verbose object.nil? would be for telling nil from false.

Testing for truth values
No, no, no:

	@@@ ruby
	if !some_object.nil?
	  ...
	end
Yes:

	@@@ ruby
	if some_object
	  ...
	end

!SLIDE

## Funny method names
In Ruby, methods are allowed to end with question marks or exclamation marks.

Methods ending in ? are predicates (Boolean queries)

	@@@ ruby
	if File.readable? "/etc/password"
	  PasswordCracker.run "/etc/password"
	end

!SLIDE

Methods ending in ! are dangerous, meaning that they modify the receiver

	@@@ ruby
	str = "   hello world   "
	str.strip!
	p str   # -> "hello world"

	database.destroy!

!SLIDE

## Implicit return value
Ruby, as does Lisp and many functional languages, return implicitly the last expression of a body (block/method).
You can write an explicit return but that's considered to be non-idiomatic. So instead of:

	@@@ ruby
	  def add(x, y)
	    return x + y
	  end
instead write:

	@@@ ruby
	  def add(x, y)
	    x + y
	  end

!SLIDE

Multi-line array/hashes
There are many ways of writing multi-line array or hashes. This is recommended style:

	@@@ ruby
	array = [
	  1,
	  2,
	  3,
	]
Note that we insert a comma also after the last element. This is very handy because we have not to worry if we are in the last line or no (and you can reorder without further editing).

!SLIDE

The same idea applies for hashes or the combination of both:

	@@@ ruby
	data = {
	  :a => 1,
	  :b => {
	    :b1 => "11",
	    :b2 => "12",
	  },
	  :c => [
	    "hello",
	    "there",
	  ],
	}

!SLIDE
## Blocks
Single line blocks are written with brackets:

	@@@ ruby
	obj.method { |foo| ... }
Multi-line blocks are written with do/end:

	@@@ ruby
	obj.method do |foo|
	  ...
	  ...
	end

!SLIDE

OR-Equal Operator
||= will only assign if the left-hand side is nil

	@@@ ruby
	s = ""
	# ...
	s ||= "hello"   # -> ""

The following two lines are equivalent:

	@@@ ruby
	s ||= "hello"
	s = "hello" if s.nil?

!SLIDE small

## Attributes (Instance Variables)
- By default, object attributes can't be read or written to outside of the object
- You can change the access on attributes with `attr_reader`, `attr_writer` and `attr_accessor`
- These are class methods that open the named attributes up to reading, writing or read/write, resp.

Ever write a Java Bean? Here's Ruby's:

	@@@ ruby
	class RubyBean
	  attr_accessor :name, :date, :location
	end

!SLIDE

## The universal truth
In Ruby, everything except `nil` and `false` is considered true.

In C, Python and many other languages, 0 and possibly other values, such as empty lists, are considered false.

!SLIDE

##Optional Parameters
Parameters that, if not specified, take on some default value

	@@@ ruby
	def somemethod(x, y=nil)
	  return x * y unless y.nil?
	  x
	end

This prevents you from having to write multiple instances of the same method (DRY)
