# Gene Repo Format

Gene Repositories, more commonly referred to as "gene pools," are responsible for the storage and indexing of many Genes.

Gene Pools are **only** accessible over **HTTPS** with SSL. Gene should always error when using a non-secured pool.

Gene mounts it's paths on `/gene`. You don't need to use a subdomain for the repo, but it is suggested.

## File Structure

Gene pools take on the following file structure:

```
/gene/
├── /TIMESTAMP
├── /index.json
└── /files/
    ├── /g/
    │   ├── index.json
    │   └── /gene/
    │       ├── index.json
    │       ├── gene_1.0.0.gene
    │       └── gene_1.0.0.gene.gpg
    └── /h/
        ├── index.json
        └── /hello-world/
            ├── index.json
            ├── hello-world_1.0.0.gene
            ├── hello-world_1.0.0.gene.gpg
            ├── hello-world_1.0.1.gene
            └── hello-world_1.0.1.gene.gpg
```

### The `TIMESTAMP` File

This file is a timestamp of the last time the pool was updated. You don't need to re-pull the pool if you don't want to.

### The `index.json` File

This is the big one. It contains references to every package and version contained in this repository.

```json
{
    "gene": ["1.0.0"],
    "hello-world": ["1.0.0", "1.0.1"]
}
```

### The `files/` Directory

This directory contains one directory for each first character in the gene. The first character is the first letter of the gene's name.

Inside each, is the index.json for that folder, similar to that above. It contains the gene folder for each package.

#### The `files/X/XXX/` Directory

This is where the individual genes are stored.

##### The `index.json` File

This file contains one property which refers to the latest release of the Gene.

```json
{ "latest": "1.0.1" }
```

##### The `NAME_VERSION.gene` File

This is the [Gene package](../packages/gene-package-format.md) of the Gene.

##### The optional `NAME_VERSION.gene.gpg` File

This is the [GPG signature](https://www.gnupg.org/gph/en/manual/gpg-signing.html) of the Gene. This is strongly recommended to be signed with a trusted key, to ensure security of packages.