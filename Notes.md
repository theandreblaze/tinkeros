#A freestanding Rust binary




Reduction of the complexity involved in creating applications is one of the many reasons for the popularity of modern programming environments. However; this reduction can also hide interesting parts of the application lifecycle - sometimes because of language abstractions for implementing inheritance, polymorphism and code reuse, and at other times, beacause of less-visible interactions between the compiler/interpreter and the operating system which manages access to the APIs for system calls and error handling.



In this freestanding binary, a few key dependencies are exposed and replaced - in the process explaining basic interaction between  running code and the OS.

-1 Inner attributes:  #![no_std], #![no_main]
    source: https://doc.rust-lang.org/reference/attributes.html
    These are attributes which annotate the item that they are within (such as a function, a module, the start of a block or the last block inside a nested code block), indicating a compile-time condition. In this example, these inner attributes unlink the standard library, and unset the dependency on a 'main' function as an entry-way to the program respectively.

- 2 Custom handlers and diverging functions: panic(_info: &PanicInfo) ->!{...}

