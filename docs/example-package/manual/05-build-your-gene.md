# Build your Gene

Now that the gene's file structure looks like this:
```
gene-image/
├── metadata.json
├── index.json
└── contents/
    └── usr/
        └── bin/
            └── hello-world (+x)
```

**It's time to build the tarball!** Let's execute the following command:
```bash
tar cvf hello_world-1.0.0.tar gene-image
mv hello_world-1.0.0.tar hello_world-1.0.0.gene
gzip hello_world-1.0.0.gene
```

Now `hello_world-1.0.0.gene.gz` is ready to be distributed to a user or to a Gene Pool!

[Previous page: Setting up Hooks][prev_page] -- *this is where it all ends.* [Return to Introduction](./README.md)

[prev_page]: ./04-setting-up-hooks.md "Setting up Hooks"