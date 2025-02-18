
### What is LD_PRELOAD?

`LD_PRELOAD` is a special environment variable in Linux that lets you load a shared library (a piece of code) before any other libraries when a program starts. This allows you to override or "hijack" functions in the program, even if you don’t have access to its source code.

### The Example: Changing Random Numbers

1. **Original Program**: Imagine you have a simple program (`random_num`) that prints 10 random numbers between 0 and 99. It uses the `rand()` function from the standard C library to generate these numbers.
    
2. **Creating a Fake `rand()` Function**: Now, let’s say you want to change how `rand()` works without modifying the original program. You can create your own version of `rand()` in a new file (`unrandom.c`) that always returns the number 42.
    
3. **Compile the Fake Function**: You compile this fake `rand()` into a shared library (`unrandom.so`).
    
4. **Use `LD_PRELOAD` to Override `rand()`**: When you run the original program, you tell the system to load your fake `rand()` function instead of the real one by setting `LD_PRELOAD` to point to your shared library. Now, when the program calls `rand()`, it uses your version, and it always returns 42.
5. 
6. `LD_PRELOAD=./unrandom.so ./random_num`
### How Does This Work?

When a program runs, it loads libraries (like the standard C library) to use functions like `rand()`. Normally, it uses the `rand()` from the standard library. But if you use `LD_PRELOAD`, your custom library gets loaded first, and your version of `rand()` is used instead.

### A More Advanced Example: Spying on File Access

You can also use `LD_PRELOAD` to spy on what a program is doing. For example, you can override the `open()` function (which is used to open files) to print the name of every file the program tries to access.

1. **Create a Fake `open()` Function**: You write a custom `open()` function that prints the file name and then calls the real `open()` function to actually open the file.
    
2. **Compile the Fake `open()`**: You compile this into a shared library (`inspect_open.so`).
    
3. **Use `LD_PRELOAD` to Override `open()`**: When you run a program (like a calculator), your custom `open()` function will print every file the program tries to access.
    
``LD_PRELOAD=./inspect_open.so gnome-calculator``
    
	Now, every time the calculator tries to open a file, you’ll see the file name printed in the terminal.
    

### Why Is This Useful?

- **Debugging**: You can use this to see what files or functions a program is using, which can help you understand how it works or why it’s crashing.
    
- **Hacking**: You can change the behavior of a program without modifying its source code. For example, you could make a game always think you have the highest score.
    
- **Security**: You can use this to monitor or restrict what a program can do, like preventing it from accessing certain files.
    

### Important Notes

- This trick only works on Linux (and some other Unix-like systems).
    
- You need to be careful because overriding functions can break programs if not done correctly.
    
- Some programs are designed to resist this kind of tampering, so it won’t always work.
    

In short, `LD_PRELOAD` is a powerful tool that lets you change or monitor how programs behave, even if you don’t have their source code. It’s like having a magic wand that lets you tweak programs from the outside!