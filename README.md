# Description

pathaudit is a small python utility which allows one to *hash*, using the SHA-256 cryptographic hash function, a user provided path (i.e. if the path refers to a valid file, then that file will be hashed; if the path refers to a directory then that directory tree will be recursively traversed and all the files within the tree will be hashed).

If an output file is specified during the hash operation, it may later be used as an input for an *audit* (checking whether the files in the audit file have changed since the audit file creation).

## Usage

```
$ ./pathaudit.py -h
usage: pathaudit.py [-h] {hash,audit} ...

positional arguments:
  {hash,audit}
    hash        Hash the supplied path
    audit       Audit mode

optional arguments:
  -h, --help    show this help message and exit
```

### Usage Example in Hash Mode

Hash the "README.md" file and write the output to stdout.

```
$ ./pathaudit.py hash README.md
README.md is a file
Hashing....
/home/ambrozie/temp/pathaudit/README.md: f623cc0ba00460252cdbffc357d07524b0a1113a87a84cb6a99a0075638b3677
```

Hash the "test" directory (this will actually process recursively the "test" directory and hash all the containing files) and write the output to the "out" file.

```
$ ./pathaudit.py hash test -o out
test is a directory
Recursively hashing...
Finished writing output to the 'out' file
```

### Usage Example in Audit Mode

Take an audit file (actually a file that's been specified as an output file during a previously issued hash mode operation and whose structure consists of lines of the form \<filepath\>:\<filehash\>) and check its consistency (meaning check the files in the audit file for changes).

```
$ ./pathaudit.py audit out
Auditing...
/home/ambrozie/temp/pathaudit/README.md: success
```