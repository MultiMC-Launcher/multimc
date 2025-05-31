---
title: "Configuration Guide - MultiMC Launcher"
description: "Complete configuration guide for MultiMC offline Minecraft launcher. Optimize performance, manage instances, and customize settings."
keywords: "multimc configuration, minecraft launcher settings, multimc optimization, java settings multimc"
layout: page
---

# Configuration Guide

## ⚙️ Initial Setup

### First Launch Configuration
After installing MultiMC, optimize these essential settings:

1. **Launch MultiMC** for the first time
2. **Open Settings** (gear icon or File → Settings)
3. **Configure core settings** following this guide
4. **Test configuration** with a new instance

---

## ☕ Java Configuration

### Automatic Java Detection
MultiMC automatically detects Java installations:

1. **Settings** → **Java**
2. **Auto-detect** button scans for Java versions
3. **Select appropriate version** for your needs:
   - **Java 8**: Minecraft 1.7.10-1.16.x
   - **Java 17**: Minecraft 1.17.x-1.19.x
   - **Java 21**: Minecraft 1.20.x+ (recommended)

### Manual Java Configuration
For custom Java installations:

```bash
# Windows example paths
C:\Program Files\Java\jdk-17\bin\javaw.exe
C:\Program Files\Eclipse Adoptium\jdk-17.0.5.8-hotspot\bin\javaw.exe

# Linux example paths
/usr/lib/jvm/java-17-openjdk/bin/java
/opt/java/jdk-17/bin/java

# macOS example paths
/Library/Java/JavaVirtualMachines/jdk-17.jdk/Contents/Home/bin/java
/usr/libexec/java_home -v 17
```

### Memory Allocation
Optimize RAM usage for best performance:

#### Recommended Settings by System RAM:
- **8GB System RAM**: 3-4GB for Minecraft
- **16GB System RAM**: 6-8GB for Minecraft
- **32GB+ System RAM**: 8-12GB for Minecraft

#### Configuration Steps:
1. **Settings** → **Java**
2. **Minimum memory allocation**: 1024 MB
3. **Maximum memory allocation**: Based on system RAM
4. **PermGen**: 256 MB (Java 8 only)

### JVM Arguments Optimization
Advanced performance tuning:

#### For Modern Java (17+):
```bash
-XX:+UseG1GC
-XX:+UnlockExperimentalVMOptions
-XX:MaxGCPauseMillis=100
-XX:+DisableExplicitGC
-XX:TargetSurvivorRatio=90
-XX:G1NewSizePercent=50
-XX:G1MaxNewSizePercent=80
-XX:G1MixedGCLiveThresholdPercent=35
-XX:+AlwaysPreTouch
-XX:+ParallelRefProcEnabled
-Dusing.aikars.flags=https://mcflags.emc.gs
-Daikars.new.flags=true
```

#### For Java 8:
```bash
-XX:+UseG1GC
-XX:+UnlockExperimentalVMOptions
-XX:MaxGCPauseMillis=100
-XX:+DisableExplicitGC
-XX:TargetSurvivorRatio=90
-XX:G1NewSizePercent=50
-XX:G1MaxNewSizePercent=80
-XX:InitiatingHeapOccupancyPercent=10
-XX:G1MixedGCLiveThresholdPercent=35
-XX:+AlwaysPreTouch
-XX:+ParallelRefProcEnabled
```

---

## 📁 Instance Management

### Instance Storage Configuration
Optimize where Minecraft instances are stored:

#### Default Locations:
- **Windows**: `%APPDATA%\.minecraft\instances`
- **macOS**: `~/Library/Application Support/minecraft/instances`
- **Linux**: `~/.local/share/multimc/instances`

#### Custom Instance Folder:
1. **Settings** → **MultiMC**
2. **Instance Folder**: Browse to desired location
3. **Considerations**:
   - Use SSD for faster loading
   - Ensure sufficient space (2GB+ per instance)
   - Avoid cloud-synced folders

### Central Mod Storage
Enable shared mod libraries:

1. **Settings** → **MultiMC**
2. **✓ Use shared mod folder**
3. **Central Mods Folder**: Choose location
4. **Benefits**:
   - Saves disk space
   - Faster mod installation
   - Easier mod management

### Instance Groups
Organize instances efficiently:

