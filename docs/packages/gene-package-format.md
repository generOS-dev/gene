# Gene Package Format

This document defines the format of individual Genes (packages of the Gene Package Manager).

## On-Disk Format

### Versioning with SemVer

The VERSION property of a Gene MUST be a valid [SemVer string](https://semver.org/).

---

Genes are stored in files named `NAME_VERSION.gene`. For example, for package `foobar` version 1.0.0, the file name is `foobar_1.0.0.gene`. The name could also be `foobar_1.0.0.gene.gz` if GZip compression is enabled.

`.gene` files are actually another name for `.tar` files. The `.gene` file is a tarball of the Gene's contents. It is possible (and recommended) to compress genes with the file extension `.gene.gz`, using GZip, but this is not required. **`.gene` files MUST NOT be compressed without the `.gene.gz` extension.**

### Contents of the Gene Tarball

We will demonstrate the tarball contents by using a `hello-world` package with version `1.0.0`.

The tarball name would be `hello-world_1.0.0.gene`. The tarball contains the following files:

```
hello-world_1.0.0.gene
├── metadata.json
├── index.json
├── hooks
│   ├── preinstall
│   ├── postinstall
│   └── purge
└── contents
    └── usr
        └── bin
            └── hello-world
```

#### The `metadata.json` File

The `metadata.json` file contains the metadata (name, description, dependencies, provider-declarations, etc.) of this Gene.

Here's an example of the metadata:

```json
{
    "geneVersion": "1.0.0", // the version of the Gene format that this Gene is compatible with
    "name": "hello-world", // the name of the Gene
    "version": "1.0.0", // the version of the Gene
    "author": "Gene", // the author of the Gene
    "email": "gene@gene.gene", // Contact email for the author.
    "description": "A simple example of a Gene", // a short description of the Gene
    "longDescription": [
        "This is a longer description of the Gene",
        "It can be multiple lines"
    ],
    "dependencies": [
        [ "depends", "foo", "1.0.0" ], // This package requires foo 1.0.0 to function to a reasonable point. We cannot install without it.
        [ "recommends", "bar", "1.3.1-dev.1" ], // We strongly prefer bar 1.3.1 (dev.1) but we do not need it. More important than baz.
        [ "suggests", "baz", "1.0.0" ], // It would be useful if baz 1.0.0 was present.
        [ "enhances", "hello", "3.1.1" ] // A reverse of suggests, this package enhances hello 3.1.1's functions. (probably want to mark it as a dependency as well!)
    ],
    "conflicts": [ "goodbye" ] // Packages that should NEVER be installed with this package.
}
```

#### The `index.json` File

This file should note what files and binaries this package provides (it's all assembled by the repository).

```json
{
    "bin": [ // Binaries that are provided by this package.
        "hello-world"
    ],
    "lib": [], // Libraries, e.g. 'libfoo.so' provided.
    "include": [] // Headers, e.g. 'foo.h' provided.
}
```

#### The `hooks` Directory

Gene packages can contain hooks that are run before and after installation.

##### preinstall

This file runs before moving the files to their destination.

##### postinstall

Same as preinstall, but *after* the files are copied.

##### purge

Runs to delete configuration files made by the program. **Required.**

#### The `contents` Directory

This directory is applied onto `/` and contains the files and directories that are part of the Gene.

For example, with the structure above, a single binary is pushed into `/`. A user will be asked if there is any conflicts.