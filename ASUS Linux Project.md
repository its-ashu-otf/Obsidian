#### Nouveau prevents boot

Boot with nouveau disabled: use `nouveau.modset=0` on the [kernel command line](https://wiki.archlinux.org/title/Kernel_command_line "Kernel command line"). Need to edit bumblebee service to boot : [https://github.com/Bumblebee-Project/Bumblebee/issues/764#issuecomment-450749984](https://github.com/Bumblebee-Project/Bumblebee/issues/764#issuecomment-450749984).

ASUS Linux is a suite of tools designed to improve the performance and functionality of ASUS laptops when running Linux. It comes in 2 main parts, [asusctl](https://wiki.archlinux.org/title/Asusctl "Asusctl") and [supergfxctl](https://wiki.archlinux.org/title/Supergfxctl "Supergfxctl"), the former interacts with the `asus-wmi` kernel module to control BIOS level features and the latter is used to control the dedicated GPU in dual GPU systems.

The project is maintained by [Luke Jones](https://gitlab.com/flukejones) and is hosted on [GitLab](https://gitlab.com/asus-linux).

## Software

ASUS Linux provides many packages, please see subsections below.

**Note:**

- There is also a custom repository which contains prebuilt binaries available: [Unofficial user repositories#g14](https://wiki.archlinux.org/title/Unofficial_user_repositories#g14 "Unofficial user repositories"), provided by [Luke Jones](https://gitlab.com/flukejones).
- This repository is the officially recommended way of installing the asus-linux utilities by the asus-linux developers, it was created and is being maintained by them. See: [https://asus-linux.org/guides/arch-guide/](https://asus-linux.org/guides/arch-guide/)
- While the project uses the G14 moniker this **does not** mean it only works with ASUS G14 models, in actuality it supports almost all ASUS ROG & TUF laptops.

### asusctl

[asusctl](https://aur.archlinux.org/packages/asusctl/)AUR is a CLI utility for ASUS ROG & TUF laptop, to name some of the important features it gives users control over:

- Integrated GPU MUX Control
- Keyboard RGB Lighting Profile (but limited compared to the Windows AURA/Armoury Crate)
- Fan Curves
- Battery Charge Limit
- Panel Overdrive
- AniMe Matrix Screens

For usage instructions see [asusctl](https://wiki.archlinux.org/title/Asusctl "Asusctl").

### supergfxctl

[supergfxctl](https://aur.archlinux.org/packages/supergfxctl/)AUR is a CLI utility for managing GPU switching functionality on ASUS hybrid laptops, particularly dedicated GPU MUX control.

For usage instructions see [supergfxctl](https://wiki.archlinux.org/title/Supergfxctl "Supergfxctl").

### rog-control-center

[rog-control-center](https://aur.archlinux.org/packages/rog-control-center/)AUR is a GUI frontend for _asusctl_ and _supergfxctl_.

### Custom kernel

The ASUS Linux project maintains a set of kernel patches specific to ASUS mobile devices and packages them into a kernel. Typically using this kernel is not required however in some edge cases (usually for very recent laptops) all your laptop features might not function without it.

[Install](https://wiki.archlinux.org/title/Install "Install") [linux-g14](https://aur.archlinux.org/packages/linux-g14/)AUR and [linux-g14-headers](https://aur.archlinux.org/packages/linux-g14-headers/)AUR.

**Note:**

- If you added the [G14 unofficial repository](https://wiki.archlinux.org/title/Unofficial_user_repositories#g14 "Unofficial user repositories"), you can install the AUR packages above directly through [pacman](https://wiki.archlinux.org/title/Pacman "Pacman").
- If you are switching from a stock kernel to a custom kernel you must also update any kernel modules to their [DKMS](https://wiki.archlinux.org/title/DKMS "DKMS") variants.

## See also

- Project homepage - [https://asus-linux.org/](https://asus-linux.org/)
- Project GitLab page - [https://gitlab.com/asus-linux](https://gitlab.com/asus-linux)


#### Republic of Gamers (ROG)

| [Model version](https://wiki.archlinux.org/title/Template:Laptops_table_header#Model_version "Template:Laptops table header") | [Date](https://wiki.archlinux.org/title/Template:Laptops_table_header#Date "Template:Laptops table header") | [Video](https://wiki.archlinux.org/title/Template:Laptops_table_header#Video "Template:Laptops table header") | [Sound](https://wiki.archlinux.org/title/Template:Laptops_table_header#Sound "Template:Laptops table header") | [Ethernet](https://wiki.archlinux.org/title/Template:Laptops_table_header#Ethernet "Template:Laptops table header") | [Wireless](https://wiki.archlinux.org/title/Template:Laptops_table_header#Wireless "Template:Laptops table header") | [Bluetooth](https://wiki.archlinux.org/title/Template:Laptops_table_header#Bluetooth "Template:Laptops table header") | [Power management](https://wiki.archlinux.org/title/Template:Laptops_table_header#Power_management "Template:Laptops table header") | [Other](https://wiki.archlinux.org/title/Template:Laptops_table_header#Other "Template:Laptops table header")                                  | [Remarks](https://wiki.archlinux.org/title/Template:Laptops_table_header#Remarks "Template:Laptops table header") |
| ----------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------- |
|                                                                                                                               |                                                                                                             |                                                                                                               |                                                                                                               |                                                                                                                     |                                                                                                                     |                                                                                                                       |                                                                                                                                     |                                                                                                                                                |                                                                                                                   |
|                                                                                                                               |                                                                                                             |                                                                                                               |                                                                                                               |                                                                                                                     |                                                                                                                     |                                                                                                                       |                                                                                                                                     |                                                                                                                                                |                                                                                                                   |
| ROG Strix G16 2023 (G614JI)                                                                                                   | 2024-05-01                                                                                                  | Yes                                                                                                           | Yes                                                                                                           | Yes                                                                                                                 | Yes                                                                                                                 | Untested                                                                                                              | Yes                                                                                                                                 | - nvidia driver version 550.78+ is required for suspend to work<br>- Set `acpi_backlight=native` for proper display brightness control on dGPU |                                                                                                                   |
### GNOME extension

[gnome-shell-extension-battery-health-charging-git](https://aur.archlinux.org/packages/gnome-shell-extension-battery-health-charging-git/)AUR is a [GNOME extension](https://wiki.archlinux.org/title/GNOME#Extensions "GNOME") that "_provides a graphical user interface for setting a laptop’s charging limit (charging threshold) within a Gnome environment_". It supports [ASUS laptops](https://maniacx.github.io/Battery-Health-Charging/device-compatibility/asus) and many other brands. See its [official website](https://maniacx.github.io/Battery-Health-Charging/) for details and screenshots.