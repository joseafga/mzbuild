MZBUILD
==========
Build helper for BananaPKG.  
It automates several functions in creating a `.mz` package avoiding unnecessary repetition and making it easier to maintain the package in future updates.

*Read this in other languages: [English](README.md), [Português (BR)](README.pt-BR.md).*

Why?
----------
Inspired by projects such as *Makepkg*, *rpmbuild*, *SlackBuilds*, and others, combined with the desire to contribute to projects [BananaPKG](https://bananapkg.github.io/) and [Mazon OS](https://github.com/mazonos/) then came the project *mzbuild* project.

Building a package with BananaPKG is a simple task but I believe that automating repetitive tasks that need to be done with each new release or *build* (such as *download*, extraction, and fills) allows us to better focus on what It really matters.

Recipes
----------
As the `.spec`,` .PKGBUILD`, `.SlackBuild`, there is also a file with the recipe to follow, no specific extension is required but `.mzb.sh` is recommended. This make it explicit that it is a shell script as it also refers to **mzb**uild.

The file variables are very similar to BananaPKG's *desc* file and have very suggestive names which I believe needs no explanation.

The *checksum* to check *download* integrity can be done using either *md5* (`CHECKSUM_MD5`) or *sha256* (`CHECKSUM_SHA256`) just set the sum value in the referent variable. It is also possible not to use either *checksum* (not recommended) as well as both (it makes no sense).

The *array* `makedeps` is an additional package dependency which is only needed in *compile time*.

Finally we have the functions called at certain times in the process. Currently there is the `build ()` function called right after extraction which should be used for configuration and compilation of the application. While the `package ()` function is executed right after `build ()` and before packaging with BananaPKG, it should be used to install/copy files in `bindir` (variable containing the directory path corresponding to the package root).

Dependencies
----------
- bash
- coreutils
- cURL
- polkit
- tar

Installation
----------
**TODO:** Is intended to make a package for mzbuild, so it will be easily managed with BananaPKG but it is desired that the development is a bit more advanced.

You can test mzbuild in its current state with the following command:

    # curl -L 'https://raw.githubusercontent.com/joseafga/mzbuild/master/mzbuild' -o '/usr/bin/mzbuild' && chmod +x '/usr/bin/mzbuild'

> Make sure you know what you are doing

Usage
------
    mzbuild [options] <file.mzb.sh>

The available options are:

    --no-download     don't download
    --force-download  force download even if file exists
    -V, --version     display mzbuild version and exit

Options to install after creating the package and verbose are already in the plans other suggestions are welcome.

License
------
**MIT License**  
See [LICENSE](LICENSE) file.
