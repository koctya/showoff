!SLIDE small

## To Ruby From Java
	- Java is mature. It’s tested. And it’s fast
	(contrary to what the anti-Java crowd may claim).

	- It’s also quite verbose. Going from Java to Ruby,
	expect your code size to shrink down considerably.

	- You can also expect it to take less time to knock
	together quick prototypes.

!SLIDE small

## Similarities
As with Java, in Ruby,…

- Memory is managed for you via a garbage collector.
- Objects are strongly typed.
- There are public, private, and protected methods.
- There are embedded doc tools (Ruby’s is called RDoc).
The docs generated by rdoc look very similar to those generated by javadoc.

!SLIDE small

## Differences
Unlike Java, in Ruby,…

- You don’t need to compile your code. You just run it directly.
- There are several different popular third-party GUI toolkits. Ruby users can try WxRuby, FXRuby, Ruby-GNOME2, Qt, or the bundled-in Ruby Tk for example.
- You use the `end` keyword after defining things like classes, instead of having to put braces around blocks of code.
- You have `require` instead of `import`.

!SLIDE small

- All member variables are private. From the outside, you access everything via methods.
- Parentheses in method calls are usually optional and often omitted.
- Everything is an object, including numbers like `2` and `3.14159`.
- There’s no static type checking.

!SLIDE small

- Variable names are just labels. They don’t have a type associated with them.
- There are no type declarations. You just assign to new variable names as-needed and they just “spring up”
	(i.e. `a = [1,2,3]` rather than `int[] a = {1,2,3};`).
- There’s no casting. Just call the methods. Your unit tests should tell you before you even run the code if you’re going to see an exception.
- It’s `foo = Foo.new("hi")` instead of `Foo foo = new Foo("hi")`.

!SLIDE small

- The constructor is always named `initialize` instead of the name of the class.
- You have “mixins” instead of interfaces.
- YAML tends to be favored over XML.
- It’s `nil` instead of `null`.

!SLIDE small

- `==` and `equals()` are handled differently in Ruby.
Use `==` when you want to test equivalence in Ruby (equals() is Java).
Use `equal?()` when you want to know if two objects are the same (`==` in Java).

!SLIDE small

Java users need IDEs

- Eclipse
- NetBeans
- Jetbrains

Ruby Users

- [TextMate](http://macromates.com)
- [Sublime Text 2](http://www.sublimetext.com/2)
- VIM
- Bash or ZSH