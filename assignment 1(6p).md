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

### Install Node.js and npm

```bash
sudo apt-get install nodejs npm
```
### Set up Express web server
- To create a new directory:
```bash
mkdir myserver && cd myserver
```
- Initialize npm:
```bash
npm init -y
```
- to install Express:
```bash
npm install express
```
![image](https://github.com/user-attachments/assets/84b5dfd3-587f-4cce-9f3a-2a593a5ed32d)

### Create myserver.js and add the following code:
```bash
const express = require('express');
const app = express();
const port = 3000;

app.get('/', (req, res) => {
    res.send('Hello World!');
});

app.get('/user', (req, res) => {
    res.json({
        user: process.env.USER || 'unknown',
        home: process.env.HOME || 'unknown'
    });
});

app.listen(port, () => {
    console.log(`Server running at http://localhost:${port}/`);
});
```
- To run the server:
```bash
node myserver.js
```
![image](https://github.com/user-attachments/assets/1d82fa27-6a60-4bdf-92cd-14b7f5e95e31)

### Install Python3 and pip
```bash
sudo apt-get update
```
![image](https://github.com/user-attachments/assets/0cb78754-f0e3-47d5-b1d9-c08ab994c631)

```bash
sudo apt-get install python3 python3-pip
```

![image](https://github.com/user-attachments/assets/32f994d0-f472-4cf5-99ac-1842060caaea)

```bash
 pip install bpytop
```
![image](https://github.com/user-attachments/assets/197ad345-67a4-4bfb-a966-c0748cdb5fea)

