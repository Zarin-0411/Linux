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
![image](https://github.com/user-attachments/assets/8592ab03-fe31-4d0e-ab64-8fb52a2c3151)

![image](https://github.com/user-attachments/assets/950dece1-12f5-4037-994d-a529ac36f20e)

Once installed, verify by running:

```gcc --version```

![image](https://github.com/user-attachments/assets/1f7abdce-88f0-4301-b34d-2e4b8228c229)

Since we already have installed gcc compiler we do not need to install the compiler again. 


### B. Make a small C program "mycalc.c" to ask user 2 numbers, and print the sum

1. For ease of use I created a directory called calculator and I am going to use this folder to write my c program. 


2. Create mycalc.c using nano editor.

3. Inorder to check our env & other setting, first try to run Hello world app,

    - Update the file 
    - Save the file (Ctrl + s)
    - Exit from nano editor (Ctrl + x)

![image](https://github.com/user-attachments/assets/a8ffd8d9-52bd-4692-9252-ea5d4684475a)


4. Compile the file and make mycalc program. 

``` gcc mycalc.c -o mycalc```

5. Now Run the app and check if its working with no issues. 

![image](https://github.com/user-attachments/assets/9a6369b5-8700-47af-9dfc-8d8522017b61)


6. Now we can modify to add our calculator codes.

Updating mycalc.c to Perform Addition

Open mycalc.c 

        nano mycalc.c

Modify the code to:
```bash
#include <stdio.h>

int main() {
    int num1, num2, sum;
    printf("Enter two numbers: ");
    scanf("%d %d", &num1, &num2);
    sum = num1 + num2;
    printf("Sum: %d\n", sum);
    return 0;
}
```

Save (Ctrl + S) and exit (Ctrl + X).

![image](https://github.com/user-attachments/assets/d24774a9-3e78-4afa-a39d-fb808d5a3073)


Recompile:

        gcc mycalc.c -o mycalc

Run the updated program:

        ./mycalc

![image](https://github.com/user-attachments/assets/583f44b0-a4b3-4d84-b76e-320423f5cf54)

