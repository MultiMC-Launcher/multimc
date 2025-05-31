---
title: "Troubleshooting Guide - MultiMC Launcher"
description: "Complete troubleshooting guide for MultiMC offline Minecraft launcher. Fix installation, startup, mod, and performance issues."
keywords: "multimc troubleshooting, minecraft launcher problems, offline minecraft issues, multimc not working"
layout: page
---

# Troubleshooting Guide

## 🚨 Common Issues & Quick Fixes

### MultiMC Won't Start

#### Problem: Application doesn't launch
**Symptoms:**
- Double-clicking does nothing
- Error message on startup
- Application crashes immediately

**Solutions:**
1. **Run as Administrator** (Windows)
   ```cmd
   Right-click MultiMC.exe → "Run as administrator"
   ```

2. **Check Java Installation**
   ```bash
   java -version
   ```
   If Java is missing, run Setup Assistant again

3. **Verify File Permissions**
   ```bash
   # Linux/macOS
   chmod +x MultiMC
   chmod -R 755 MultiMC/
   ```

4. **Disable Antivirus Temporarily**
   - Some antivirus software blocks Java applications
   - Add MultiMC folder to exclusions

5. **Check System Requirements**
   - Windows 7+ / macOS 10.12+ / Ubuntu 16.04+
   - 4GB RAM minimum
   - 2GB free disk space

#### Problem: "Java not found" error
**Solution:**
```bash
# Download and run Setup Assistant again
./Setup-Assistant.bat  # Windows
./setup.sh             # Linux/macOS
```

### Installation Issues

#### Problem: Setup Assistant fails
**Common causes:**
- Insufficient permissions
- Corrupted download
- Antivirus interference

**Solutions:**
1. **Re-download Setup Assistant**
   - Verify file integrity
   - Use different download method

2. **Run with elevated privileges**
   ```cmd
   # Windows
   Right-click → "Run as administrator"
   
   # Linux/macOS
   sudo ./setup.sh
   ```

3. **Temporarily disable antivirus**
   - Add exception for MultiMC folder
   - Re-enable after installation

#### Problem: Cannot extract archive
**Solutions:**
1. **Use different extraction tool**
   - 7-Zip (recommended)
   - WinRAR
   - Built-in Windows extractor

2. **Check available disk space**
   - Need 2GB+ free space
   - Clear temporary files if needed

3. **Download to different location**
   - Avoid special characters in path
   - Use shorter folder names

### Minecraft Launch Issues

#### Problem: Minecraft won't start
**Diagnostic steps:**
1. **Check console output**
   - MultiMC shows detailed logs
   - Look for error messages

2. **Verify Minecraft version**
   - Ensure version is supported
   - Try vanilla Minecraft first

3. **Test with minimal setup**
   - Remove all mods
   - Use default settings
   - Gradually add components

#### Problem: "Out of memory" errors
**Solutions:**
1. **Increase memory allocation**
   ```
   Edit Instance → Settings → Java
   Maximum memory: 4096 MB (4GB)
   Minimum memory: 1024 MB (1GB)
   ```

2. **Close other applications**
   - Free up system RAM
   - Check Task Manager/Activity Monitor

3. **Use 64-bit Java**
   - Required for >4GB memory
   - Setup Assistant installs correct version

#### Problem: Minecraft crashes during gameplay
**Common fixes:**
1. **Update graphics drivers**
   - NVIDIA: GeForce Experience
   - AMD: Radeon Software
   - Intel: Intel Driver & Support Assistant

2. **Reduce graphics settings**
   - Lower render distance
   - Disable fancy graphics
   - Turn off shaders

3. **Check mod compatibility**
   - Remove recently added mods
   - Verify mod versions match Minecraft

### Mod-Related Issues

#### Problem: Mods not loading
**Troubleshooting:**
1. **Verify mod loader**
   ```
   Edit Instance → Version → Install Forge/Fabric
   ```

2. **Check mod compatibility**
   - Minecraft version must match
   - Mod loader version must be compatible

3. **Install dependencies**
   - Some mods require libraries
   - Check mod documentation

#### Problem: Mod conflicts
**Symptoms:**
- Crashes when loading world
- Missing items/blocks
- Strange behavior

**Solutions:**
1. **Binary search method**
   - Remove half the mods
   - Test if problem persists
   - Narrow down problematic mod

2. **Check mod compatibility lists**
   - Some mods don't work together
   - Look for known conflicts

3. **Update conflicting mods**
   - Newer versions may fix conflicts
   - Check mod changelogs

#### Problem: OptiFine issues
**Common problems:**
- Shaders not working
- Performance worse than vanilla
- Texture glitches

**Solutions:**
1. **Use correct OptiFine version**
   - Must match Minecraft version exactly
   - Download from official site only

2. **Disable conflicting features**
   - Turn off shaders temporarily
   - Disable advanced graphics options

3. **Try alternative performance mods**
   - Sodium (Fabric)
   - Phosphor (Fabric)
   - Lithium (Fabric)

### Performance Issues

#### Problem: Low FPS/stuttering
**Optimization steps:**
1. **Allocate appropriate memory**
   - Too little: stuttering
   - Too much: garbage collection lag
   - Sweet spot: 4-6GB for modded