1. **Right-click** in instance list
2. **Create Group** → Name your group
3. **Drag instances** into groups
4. **Suggested groups**:
   - Vanilla Versions
   - Modded Survival
   - Creative/Testing
   - Educational/Learning

---

## 🌐 Network Settings

### Offline Mode Configuration
For air-gapped systems:

1. **Settings** → **Network**
2. **✓ Work offline**
3. **Disable update checking**
4. **Configure proxy** if needed

### Proxy Configuration
For corporate/restricted networks:

#### HTTP Proxy:
```
Type: HTTP
Host: proxy.company.com
Port: 8080
Username: [if required]
Password: [if required]
```

#### SOCKS Proxy:
```
Type: SOCKS5
Host: 127.0.0.1
Port: 1080
```

### Download Settings
Optimize download performance:

1. **Concurrent downloads**: 6 (default)
2. **Download timeout**: 30 seconds
3. **Retry attempts**: 3
4. **Use system proxy**: Enable if needed

---

## 🎮 Game-Specific Settings

### Minecraft Window Configuration
Optimize game window settings:

1. **Edit Instance** → **Settings** → **Minecraft**
2. **Window size**: 
   - **Maximized**: Best for most users
   - **Custom**: 1920x1080 for specific needs
3. **✓ Start Minecraft maximized**

### Game Directory Structure
Understand instance organization:

```
instances/
├── MyInstance/
│   ├── minecraft/
│   │   ├── saves/          # World saves
│   │   ├── resourcepacks/  # Texture packs
│   │   ├── screenshots/    # Screenshots
│   │   └── logs/          # Game logs
│   ├── mods/              # Mod files
│   └── .minecraft/        # Instance config
```

### Performance Optimization
In-game settings for better performance:

#### Video Settings:
- **Graphics**: Fast
- **Render Distance**: 8-12 chunks
- **Smooth Lighting**: Off
- **VSync**: Off
- **Max Framerate**: Unlimited

#### Advanced Settings:
- **Use VBOs**: On
- **Threaded Optimization**: On
- **Anisotropic Filtering**: Off
- **Antialiasing**: Off

---

## 🔧 Advanced Configuration

### Custom Launch Wrapper
For advanced users:

1. **Edit Instance** → **Settings** → **Custom Commands**
2. **Pre-launch command**:
   ```bash
   # Windows
   echo "Starting Minecraft..." > launch.log
   
   # Linux/macOS
   echo "Starting Minecraft..." >> launch.log
   ```

3. **Post-exit command**:
   ```bash
   # Cleanup or logging
   echo "Minecraft closed at $(date)" >> launch.log
   ```

### Environment Variables
Set custom environment variables:

```bash
# Performance tweaks
JAVA_OPTS="-Djava.awt.headless=true"
MC_OPTS="-Dfml.ignoreInvalidMinecraftCertificates=true"

# Debug options
DEBUG_MODE=true
VERBOSE_LOGGING=true
```

### Config File Locations
Direct configuration file editing:

#### MultiMC Settings:
- **Windows**: `%APPDATA%\MultiMC\multimc.cfg`
- **macOS**: `~/Library/Application Support/MultiMC/multimc.cfg`
- **Linux**: `~/.local/share/multimc/multimc.cfg`

#### Instance Settings:
```
instances/[instance_name]/instance.cfg
```

---

## 🏫 Educational Environment Setup

### Classroom Configuration
Optimize for educational use:

#### Shared Settings:
1. **Disable automatic updates**
2. **Set consistent memory allocation**
3. **Configure shared mod folder**
4. **Enable offline mode**

#### Student-Friendly Settings:
```ini
# multimc.cfg additions
[General]
ShowConsole=false
AutoCloseConsole=true
LogPrePostOutput=false

[Java]
MaxMemAlloc=2048
MinMemAlloc=1024
```

### Batch Configuration Script
Automate setup across multiple computers:

#### Windows Batch Script:
```cmd
@echo off
echo Configuring MultiMC for classroom use...

REM Copy configuration
copy "\\server\multimc\multimc.cfg" "%APPDATA%\MultiMC\"

REM Set instance folder
mkdir "C:\MinecraftInstances"
reg add "HKCU\Software\MultiMC" /v "InstanceDir" /t REG_SZ /d "C:\MinecraftInstances"

echo Configuration complete!
```

