# Programming With C language


### A. Install the GCC Compiler

Most Linux distributions has GCC (GNU Compiler Collection) pre-installed. To check if GCC is installed, run:

```gcc --version```

If it's not installed, install it using:

Ubuntu/Debian:

```
sudo apt update
sudo apt install gcc
```

Once installed, verify by running:

```gcc --version```

Since we already have installed gcc compiler we do not need to install the compiler again. 


### B. Make a small C program "mycalc.c" to ask user 2 numbers, and print the sum

1. For ease of use I created a directory called calculator and I am going to use this folder to write my c program. 


2. Create mycalc.c using nano editor.

3. Inorder to check our env & other setting, first try to run Hello world app,

    - Update the file 
    - Save the file (Ctrl + s)
    - Exit from nano editor (Ctrl + x)


4. Compile the file and make mycalc program. (-o mycalc : Output will be mycalc)

``` gcc mycalc.c -o mycalc```

5. Now Run the app and check if its working with no issues. 


6. Now we can modify to add our calculator codes. 