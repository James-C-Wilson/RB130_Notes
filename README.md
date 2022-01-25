# BLOCKS

# **BLOCKS**

## **What are closures?**

1. `Closures` are a general computer science concept signifying a “chunk of code” that can be saved and passed around; this concept exists among many different computer programming languages.  They can be executed at a later time, even from a different location in the code structure.  When created, the `closure` works by binding its `surrounding artifacts`, which can include objects, methods, variables, and other pieces of code and data.  

```ruby
# **CODE EXAMPLES FOR EACH**
```

## **What is binding?**

1. `Binding` is the context, or surrounding environment for a `closure`.  When a closure is instantiated or created, it creates an `enclosure` around its surrounding artifacts that are within its scope, enabling the closure to retain access to them when the closure is executed.  Thus, closures can use and update local variables that are in scope when they are executed.  Additionally, the call for execution can come from a place in the code structure where these variables are not in scope.

```ruby
# **CODE EXAMPLES FOR EACH**
```

## **Variable Scope and Binding**

1. For local variables, blocks create a new scope (this pertains to local variables solely).  Local variables initialized in outer scope is available to a block.  However, a local variable initialized in inner scope is not available in outer scope.
2. Binding is the mechanism in which closures use to keep track of the local variables that are available to them.  Since the `binding` consists of the context or surrounding environment for a closure, this can include method calls/references, constants, local variables, basically any other kind of artifact within scope.  The closure is said to “bind” itself to the artifacts and “drag” them around as needed.
3. Example
    1. 
    
    ```ruby
    def introduce_yourself(introduction)
      introduction.call
    end
    
    me = "James"
    
    my_proc = Proc.new { puts "Hello, my name is #{me}."}
    
    introduce_yourself(my_proc)
    #=> Hello, my name is James.
    
    ```
    
    Above CODE DESCRIPTION
    

## What Are Blocks?

1. In Ruby, `blocks` are sections of code that are surrounded by `{...}` or `do...end`.  Blocks are passed as arguments to the method that invokes them. All methods can accept `implicit blocks`.  However, only those methods that implement their execution with a call to `yield` will execute the code inside the given block.  Depending upon how the method that takes the block is implemented determines how the return value of the block is used.  The method could end up not using the block at all.

```ruby
# CODE EXAMPLES
```

## **Writing Methods that take Blocks**

1. In order to define a method that takes a `block`, we must invoke the Ruby `keyword yield`.  `Yield` executes any `block` that gets passed to the method as an argument.  This allows the method invoker to add their section of code into the method that was defined.

```ruby
# Code EXAMPLE
```

b. If a method is defined with `yield`, but no block is passed to the method, a `LocalJumpError` will be raised. 

```ruby
CODE EXAMPLE
```

 c. In order to add additional flexibility to the `method implementation`, a conditional can be used with the `Kernel#block_given?` method.  `Kernel#block_given?` will return `true` if a `block`is passed to method, and `false` if not.  

```ruby
# CODE EXAMPLE
```

## **Passing Execution to a Block**

`Yield` `passes execution` to the `block`.  `Execution` moves to where the `block` is `defined`  — the `closure`— and executes the code inside.  Next, execution will continue back to where it was when `yield` was `invoked`, and continue execution of the method that was passed the `block`.

Method implementation and method execution are not the same.  Method implementation is the defining of the method.  This is where execution occurs when we call the method initially.  The invocation of the method is the actual calling of the method.  

`Blocks` allow us additional flexibility in programming.  The method implementer, the person defining the method, may not necessarily know how the invoker of the method will use it.  By providing the option (or necessity depending upon the method) for blocks, however, the person invoking the method can refine some of the method implementation without having to change the previous implementation steps of the method in question.

CODE EXAMPLE

## **Yielding with an Argument**

At times, when passing a block into a method, the block may require an argument.  This can be achieved chiefly in two ways: one at method implementation and one at method invocation.

