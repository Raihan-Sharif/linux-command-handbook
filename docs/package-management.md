# Linux Package Management

Package managers in Linux handle the installation, updating, configuration, and removal of software. Different Linux distributions use different package management systems.

## APT (Advanced Package Tool) - Debian/Ubuntu

### Basic Commands

| Command | Description | Example |
|---------|-------------|---------|
| `apt update` | Update package lists | `sudo apt update` |
| `apt upgrade` | Upgrade installed packages | `sudo apt upgrade` |
| `apt install` | Install packages | `sudo apt install git` |
| `apt remove` | Remove packages | `sudo apt remove git` |
| `apt purge` | Remove packages and configurations | `sudo apt purge git` |
| `apt search` | Search for packages | `apt search python` |
| `apt show` | Show package details | `apt show nginx` |
| `apt list --installed` | List installed packages | `apt list --installed` |
| `apt autoremove` | Remove unused dependencies | `sudo apt autoremove` |

### Advanced Usage

```bash
# Install multiple packages
sudo apt install git nginx python3 -y

# Install specific version
sudo apt install nginx=1.18.0-0ubuntu1

# Update only security packages
sudo apt upgrade -s
```

## DNF/YUM - Red Hat/Fedora/CentOS

### Basic Commands

| Command | Description | Example |
|---------|-------------|---------|
| `dnf check-update` | Check for updates | `sudo dnf check-update` |
| `dnf upgrade` | Upgrade packages | `sudo dnf upgrade` |
| `dnf install` | Install packages | `sudo dnf install git` |
| `dnf remove` | Remove packages | `sudo dnf remove git` |
| `dnf search` | Search for packages | `dnf search python` |
| `dnf info` | Show package info | `dnf info nginx` |
| `dnf list installed` | List installed packages | `dnf list installed` |
| `dnf autoremove` | Remove unused dependencies | `sudo dnf autoremove` |

### Advanced Usage

```bash
# Install from a specific repository
sudo dnf --enablerepo=epel install htop

# Install local RPM package
sudo dnf localinstall package.rpm

# Group install
sudo dnf group install "Development Tools"
```

## Pacman - Arch Linux

### Basic Commands

| Command | Description | Example |
|---------|-------------|---------|
| `pacman -Syu` | Synchronize and upgrade | `sudo pacman -Syu` |
| `pacman -S` | Install packages | `sudo pacman -S git` |
| `pacman -R` | Remove packages | `sudo pacman -R git` |
| `pacman -Rs` | Remove package and dependencies | `sudo pacman -Rs git` |
| `pacman -Ss` | Search for packages | `pacman -Ss python` |
| `pacman -Si` | Show package info | `pacman -Si nginx` |
| `pacman -Q` | List installed packages | `pacman -Q` |
| `pacman -Sc` | Clean package cache | `sudo pacman -Sc` |

### Advanced Usage

```bash
# Reinstall a package
sudo pacman -S --needed git

# Remove package and config files
sudo pacman -Rns package

# Update only AUR packages (using yay)
yay -Sua
```

## Zypper - openSUSE

### Basic Commands

| Command | Description | Example |
|---------|-------------|---------|
| `zypper refresh` | Update repositories | `sudo zypper refresh` |
| `zypper update` | Update packages | `sudo zypper update` |
| `zypper install` | Install packages | `sudo zypper install git` |
| `zypper remove` | Remove packages | `sudo zypper remove git` |
| `zypper search` | Search for packages | `zypper search python` |
| `zypper info` | Show package info | `zypper info nginx` |
| `zypper se --installed-only` | List installed packages | `zypper se --installed-only` |
| `zypper clean` | Clean package cache | `sudo zypper clean` |

## Snap and Flatpak

### Snap

```bash
# Install snap
sudo snap install package

# Find snaps
snap find keyword

# List installed snaps
snap list

# Remove snap
sudo snap remove package

# Update all snaps
sudo snap refresh
```

### Flatpak

```bash
# Install flatpak
flatpak install flathub com.application.Name

# List installed flatpaks
flatpak list

# Remove flatpak
flatpak uninstall com.application.Name

# Update all flatpaks
flatpak update
```

## Troubleshooting

### Fixing Broken Packages (APT)

```bash
# Fix broken installs
sudo apt --fix-broken install

# Reconfigure packages
sudo dpkg --configure -a

# Force reinstall
sudo apt install --reinstall package
```

### Package Lock Issues

```bash
# For APT when dpkg is locked
sudo rm /var/lib/dpkg/lock-frontend
sudo rm /var/lib/apt/lists/lock
sudo dpkg --configure -a

# For YUM/DNF
sudo rm /var/run/yum.pid
```

### Managing Repository Keys

```bash
# Add a repository key (APT)
curl -fsSL https://key-server.example/key.gpg | sudo apt-key add -

# List repository keys
sudo apt-key list

# Remove repository key
sudo apt-key del "key_id"
```

## Best Practices

1. **Regular Updates**: Run system updates regularly for security patches.
2. **Clean Unused Packages**: Remove unused packages to free disk space.
3. **Backup Before Major Upgrades**: Always backup your system before distribution upgrades.
4. **Use Official Repositories**: Prioritize official repositories for stability and security.
5. **Check Dependencies**: Be aware of what will be installed/removed when managing packages.
6. **Keep Package Cache Clean**: Periodically clean old package caches.

## Additional Resources

- [Debian Package Management Documentation](https://www.debian.org/doc/manuals/debian-reference/ch02.en.html)
- [Fedora DNF Documentation](https://docs.fedoraproject.org/en-US/fedora/latest/system-administrators-guide/package-management/DNF/)
- [Arch Linux Pacman Guide](https://wiki.archlinux.org/title/pacman)
- [openSUSE Zypper Guide](https://en.opensuse.org/SDB:Zypper_usage)