#### Linux Shell Script:
```bash
#!/bin/bash
echo "Configuring MultiMC for classroom use..."

# Create directories
mkdir -p ~/.local/share/multimc
mkdir -p ~/MinecraftInstances

# Copy configuration
cp /shared/multimc/multimc.cfg ~/.local/share/multimc/

# Set permissions
chmod 644 ~/.local/share/multimc/multimc.cfg

echo "Configuration complete!"
```

---

## 🏢 Enterprise Configuration

### Domain Deployment
For Windows domain environments:

#### Group Policy Settings:
1. **Computer Configuration** → **Administrative Templates**
2. **Create custom ADMX** for MultiMC settings
3. **Deploy via GPO**

#### Registry Settings:
```reg
[HKEY_LOCAL_MACHINE\SOFTWARE\MultiMC]
"InstallPath"="C:\\Program Files\\MultiMC"
"InstancePath"="C:\\MinecraftInstances"
"JavaPath"="C:\\Program Files\\Java\\jdk-17\\bin\\javaw.exe"
"MaxMemory"=dword:00001000
"OfflineMode"=dword:00000001
```

### Centralized Management
Configuration management with Ansible:

```yaml
---
- name: Configure MultiMC for Enterprise
  hosts: workstations
  tasks:
    - name: Create MultiMC config directory
      file:
        path: "{{ ansible_user_dir }}/.local/share/multimc"
        state: directory
        mode: '0755'
    
    - name: Deploy MultiMC configuration
      template:
        src: multimc.cfg.j2
        dest: "{{ ansible_user_dir }}/.local/share/multimc/multimc.cfg"
        mode: '0644'
    
    - name: Set Java path
      lineinfile:
        path: "{{ ansible_user_dir }}/.local/share/multimc/multimc.cfg"
        regexp: '^JavaPath='
        line: 'JavaPath=/usr/lib/jvm/java-17-openjdk/bin/java'
```

---

## 🔍 Troubleshooting Configuration

### Common Configuration Issues

#### Java Not Detected:
```bash
# Verify Java installation
java -version

# Check JAVA_HOME
echo $JAVA_HOME  # Linux/macOS
echo %JAVA_HOME% # Windows

# Manual Java path setting
# Settings → Java → Browse → Select java executable
```

#### Memory Allocation Problems:
```bash
# Check available system memory
free -h  # Linux
vm_stat # macOS
wmic OS get TotalVisibleMemorySize /value # Windows

# Recommended allocation: 50-75% of system RAM
```

#### Instance Launch Failures:
1. **Check console output** for error messages
2. **Verify Java version** compatibility
3. **Test with vanilla instance** first
4. **Review mod compatibility**

### Configuration Validation
Verify your setup:

1. **Create test instance**
2. **Launch vanilla Minecraft**
3. **Check performance** (F3 debug screen)
4. **Test mod installation**
5. **Verify offline functionality**

---

## 📊 Performance Monitoring

### Built-in Monitoring
MultiMC provides performance insights:

1. **Console output** shows memory usage
2. **Launch time** tracking
3. **Java process** monitoring

### External Monitoring Tools
Advanced performance tracking:

#### Windows:
- **Task Manager**: Process monitoring
- **Resource Monitor**: Detailed system usage
- **Process Explorer**: Advanced process info

#### Linux:
```bash
# Monitor MultiMC process
htop -p $(pgrep MultiMC)

# Memory usage
ps aux | grep MultiMC

# Java process monitoring
jstat -gc $(pgrep java)
```

#### macOS:
- **Activity Monitor**: System resource usage
- **Instruments**: Detailed profiling

---

## 📞 Configuration Support

### Getting Help
If you need configuration assistance:

- 📖 **[FAQ](faq.md)** - Common configuration questions
- 🐛 **[Troubleshooting](troubleshooting.md)** - Fix configuration issues
- 💬 **[Community](https://github.com/MultiMC-Launcher/multimc/discussions)** - Ask for help
- 📧 **[Enterprise Support](mailto:enterprise@multimc-launcher.org)** - Professional assistance

### Best Practices
Follow these guidelines:

1. **Start with defaults** and adjust gradually
2. **Test changes** with vanilla instances first
3. **Document custom configurations**
4. **Regular backups** of settings
5. **Monitor performance** after changes

---

**Configuration complete? Learn about [Mod Management](mod-management.md) next!** 🔧 