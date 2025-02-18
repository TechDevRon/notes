
The sudo command, by default, allows you to run a program with root privileges. Under some conditions, system administrators may need to give regular users some flexibility on their privileges. For example, a junior SOC analyst may need to use Nmap regularly but would not be cleared for full root access. In this situation, the system administrator can allow this user to only run Nmap with root privileges while keeping its regular privilege level throughout the rest of the system.

You can check what is available with "sudo -l"

[https://gtfobins.github.io/](https://gtfobins.github.io/) is a valuable source that provides information on how any program, on which you may have sudo rights, can be used.

**Leverage application functions**

Some applications will not have a known exploit within this context. Such an application you may see is the Apache2 server.

In this case, we can use a "hack" to leak information leveraging a function of the application. As you can see below, Apache2 has an option that supports loading alternative configuration files (`-f` : specify an alternate ServerConfigFile).

![](https://i.imgur.com/rNpbbL8.png)

**Leverage LD_PRELOAD**
On some systems, you may see the LD_PRELOAD environment option.
![](https://i.imgur.com/gGstS69.png)
LD_PRELOAD is a function that allows any program to use shared libraries. This [blog post](https://rafalcieslak.wordpress.com/2013/04/02/dynamic-linker-tricks-using-ld_preload-to-cheat-inject-features-and-investigate-programs/) will give you an idea about the capabilities of LD_PRELOAD. If the "env_keep" option is enabled we can generate a shared library which will be loaded and executed before the program is run. Please note the LD_PRELOAD option will be ignored if the real user ID is different from the effective user ID.

We can save this code as shell.c and compile it using gcc into a shared object file using the following parameters;

`gcc -fPIC -shared -o shell.so shell.c -nostartfiles`

![](https://i.imgur.com/HxbszMW.png)


**unistd.h**

If unisted.h isn't used when using setgid(0), setuid(0) you will get this error.
![[Pasted image 20250218124022.png]]
To fix this just include the unistd.h header at the top of the file.

The `unistd.h` header file in C and C++ provides access to the POSIX operating system API. It declares various functions, constants, and types that allow programs to interact with the underlying operating system. It is part of the Single UNIX Specification and should be available in any POSIX-compliant system.

