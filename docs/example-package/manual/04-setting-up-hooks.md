# Setting up Hooks

Gene uses a structure of "hooks" to allow you to customize the behavior of Gene when your genes are installed, removed, upgraded, or purged.

Let's write a simple postinstall hook that tells Gene to execute hello-world after installing it.

Make the folder `gene-image/hooks` and create a file named `postinstall` with the following contents:

```bash
#!/bin/bash
hello-world
```

After this is done, make sure the `postinstall` file is executable.

```bash
chmod +x gene-image/hooks/postinstall
```

Did you notice anything? We used Bash in the `postinstall` hook, meaning we **now have a dependency!**

Let's add it to the `metadata.json` file:
```json
{
    // ...
    "dependencies": [
        ["bash", "5"]
    ],
    // ...
}
```

This now means `bash` version `5.x.x` is now installed when we pull this Gene in.

Now that the hook writing is complete, let's [build the Gene][next_page]!

[Previous page: Writing the `metadata.json` File][prev_page] -- [Next page: Build your Gene][next_page]

[prev_page]: ./03-writing-the-metadata-file.md "Writing the metadata.json File"
[next_page]: ./05-build-your-gene.md "Build your Gene"