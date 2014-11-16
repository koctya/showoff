!SLIDE subsection



# Resources #
!SLIDE small

# Resources #

- [Ruby language](https://www.ruby-lang.org/en/)
- [Ruby Documentation and Tutorials](https://www.ruby-lang.org/en/documentation/)
- [Programming Ruby by Dave Thomas](https://pragprog.com/book/ruby4/programming-ruby-1-9-2-0)
- [Ruby gems](http://rubygems.org)
- [JRuby](http://jruby.org)
- [From Java to Ruby](http://www.paulklipp.com/articles/from-java-to-ruby-book-summary.pdf)

!SLIDE

It is useful to know, however, that a number of pre-defined global variables are available to you as a Ruby developer to obtain information about the Ruby environment. A brief summary of each of these variables is contained in the following table.

Variable Name	Variable Value
$@	 The location of latest error
$_	 The string last read by gets
$.	 The line number last read by interpreter
$&	 The string last matched by regexp
$~	 The last regexp match, as an array of subexpressions
$n	 The nth subexpression in the last match (same as $~[n])
$=	 The case-insensitivity flag
$/	 The input record separator
$\	 The output record separator
$0	 The name of the ruby script file currently executing
$*	 The command line arguments used to invoke the script
$$	 The Ruby interpreter's process ID
$?	 The exit status of last executed child process