2. **Optimize Java arguments**
   ```
   -XX:+UseG1GC -XX:+UnlockExperimentalVMOptions -XX:MaxGCPauseMillis=100 -XX:+DisableExplicitGC -XX:TargetSurvivorRatio=90 -XX:G1NewSizePercent=50 -XX:G1MaxNewSizePercent=80 -XX:G1MixedGCLiveThresholdPercent=35 -XX:+AlwaysPreTouch
   ```

3. **Reduce graphics settings**
   - Render distance: 8-12 chunks
   - Graphics: Fast
   - Smooth lighting: Off

#### Problem: Long loading times
**Solutions:**
1. **Install on SSD**
   - Significantly faster than HDD
   - Move MultiMC folder to SSD

2. **Reduce mod count**
   - Each mod increases loading time
   - Remove unused mods

3. **Optimize world settings**
   - Smaller world sizes
   - Fewer entities
   - Regular world cleanup

### Network/Multiplayer Issues

#### Problem: Can't connect to servers (offline mode)
**Expected behavior:**
- Internet servers won't work offline
- LAN servers should work
- Local hosting is possible

**Solutions for offline multiplayer:**
1. **Use LAN hosting**
   ```
   Minecraft → Open to LAN
   Other players connect via local IP
   ```

2. **Set up local server**
   - Install Minecraft server
   - Configure for LAN use
   - Use same mod versions

#### Problem: Authentication errors
**In offline mode:**
- Expected behavior
- No Microsoft account needed
- Local authentication only

**Solutions:**
1. **Verify offline mode enabled**
   ```
   Edit Instance → Settings → Miscellaneous
   ✓ Work offline
   ```

2. **Use offline usernames**
   - Any username works
   - No special characters
   - Keep consistent for saves

### File System Issues

#### Problem: Permission denied errors
**Linux/macOS solutions:**
```bash
# Fix permissions
chmod -R 755 /path/to/MultiMC/
chown -R $USER:$USER /path/to/MultiMC/

# Run with proper permissions
sudo ./MultiMC
```

**Windows solutions:**
1. Run as Administrator
2. Check folder permissions
3. Disable UAC temporarily

#### Problem: Corrupted instances
**Symptoms:**
- Instance won't load
- Missing files
- Crashes on launch

**Recovery steps:**
1. **Restore from backup**
   ```
   MultiMC/instances/[instance]/backups/
   ```

2. **Recreate instance**
   - Export world saves first
   - Create new instance
   - Import saves and mods

3. **Verify file integrity**
   - Check for corrupted files
   - Re-download if needed

### Advanced Troubleshooting

#### Collecting Debug Information

**System Information:**
```bash
# Windows
systeminfo

# macOS
system_profiler SPSoftwareDataType

# Linux
uname -a
lscpu
free -h
```

**MultiMC Logs:**
- Location: `MultiMC/logs/`
- Latest: `latest.log`
- Crash reports: `crash-reports/`

**Java Information:**
```bash
java -version
java -XshowSettings:vm
```

#### Creating Minimal Test Case

1. **Fresh instance**
   - Create new instance
   - Vanilla Minecraft only
   - Test if issue persists

2. **Add components gradually**
   - Add mod loader
   - Add one mod at a time
   - Identify problematic component

3. **Document findings**
   - Note exact steps to reproduce
   - Include system information
   - Attach relevant logs

### Getting Help

#### Before Reporting Issues

**Check existing resources:**
- [FAQ](faq.md) - Common questions
- [Documentation](index.md) - Complete guides
- [GitHub Issues](https://github.com/MultiMC-Launcher/multimc/issues) - Known problems

**Gather information:**
- System specifications
- MultiMC version
- Minecraft version
- Mod list (if applicable)
- Error messages/logs

#### Reporting Bugs

**Use our bug report template:**
1. Go to [GitHub Issues](https://github.com/MultiMC-Launcher/multimc/issues)
2. Click "New Issue"
3. Select "Bug Report"
4. Fill out all sections
5. Attach log files

**Include:**
- Clear description of problem
- Steps to reproduce
- Expected vs actual behavior
- System information
- Log files

#### Community Support

**Get help from community:**
- [GitHub Discussions](https://github.com/MultiMC-Launcher/multimc/discussions)
- [Discord Server](https://discord.gg/multimc)
- [Reddit Community](https://reddit.com/r/MultiMC)

**Enterprise Support:**
- Email: enterprise@multimc-launcher.org
- Priority support for business users
- Custom deployment assistance

---

## 🔧 Emergency Recovery

### Complete Reset
If all else fails, perform a clean installation:

1. **Backup important data**
   ```
   Copy: MultiMC/instances/*/minecraft/saves/
   Copy: MultiMC/instances/*/mods/
   ```

2. **Remove MultiMC completely**
   ```bash
   # Delete entire MultiMC folder
   rm -rf MultiMC/  # Linux/macOS
   # Or delete folder in Windows Explorer
   ```

3. **Fresh installation**
   - Download Setup Assistant again
   - Run installation process
   - Restore backed up data

### Contact Support
If you're still experiencing issues:
- 📧 **Enterprise users**: enterprise@multimc-launcher.org
- 💬 **Community**: [GitHub Discussions](https://github.com/MultiMC-Launcher/multimc/discussions)
- 🐛 **Bug reports**: [GitHub Issues](https://github.com/MultiMC-Launcher/multimc/issues)

**We're here to help make your offline Minecraft experience perfect!** 🎮 