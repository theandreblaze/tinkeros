# A freestanding Rust binary


Reduction of the complexity involved in creating applications is one of the many reasons for the popularity of modern programming environments. However; this reduction can also hide interesting parts of the application lifecycle - sometimes because of language abstractions for implementing inheritance, polymorphism and code reuse, and at other times, beacause of less-visible interactions between the compiler/interpreter and the operating system which manages access to the APIs for system calls and error handling.



In this freestanding binary, a few key dependencies are exposed and replaced - in the process explaining basic interaction between code being executed, and the OS.

- 1 Inner attributes:  #![no_std], #![no_main]
    source: https://doc.rust-lang.org/reference/attributes.html
    
    These are attributes which annotate the item that they are within (such as a module), indicating a compile-time condition. In this example, these inner attributes unlink the standard library, and unset the dependency on a 'main' function as an entry-way to the program respectively.

- 2 Custom handlers & diverging functions: panic(_info: &PanicInfo) ->!{...}
    source: https://doc.rust-lang.org/rust-by-example/fn/diverging.html

    The custom panic handler is a requirement in this binary because the usual flow of logic when an operating system is available to a program, is to hand errors off to it to choose the appropriate signal for the exception, alert and/or logging process for that error. 
    
    This is actually a good thing because programmers can simply return errors when a condition is unmet, for instance, that the operating system can associate with relevant processes without having the program share in that knowledge. The Rust PanicInfo parameter holds two values: the name of the module being executed, and the line where the panic happened.



- 2.1 Diverging functions are a pattern which handles functions that are never expected to return.
    source: https://docs.rust-lang.org/rust-by-example/fn/diverging.html
   

    Within main.rs, the panic handler is a diverging function because it isnt expected to return, rather like the main loop of the code on a network device such as a server.

    The LLVM manual describes exceptions as events that rarely occur within the normal scope of operation of a program, and seen in that light, diverging functions allow the freestanding binary, which has no OS support, to handle errors as they occur, without terminating the program itself (source: https://llvm.org/docs/ExceptionHandling.html). 
    The diverging function is compatible with all types, and can be used as a wrapper around errors whose values are unknown or indeterminate.




# A minimal Rust Kernel.

A kernel is the interface between the hardware components and the software applications on a computer, and acts as an authority for memory, allocating resources via system calls and residing in a bespoke memory space on the computer. It is the kernel's responsibility to assign the order of execution of programs on the computer and it differs from the bootloader (BIOS, GRUB or UEFI), which are stored in special flash memory on the motherboard) and/or the OS.







