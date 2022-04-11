# Preparing the Files

For Gene to properly extract the `hello-world` executable, we need to create a version of the `/` filesystem to write on top of the real root filesystem.

`hello-world` has one binary file named `hello-world`, which should be in `$PATH`, so we will add it to `/usr/bin/hello-world`. First, create the `gene-image` folder with the subfolder named `contents`.

```bash
mkdir gene-image
mkdir gene-image/contents
```

Then, create the `/usr/bin` folder.

```bash
mkdir gene-image/contents/usr
mkdir gene-image/contents/usr/bin
```

> **Note:**
> This can all be done in one command by `mkdir -p gene-image/contents/usr/bin`.

Then, copy the `hello-world` binary file to `/usr/bin/hello-world`.

```bash
cp hello-world gene-image/contents/usr/bin/hello-world
```

Now the Gene image's contents have been assembled, let's move on to [writing the `metadata.json` file][next_page].

[Previous page: Writing a Hello World Program][previous_page] -- [Next page: Writing the `metadata.json` File][next_page]

[prev_page]: ./01-writing-a-hello-world-program.md "Writing a Hello World Program"
[next_page]: ./03-writing-the-metadata-file "Writing the metadata.json File"