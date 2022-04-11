# Writing a Hello World Program

Let's write a simple Hello, World! program in C.

## Writing the C code
Here's how you would write a simple program in C that prints just "Hello, World!" to the screen.

```c
#include <stdio.h>

int main() {
    printf("Hello, World!\n");
    return 0;
}
```

Let's take this C code and write it to the file `hello-world.c`.

```bash
cat > hello-world.c << EOF
#include <stdio.h>

int main() {
    printf("Hello, World!\n");
    return 0;
}
EOF
```

## Compiling this C code into an executable

Let's build this code using gcc:

```bash
gcc -o hello-world hello-world.c
```

Once you build this code, you can run it:

```bash
./hello-world
```

You should get the output of `Hello, World!` printed to the screen. If this doesn't happen, check your source code.

Now we have this hello-world file, let's move on to [preparing the files](./02-preparing-the-files.md).

[Previous page: Intro to Gene Packaging][prev_page] -- [Next page: Preparing the Files][next_page]

[prev_page]: ./00-intro-to-gene-packaging.md "Intro to Gene Packaging"
[next_page]: ./02-preparing-the-files.md "Preparing the Files"