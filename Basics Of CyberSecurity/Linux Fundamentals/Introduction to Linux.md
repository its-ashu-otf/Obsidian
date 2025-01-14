![[Pasted image 20240705024539.jpg]]

## History 
The history of Linux begins with the release of Unix in 1970 by Ken Thompson and Dennis Ritchie at AT&T. Later, the Berkeley Software Distribution (BSD) emerged in 1977, but legal issues with AT&T limited its development. In 1983, Richard Stallman launched the GNU project to create a free Unix-like operating system, leading to the creation of the GNU General Public License (GPL). However, no free, widely adopted kernel existed until Linus Torvalds developed the Linux kernel in 1991 as a personal project.

The Linux kernel has since grown significantly, with over 23 million lines of source code, and is licensed under the GPL v2. Today, Linux powers over 600 distributions, including popular ones like Ubuntu, Debian, Fedora, and Red Hat. It is widely recognized for its security, stability, performance, and frequent updates, though it can be challenging for beginners and has fewer hardware drivers than Windows.

Linux’s open-source nature allows anyone to modify and distribute it for various purposes. It is used in servers, desktops, embedded systems, and even Android, making it the most widely installed OS globally. 

## Philosophy
| **Principle**                                                 | **Description**                                                                                                                                                   |
| ------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `Everything is a file`                                        | All configuration files for services and components in Linux are stored as one or more text files, making management and modification straightforward.            |
| `Small, single-purpose programs`                              | Linux provides a variety of tools, each designed for a specific purpose. These can be combined for flexibility and efficiency.                                    |
| `Ability to chain programs together to perform complex tasks` | Tools can be integrated to perform large and intricate tasks, such as filtering or processing specific data.                                                      |
| `Avoid captive user interfaces`                               | Linux emphasizes using the shell (or terminal), granting users powerful control and flexibility over the operating system.                                        |
| `Configuration data stored in a text file`                    | Key configuration data, like the `/etc/passwd` file (which stores registered system users), is stored in editable text files for ease of access and modification. |

## Components
| **Component**     | **Description**                                                                                                                                                    |
| ----------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `Bootloader`      | The code that initiates the booting process to load the operating system. For example, Parrot Linux uses the GRUB Bootloader.                                      |
| `OS Kernel`       | The core of the operating system, responsible for managing hardware resources and handling input/output at the hardware level.                                     |
| `Daemons`         | Background services, called daemons, ensure essential functions like scheduling, printing, and multimedia operate correctly. They start during or after booting.   |
| `OS Shell`        | The shell is the command-line interface between the user and the operating system, allowing users to execute commands. Popular shells include Bash, Zsh, and Fish. |
| `Graphics server` | The graphical subsystem, often referred to as "X" or "X-server," enables graphical applications to run on the system, locally or remotely.                         |
| `Window Manager`  | The graphical user interface (GUI) includes options like GNOME, KDE, or MATE. It provides tools like file managers and browsers to access system features.         |
| `Utilities`       | These are programs designed for specific tasks, helping users or other programs perform essential functions.                                                       |

## Linux Architecture

