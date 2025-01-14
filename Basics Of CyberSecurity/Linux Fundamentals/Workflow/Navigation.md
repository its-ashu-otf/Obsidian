Navigation is essential, like working with the mouse as a standard Windows user. With it, we move across the system and work in directories and with files, we need and want. Therefore, we use different commands and tools to print out information about a directory or a file and can use advanced options to optimize the output to our needs.

Let us start with the navigation. Before we move through the system, we have to find out in which directory we are. We can find out where we are with the command `pwd`.

```powershell
ashu@htb[~]$ pwd

/home/ashu
```

Only the `ls` command is needed to list all the contents inside a directory. It has many additional options that can complement the display of the content in the current folder.

```powershell
ashu@htb[~]$ ls

Desktop  Documents  Downloads  Music  Pictures  Public  Templates  Videos
```

Using it without any additional options will display the directories and files only. However, we can also add the `-l` option to display more information on those directories and files.

```powershell
ashu@htb[~]$ ls -l

total 32
drwxr-xr-x 2 ashu htbacademy 4096 Nov 13 17:37 Desktop
drwxr-xr-x 2 ashu htbacademy 4096 Nov 13 17:34 Documents
drwxr-xr-x 3 ashu htbacademy 4096 Nov 15 03:26 Downloads
drwxr-xr-x 2 ashu htbacademy 4096 Nov 13 17:34 Music
drwxr-xr-x 2 ashu htbacademy 4096 Nov 13 17:34 Pictures
drwxr-xr-x 2 ashu htbacademy 4096 Nov 13 17:34 Public
drwxr-xr-x 2 ashu htbacademy 4096 Nov 13 17:34 Templates
drwxr-xr-x 2 ashu htbacademy 4096 Nov 13 17:34 Videos
```

