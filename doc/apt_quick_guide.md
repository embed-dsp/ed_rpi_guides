
# APT Quick Guide

Here is a summary of some usefull `apt` commands.

List all available packages.
```sh
sudo apt-cache pkgnames
```

Search for a specific package.
```sh
sudo apt-cache search <package-name>
```

Get information about a specific package.
```sh
sudo apt-cache show <package-name>
```

Get information about a dependencies of a specific package.
```sh
sudo apt-cache showpkg <package-name>
```

Resynchronize the package index files.
```sh
sudo apt-get update
```

Install the newest versions of all packages.
```sh
sudo apt-get upgrade
```

Install specific package.
```sh
sudo apt-get install <package-name>
```
