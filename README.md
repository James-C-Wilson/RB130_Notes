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
