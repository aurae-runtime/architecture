# Introduce Dependency on `libc`

This feature will accomplish **defining the standard way to interface with the kernel** because **having more than 1 system call library is a security and operational concern**.

### Outcomes

 - The `auraed` daemon will introduce the Rust libc 2.0 crate.
 - The project adopts libc over musl (or similar) for all system call interactions.

### Goals

 - All **projects within aurae that need to touch the kernel** will use **libc**.

### Decisions

 - The project will use **libc** and a subsequent dependence on the GNU license to solve **interfacing with a Linux kernel**.
     - Documentation on [libc](https://man7.org/linux/man-pages/man7/libc.7.html)

### Notes

 - As we slide into the slippery slope of the GNU ecosystem we need to be extremely cognizant of where GPL licenses will show up. This will impact our CLA.


### Authors

 - [@kris-nova](https://github.com/kris-nova)
