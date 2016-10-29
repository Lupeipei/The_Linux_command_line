# Package management

Most of the top-tier Linux distributions release new versions every six months and many individual program updates every day.

### Packaging Systems
Most distributions fall into one of two camps of packaging technologies:
- the Debian “.deb” camp
- the Red Hat “.rpm” camp

Major packaging system families:

| Packaging System | Distributions (Partial Listing)|
| ---------------- | ------------------------------ |
| Debian Style (.deb) | Debian, Ubuntu, Linux Mint, Raspbian |
| Red Hat Style (.rpm) | Fedora, CentOS, Red Hat Enterprise Linux, OpenSUSE |

### How A Package System Works

- Virtually all software for a Linux system will be found on the Internet.

- Most of it will be provided by the distribution vendor in the form of package files and the rest will be available in source code form that can be installed manually.

#### Package Files

- The basic unit of software in a packaging system is the package file.

- Package files are created by a person known as a package maintainer.

- The package maintainer gets the software in source code form from the upstream provider (the author of the program), compiles it, and creates the package metadata and any necessary installation scripts.

#### Repositories

- Packages are made available to the users of a distribution in central repositories that may contain many thousands of packages, each specially built and maintained for the distribution.

- A distribution may maintain several different repositories for different stages of the software development life cycle.

- A distribution may also have related third-party repositories.

#### Dependencies

- Programs are seldom “standalone”; rather they rely on the presence of other software components to get their work done.

- Common activities, such as input/output for example, are handled by routines shared by many programs.

- These routines are stored in what are called *shared libraries*, which provide essential services to more than one program.

- If a package requires a shared resource such as a shared library, it is said to have a dependency.

#### High And Low-level Package Tools

Package management systems usually consist of two types of tools:

- Low-level tools which handle tasks such as installing and removing package files;

- High-level tools that perform metadata searching and dependency resolution.

Packaging system tools:

| Distributions | Low-level tools | High-level tools |
| ------------- | --------------- | ---------------- |
| Debian-Style | dpkg | apt-get, aptitude |
| Fedora, Red Hat Enterprise Linux, CentOS | rpm | yum |

### Common Package Management Tasks

#### Finding A Package In A Repository

| Style | Commands |
| ----- | -------- |
| Debian | apt-get update; apt-cache search search_string |
| Red Hat | yum search search_string |

Example(s):

```
yum search emacs
apt-cache search emacs
```

#### Installing A Package From A Repository

| Style | Commands |
| ----- | -------- |
| Debian | apt-get update; apt-get install package_name |
| Red Hat | yum install package_name |

Example(s):

```
apt-get update; apt-get install emacs
```

```
yum install emacs
```

#### Installing A Package From A Package File

If a package file has been downloaded from a source other than a repository, it can be installed directly (though without dependency resolution) using a low-level tool.

| Style | Commands |
| ----- | -------- |
| Debian | dpkg --install package_file |
| Red Hat | rpm -i package_file |

Example(s):

```
yum install emacs-22.1-7.fc7-i386.rpm
```

#### Removing A Package

| Style | Commands |
| ----- | -------- |
| Debian | apt-get remove package_name |
| Red Hat | yum erase package_name |

Example:

```
apt-get remove emacs
```

#### Updating Packages From A Repository


The most common package management task is keeping the system up-to-date with the latest versions of packages.

| Style | Commands |
| ----- | -------- |
| Debian | apt-get update; apt-get upgrade |
| Red Hat | yum update |

Example:

```
apt-get update; apt-get upgrade
```

#### Upgrading A Package From A Package File

If an updated version of a package has been downloaded from a non-repository source, it can be installed, replacing the previous version:

| Style | Commands |
| ----- | -------- |
| Debian | dpkg --install package_file |
| Red Hat | rpm -U package_file |

Example:

```
rpm -U emacs-22.1-7.fc7-i386.rpm
```

Note :

`dpkg` does not have a specific option for upgrading a package versus installing one as `rpm` does.

#### Listing Installed Packages

| Style | Commands |
| ----- | -------- |
| Debian | dpkg --list |
| Red Hat | rpm -qa |

#### Determining If A Package Is Installed

| Style | Commands |
| ----- | -------- |
| Debian | dpkg --status package_name |
| Red Hat | rpm -q package_name |

Example:

```
dpkg --status emacs
```

#### Displaying Info About An Installed Package

| Style | Commands |
| ----- | -------- |
| Debian | apt-cache show package_name |
| Red Hat | rpm info package_name |

Example:

```
apt-cache show emacs
```

#### Finding Which Package Installed A File

| Style | Commands |
| ----- | -------- |
| Debian | dpkg --search file_name |
| Red Hat | rpm -qf file_name |

Example:

```
rpm -qf /usr/bin/vim
```
