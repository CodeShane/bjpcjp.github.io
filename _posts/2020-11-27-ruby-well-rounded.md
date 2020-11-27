---
title: Well-Rounded Ruby - book notes
layout: post
date: 2020-11-27
tags: ruby
---

![book-cover](/px/ruby/book-cover.png)

* Book notes from "The Well Rounded Rubyist" (Black, Leo, 3rd ed), compiled into Jupyter Notebook pages. Each chapter link points to a corresponding GitHub repo. Built using Ruby 2.7.

### Contents:
1. [Bootstrapping](https://github.com/bjpcjp/well-grounded-rubyist-book-notes/blob/master/ch01-bootstrap.ipynb)
    - installation, syntax, Ruby basics
    - Ruby anatomy
    - Ruby extensions & libraries
    - Ruby standard tools
        - ruby, irb, rdoc, ri, rake, gem, erb   
    
2. [Objects, Methods, Local Variables](https://github.com/bjpcjp/well-grounded-rubyist-book-notes/blob/master/ch02-objs-meths-locals.ipynb)
    - talking to objects
    - creating an object
    - innate object behaviors
    - method arguments
    - local variables & assignments
    
3. [Classes](https://github.com/bjpcjp/well-grounded-rubyist-book-notes/blob/master/ch03-classes.ipynb)
    - classes & instances
    - instance variables & object state
    - setter methods
    - attributes
    - inheritance
    - classes as objects & message receivers
    - constants
    - nature vs nurture
    
4. [Modules](https://github.com/bjpcjp/well-grounded-rubyist-book-notes/blob/master/ch04-modules.ipynb)
    - intro
    - modules, classes & method lookup
    - method_missing
    - class & module design/naming
    
5. [Self](https://github.com/bjpcjp/well-grounded-rubyist-book-notes/blob/master/ch05-self.ipynb)
    - intro
    - scope
    - method-access rules
    - top-level methods
    
6. [Control Flow Techniques](https://github.com/bjpcjp/well-grounded-rubyist-book-notes/blob/master/ch06-control-flow.ipynb)
    - conditional execution
    - loops
    - iterators & code blocks
    - error handling & exceptions
    
7. [Essential Classes & Modules](https://github.com/bjpcjp/well-grounded-rubyist-book-notes/blob/master/ch07-essentials.ipynb)
    - literal constructors
    - syntactic sugar
    - bang methods and danger
    - conversion methods
    - boolean states & objects ... and nil
    - comparing two objects
    - inspecting object capabilities
    
8. [Strings, Symbols, other Scalars](https://github.com/bjpcjp/well-grounded-rubyist-book-notes/blob/master/ch08-scalars.ipynb)
    - string basics
    - symbols
    - numbers
    - times & dates
    
9. [Collections & Containers](https://github.com/bjpcjp/well-grounded-rubyist-book-notes/blob/master/ch09-collections-containers.ipynb)
    - arrays & hashes
    - collection handling with arrays
    - hashes
    - ranges
    - sets
    
10. [Enumerables](https://github.com/bjpcjp/well-grounded-rubyist-book-notes/blob/master/ch10-enumerables.ipynb)
    - each
    - boolean queries
    - searches & indexes
    - element-wise ops
    - additional ops
    - map, aka collect
    - strings as enumerables (sorta)
    - sorting
    - enumerators
    - enumerator semantics & use cases
    - method chaining
    - lazy enumerators
    
11. [Regular Expressions](https://github.com/bjpcjp/well-grounded-rubyist-book-notes/blob/master/ch11-regexes.ipynb)
    - intro
    - writing
    - building a pattern
    - matching, substrings, MatchData
    - quantifiers, anchors, modifiers
    - string <=> regex conversions
    - common use cases
    
12. [File I/O Operations (TODO)](https://github.com/bjpcjp/well-grounded-rubyist-book-notes/blob/master/ch12-file-io.ipynb)
    - IO class
    - basic file ops
    - IO and File queries
    - directories
    - file tools
    
13. [Object Individualization](https://github.com/bjpcjp/well-grounded-rubyist-book-notes/blob/master/ch13-object-individualization.ipynb)
    - singletons
    - modifying core classes & modules
    - BasicObject
    
14. [Callables & Runnables](https://github.com/bjpcjp/well-grounded-rubyist-book-notes/blob/master/ch14-callables-runtimes.ipynb)
    - procs
    - lambdas and ->
    - methods as objects
    - eval family of methods
    - threads
    - system commands from inside Ruby
    
15. [Callbacks, Hooks, Runtime Introspection (TODO)](https://github.com/bjpcjp/well-grounded-rubyist-book-notes/blob/master/ch15-callbacks-hooks-introspection.ipynb)
    - callbacks & hooks
    - interpreting object capability queries
    - introspection: variables & constants
    - tracing execution
    - callbacks & method inspection in practice 
    
16. [Functional Programming](https://github.com/bjpcjp/well-grounded-rubyist-book-notes/blob/master/ch16-functional-programming.ipynb)
    - pure functions
    - immutability
    - higher-order functions
    - recursion