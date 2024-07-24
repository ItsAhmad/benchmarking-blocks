## Introduction

This is a small challenge to learn more about how blocks work in Ruby. Blocks are actually very similiar to methods.

So let's think about methods for a second... You call a method with data - the method's arguments - from the outside world. The code inside the method can see and use this data to do it's job.

If arguments are how we pass in _data_ into methods, blocks are how we pass in _behavior_. Think of them as a chunk of logic that your method can run (aka: "call" or "yield").

In this case, we can think of a method as a robot that is responsible for doing one thing for us. When we ask it do that thing though, we give it parameters on how to do it, and sometimes we have to give it more than just data parameters, sometimes we have to give it specific instructions to give enough detail about how we want that task accomplished.

Look at `Enumerable#select` (which you'd normally call on an `Array`) or `#detect` methods which use blocks to get their job done. 

In Ruby, blocks can be passed into methods as a sort of "invisible argument", like this:

    def print_result
      result_from_block = yield
      puts result_from_block
    end
    
    # This will print out the number 9 to the console
    print_result { 3 * 3 }
    
    # Blocks can also be written using the do...end format
    print_result do
      creature = "walrus"
      "I am the #{creature}!"
    end
    
    # Very cool: blocks have access to variables outside of their definition!
    
    shopping_list = [:milk, :eggs, :cheese]
    print_result do
      important_item = shopping_list.sample # select one at random
      "I hope I don't forget #{important_item}!!!"
    end

As you will notice, the call to `yield` in the method definition is where the block is executed.

Let's write something practical using blocks. A common scenario is wanting to benchmark some code. The "skeleton" involved in benchmarking doesn't need to know what it's benchmarking, but it should be responsible for keeping track of how long it's running and other benchmarking-specific concerns.

That is, it shouldn't care whether we're benchmarking a simple function to add two numbers or something much more complicated.

Without blocks we might write code like this:
    
    start_time = Time.now
    
    # Calculate the 200th Fibonacci number
    fibonacci(200)
    
    end_time = Time.now
    
    # This will return the difference in the timestamps in seconds
    running_time = end_time - start_time
    
    puts "fibonacci(200) took #{running_time} seconds."

To make our benchmarking logic reusable, let's use blocks to create a benchmark method that can benchmark anything.

### Resources
1. [Blocks and Yield in Ruby](http://stackoverflow.com/questions/3066703/blocks-and-yields-in-ruby)
2. [The Building Blocks of Ruby](http://yehudakatz.com/2010/02/07/the-building-blocks-of-ruby/)

### Learning Goals
The goal of this challenge is to help you get better at understanding and using blocks. Feel free to play around and create toy versions of your code before you dive in.

* Writing methods that take a block parameter
* Returning values from blocks

### Objectives

**Implement the `benchmark` method** in the `benchmark_with_block.rb` file.

    # Be careful, pasting this into IRB/Pry will take a long time to print.
    # It's a loooong string. :)
    long_string = "apple" * 100000000
    
    running_time = benchmark { long_string.reverse }
    
    puts "string.reverse took #{running_time} seconds to run"