1. Method implementation: Adding an argument to the `yield` statement, ie. `yield(argument_to_pass)`
2. Method invocation: Defining the block with a `block parameter`, ie { |block_parameter| # code goes here }
    
     a. The block parameter, also known as a `block local variable` is a special type of local variable; its scope is confined to the block itself.  It is essential that the block parameter has a unique name, because if it conflicts with other local variables outside the block; this is known as variable shadowing.  
    
    ### When to use:
    
    1. Blocks allow additional flexibility in the use of methods, particularly blocks that take an argument.  A method implementor (the person that created the method) may not know exactly how the invoker of the method will use it.  The use of blocks allows the invoker to specify this specific behavior on a value within the method once the method is invoked.
    2. A good example of deferring the specific use of a method is the `Array#each` method.  
    
    ```ruby
    # CODE EXAMPLE
    ```
    
    ```ruby
    # CODE EXAMPLE
    ```
    
    ## **Return Value of a Block**
    
    Similar to methods, that last evaluated expression in the `block` is the block’s return value.  That last evaluated expression will be implicitly returned by the block.  This returned value can saved and used when execution returns to the method implementation that yielded to the block.
    
    The return value of a block can be saved by assigning it to a local variable inside the method.  This value can later be referenced and evaluated or manipulated.
    
    ```ruby
    #CODE EXAMPLE
    ```
    
    Return values can also be used in conditionals.  
    
    ```ruby
    #CODE EXAMPLE
    
    ```
    
    Similar to how methods should either return a value, or perform a specific action (output a value, mutate a value), the same applies to blocks as well.  
    
    ```ruby
    #CODE EXAMPLE
    ```
    

## **Use Cases for Blocks**

### **Defer Implementation**

1. Oftentimes, when writing a method, the implementer may not know exactly how the invoker of the method will use it during invocation.  This is a perfect situation of using `blocks` to account for this uncertainty.  By using blocks, the implementer can defer the specific implementation until the invocation of the method.  An example of this is the `each` method.  The implementer of the `Array#each` method defined the method in a general, ambiguous way.  This was so that the person invoking the method could provide details about a specific condition that they wanted to occur during execution. As an example, Instead of making `Array#each_odd` , or `Array#each_number_divisible_by_2` Ruby has a general `Array#each` method that allows the invoker to be specific about what they want to occur during execution via the use of a `block`. 

### **Sandwich Code**

The concept of `sandwich code` refers to methods that need to implement some “before” and “after” action.  

This could include logging something (**what is logging**), some sort of notification system or timing a specific process.  (REVISE)  Additionally, it includes interfacing with the operating system, or resource management. For example, when working with files, first we need to allocate memory to open said file.  Then, once we finish a specific task on the file, we need to close the file and clean up the memory allocation.  Placing a block in between these two steps—sandwiching—allows one to automate the set up and clean up process.

```ruby
#CODE EXAMPLE HERE
```

## Explicit Block Parameters

Every method in Ruby can take an `implicit block`.  An `implicit block` is a block that is passed to a method invocation as an argument, without being named explicitly or assigned to a parameter once its passed into the method; implicit blocks are “anonymous”.  The only way to execute the block is through the invocation of the Ruby keyword `yield`, passing along any arguments that it requires.  Additionally, we can save the resulting return value of the block, but not the `block` itself.

However, one can assign an `explicit block` to a parameter.  The `block` that is assigned to a `parameter`, the explicit block, is treated as a `named object`.  Thus it can be referenced, passed around, invoked multiple times, reassigned, and manipulated in a manner that an `implicit block` cannot.  This is achieved by `converting the block argument into a Proc`.

### To Convert A Block Into A Proc

First, we add a parameter with an arbitrary name prepended with unary `&` to the list of parameters in the method definition.  Note: this has to be the last parameter in the method definition. 

This saves the block that is passed to the method as a `Proc` object.  Since the `block` is now a `Proc` object, it can be passed around or referenced via the use of the parameter.

In order to reference the `Proc` inside the method, we call the parameter (variable) without the unary `&`.

When we wish to execute it, we call the `Proc#call` method on the parameter (variable)

```ruby
# CODE EXAMPLE hi
```

Since we have a way to reference the `Proc` object we could pass it to other methods.

```ruby
# CODE EXAMPLE
```

```ruby
# Additional Example
```

In summation, in order to do utilize a block in one’s method—other than just executing it with `yield`-- it is necessary to utilize `Procs`. A `Proc` is created by invoking a method with an `explicit block parameter` (`&parameter_name)`.  Now the `block` has been converted into a `Proc object` that can be referenced and passed around the code structure.  Since the only place that `blocks` exist is in method calls, there really is no other way to convert a `block` to a `Proc`.

## Symbol to Proc

By passing a `block` to a method as an explicit parameter, we can create a `Proc` out of a `block` .  

```ruby
# Remake an Example
def take_a_guess(range, &my_guess)
  guess = range.to_a.sample
  if my_guess.call(guess) # test truthiness with Proc
    puts "Yay! My guess #{guess} was correct!"
  else
    puts "Aw, my guess #{guess} was incorrect."
  end
end

# pass a block as argument to be converted to Proc
take_a_guess(1..10) { |g| g == 5}
# => Yay! My guess 5 was correct!  (results may vary)
```

We can also do the reverse of this.   By passing a `Proc` argument with the unary `&` to a method that expects a block we can effectively convert `Proc` into a block.

Consequently, we can do the inverse of the above example.  If we pass a `Proc` argument with the unary `&` to a method that expects a block, we can effectively convert `Proc` into a block.

 

```ruby
def take_multiple_guesses(range, &my_number)
  guess = []
  3.times { guesses << range.to_a.sample}

  # recall that we currently have the Proc my_number
  # but the any? method expects a block
  # convert the Proc to a block by passing as argument with &
  if guesses.any?(&my_number)
    puts "#{guesses} includes your number!"
  else
  puts "Aw, #{guesses} does not include your number."
  end
end
```

- When `&` is in a method definition:
    - It’s being used to describe an explicit block parameter
    - It expects to take a block
    - It will return a converted `Proc` from the block
- When `&` is in a method invocation:
    - It’s being used to help pass a `Proc` (or Symbol) as an argument to a method that expects a block
    - It expects to take a `Proc`
    - Will return a block that was converted from the given `Proc`
    

If `&` is expecting a `Proc` and it doesn’t receive one, it will automatically attempt to convert the object into a `Proc`.  It does this by calling `to_proc` on the object that it received. 

If the aforementioned object does not have a `to_proc` method and can’t be converted, an error will be raised.  Interestingly, this implies a very useful shortcut that can be used with symbols.

When `unary &` is paired with a symbol, Ruby takes the method that this symbol represents, and creates a `Proc` that calls the method on the object that gets passed to it.  Thus, this `Proc` can be converted to a block by `unary &` .

```ruby
# CODE EXAMPLE
```

We can pass symbols with the `unary &` into methods that expect blocks.  The block needs to be very simple, however.  Additionally, the methods cannot require an argument.

5, When do we use blocks? (List the two reasons)

1. Blocks are used when we want to defer implementation of a method
2. Also, when we wish to sandwich some code.  An example would be if we want to time some sort of execution before yielding to a block, and then after yielding to the block

```ruby
# **CREATE TWO CODE EXAMPLES FOR
 # EACH**
```

```ruby
# **CREATE TWO CODE EXAMPLES FOR
 # EACH**
```

## f

At times, when passing a block into a method, the block may require an argument.  This can be achieved chiefly in two ways

6, Describe the two reasons we use blocks, use examples.

7, When can you pass a block to a method? Why?

1. All `methods` can take an `implicit` block.  Thus, you can technically always pass a block to a method, though depending on the method’s implementation, it could ignore the block.

8, How do we make a block argument mandatory?

1. In order to make a block argument mandatory, we can have the method implementation invoke the `Proc#call` method on the `explicit block parameter` in the method definition, without the `&`.  When the block is passed to the method, the `&` converts the `block` to a `simple Proc object`.  
2. Additionally we could use the Ruby `keyword yield` within the implementation of the method.  The `yield` keyword requires that it yield to and execute a block.  If there is no block, a `LocalJumpError no block given` error will be raised.

9, How do methods access both implicit and explicit blocks passed in?

1. All methods take implicit blocks. Explicit blocks are passed in and soncerted via & in the parameter name.

10, What is `yield` in Ruby and how does it work?

11, How do we check if a block is passed into a method?

12, Why is it important to know that methods and blocks can return closures?

13, What are the benifits of explicit blocks?

14, Describe the arity differences of blocks, procs, methods and lambdas.

15, What other differences are there between lambdas and procs? (might not be assessed on this, but good to know)

16, What does `&` do when in a the method parameter?

`def method(&var); end`

17, What does `&` do when in a method invocation argument?

`method(&var)`

18, What is happening in the code below?

`arr = [1, 2, 3, 4, 5]

p arr.map(&:to_s) # specifically `&:to_s``

19, How do we get the desired output without altering the method or the method invocations?

`def call_this
  yield(2)
end

# your code here

p call_this(&to_s) # => returns 2
p call_this(&to_i) # => returns "2"`

20, How do we invoke an explicit block passed into a method using `&`? Provide example.

21, What concept does the following code demonstrate?

`def time_it
  time_before = Time.now
  yield
  time_after= Time.now
  puts "It took #{time_after - time_before} seconds."
end`

22, What will be outputted from the method invocation `block_method('turtle')` below? Why does/doesn't it raise an error?

`def block_method(animal)
  yield(animal)
end

block_method('turtle') do |turtle, seal|
  puts "This is a #{turtle} and a #{seal}."
end`

23, What will be outputted if we add the follow code to the code above? Why?

`block_method('turtle') { puts "This is a #{animal}."}`

24, What will the method call `call_me` output? Why?

`def call_me(some_code)
  some_code.call
end

name = "Robert"
chunk_of_code = Proc.new {puts "hi #{name}"}
name = "Griffin"

call_me(chunk_of_code)`

25, What happens when we change the code as such:

`def call_me(some_code)
  some_code.call
end

chunk_of_code = Proc.new {puts "hi #{name}"}
name = "Griffin"

call_me(chunk_of_code)`

26, What will the method call `call_me` output? Why?

`def call_me(some_code)
  some_code.call
end

name = "Robert"

def name
  "Joe"
end

chunk_of_code = Proc.new {puts "hi #{name}"}

call_me(chunk_of_code)`

27, Why does the following raise an error?

`def a_method(pro)
  pro.call
end

a = 'friend'
a_method(&a)`

28, Why does the following code raise an error?

`def some_method(block)
  block_given?
end

bl = { puts "hi" }

p some_method(bl)`

29, Why does the following code output `false`?

`def some_method(block)
  block_given?
end

bloc = proc { puts "hi" }

p some_method(bloc)`

30, How do we fix the following code so the output is `true`? Explain

`def some_method(block)
  block_given? # we want this to return `true`
end

bloc = proc { puts "hi" } # do not alter this code

p some_method(bloc)`

31, How does `Kernel#block_given?` work?

32, Why do we get a `LocalJumpError` when executing the below code? & How do we fix it so the output is `hi`? (2 possible ways)

`def some(block)
  yield
end

bloc = proc { p "hi" } # do not alter

some(bloc)`

33, What does the following code tell us about lambda's? (probably not assessed on this but good to know)

`bloc = lambda { p "hi" }

bloc.class # => Proc
bloc.lambda? # => true

new_lam = Lambda.new { p "hi, lambda!" } # => NameError: uninitialized constant Lambda`

34, What does the following code tell us about explicitly returning from proc's and lambda's? (once again probably not assessed on this, but good to know ;)

`def lambda_return
  puts "Before lambda call."
  lambda {return}.call
  puts "After lambda call."
end

def proc_return
  puts "Before proc call."
  proc {return}.call
  puts "After proc call."
end

lambda_return #=> "Before lambda call."
              #=> "After lambda call."

proc_return #=> "Before proc call."`

35, What will `#p` output below? Why is this the case and what is this code demonstrating?

`def retained_array
  arr = []
  Proc.new do |el|
    arr << el
    arr
  end
end

arr = retained_array
arr.call('one')
arr.call('two')
p arr.call('three')`

# **TESTING WITH MINITEST**

36, What is a test suite?

37, What is a test?

38, What is an assertion?

39, What do testing framworks provide?

40, What are the differences of Minitest vs RSpec

41, What is Domain Specific Language (DSL)?

42, What is the difference of assertion vs refutation methods?

43, How does assert_equal compare its arguments?

44, What is the SEAT approach and what are its benefits?

45, When does setup and tear down happen when testing?

46, What is code coverage?

47, What is regression testing?

# **CORE TOOLS**

48, What are the purposes of core tools?

49, What are RubyGems and why are they useful?

50, What are Version Managers and why are they useful?

51, What is Bundler and why is it useful?

52, What is Rake and why is it useful?

53, What constitutes a Ruby project?
