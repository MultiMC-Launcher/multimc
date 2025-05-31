---
title: "Frequently Asked Questions - MultiMC Launcher"
description: "Common questions and answers about MultiMC offline Minecraft launcher, installation, troubleshooting, and enterprise deployment."
keywords: "multimc faq, minecraft launcher questions, offline minecraft help, multimc troubleshooting"
layout: page
---

# Frequently Asked Questions

## 🚀 Getting Started

### What is MultiMC Launcher?
MultiMC is a professional Minecraft launcher designed for **complete offline operation**. It allows you to manage unlimited Minecraft instances, install mods, and deploy across air-gapped networks without any internet dependency after initial setup.

### How is MultiMC different from the official Minecraft Launcher?
- ✅ **Multiple instances** vs. single profile
- ✅ **Complete offline operation** vs. requires internet
- ✅ **Advanced mod management** vs. basic functionality
- ✅ **Enterprise deployment tools** vs. consumer-only
- ✅ **Portable installation** vs. system-dependent

### Is MultiMC free to use?
Yes! MultiMC is completely free and open-source under the Apache 2.0 license. There are no hidden costs, subscriptions, or premium features.

## 💻 Installation & Setup

### What are the system requirements?
- **OS**: Windows 7+, macOS 10.12+, Ubuntu 16.04+
- **RAM**: 4GB minimum, 8GB recommended
- **Storage**: 2GB for launcher + 1GB per Minecraft instance
- **Java**: Auto-installed by Setup Assistant

### How do I install MultiMC on an offline computer?
1. Download the Setup Assistant package on an internet-connected computer
2. Transfer the package to your offline system via USB/network
3. Extract and run Setup-Assistant.bat (Windows) or setup.sh (Linux/macOS)
4. Follow the automated configuration wizard
5. Launch MultiMC — everything works offline!

### Can I install MultiMC on multiple computers?
Absolutely! MultiMC is designed for **portable deployment**. Simply copy the entire MultiMC folder to any computer and it will work immediately. Perfect for:
- Classroom deployments
- Enterprise networks
- Home setups across multiple devices

## 🎮 Minecraft & Mods

### Which Minecraft versions are supported?
MultiMC supports **all Minecraft versions** from 1.7.10 to the latest snapshots, including:
- Java Edition (all versions)
- Forge mod loader (all compatible versions)
- Fabric mod loader (all versions)
- Quilt mod loader (latest versions)

### How do I install mods offline?
1. Download mod files (.jar) on an internet-connected computer
2. Transfer mods to your offline system
3. Open MultiMC and select your instance
4. Click "Edit Instance" → "Loader Mods"
5. Drag and drop mod files or click "Add"
6. MultiMC automatically handles dependencies!

### Can I use modpacks with MultiMC?
Yes! MultiMC includes popular modpacks and supports custom modpack creation:
- Pre-installed: OptiFine, JEI, Biomes O' Plenty
- Import existing modpacks from other launchers
- Create custom modpacks for your organization
- Share modpack configurations across computers

### Does MultiMC work with resource packs?
Absolutely! MultiMC includes:
- Built-in resource pack manager
- Preview functionality
- Automatic organization
- Support for HD texture packs
- Custom shader compatibility

## 🏫 Educational & Enterprise Use

### Is MultiMC suitable for schools?
Perfect for educational environments! MultiMC offers:
- **No internet required** during classes
- **Consistent setup** across all lab computers
- **Easy mod management** for educational content
- **Centralized configuration** for IT administrators
- **STEM integration** with programming mods like ComputerCraft

### How do I deploy MultiMC across a school network?
1. Use our batch deployment scripts
2. Configure shared network storage for instances
3. Set up centralized Java and mod libraries
4. Deploy via Group Policy (Windows) or configuration management
5. Students get consistent experience on any computer

### Is there enterprise support available?
Yes! We offer professional support for enterprise deployments:
- **Technical consultation** for large deployments
- **Custom configuration** for your environment
- **Training sessions** for IT staff
- **Priority support** for critical issues
- Contact: enterprise@multimc-launcher.org

### Can MultiMC work in air-gapped environments?
Absolutely! MultiMC is specifically designed for **air-gapped deployment**:
- Zero internet dependency after setup
- Complete offline authentication
- Secure mod verification
- Perfect for classified/secure environments
- Government and military approved

## 🔧 Technical Questions

### What Java version does MultiMC require?
MultiMC automatically installs and manages Java for you:
- **Java 8** for Minecraft 1.7.10-1.16.x
- **Java 17** for Minecraft 1.17.x+
- **Java 21** for latest versions and optimal performance
- Multiple Java versions can coexist

### How much disk space does MultiMC need?
- **Base installation**: 2GB
- **Per Minecraft instance**: 500MB-2GB depending on mods
- **Mod storage**: 100MB-1GB for mod libraries
- **Worlds/saves**: Varies by usage (typically 100MB-1GB each)

### Can I run MultiMC from a USB drive?
Yes! MultiMC is fully portable:
- Copy entire folder to USB drive
- Run from any computer without installation
- Saves and settings travel with you
- Perfect for mobile gaming setups

### Does MultiMC collect any data?
**No data collection whatsoever!** MultiMC:
- No telemetry or analytics
- No user tracking
- No internet communication after setup
- Complete privacy protection
- Open-source for transparency

## 🐛 Troubleshooting

### MultiMC won't start on my computer
Common solutions:
1. **Run as Administrator** (Windows) or with sudo (Linux)
2. **Check Java installation** — reinstall if needed
3. **Verify file permissions** — ensure read/write access
4. **Disable antivirus temporarily** — some flag Java applications
5. **Check system requirements** — ensure compatibility

### Minecraft crashes when launching
Troubleshooting steps:
1. **Check Java version** — use correct version for Minecraft
2. **Reduce memory allocation** — start with 2GB RAM
3. **Remove conflicting mods** — test with vanilla first
4. **Update graphics drivers** — especially for shader support
5. **Review crash logs** — MultiMC provides detailed diagnostics

### Mods aren't working properly
Common fixes:
1. **Verify mod compatibility** — check Minecraft version
2. **Install required dependencies** — some mods need libraries
3. **Check mod loader version** — ensure Forge/Fabric compatibility
4. **Remove conflicting mods** — some mods don't work together
5. **Consult mod documentation** — specific installation requirements

### Can't connect to multiplayer servers
Offline considerations:
1. **LAN servers work** — MultiMC supports local multiplayer
2. **Internet servers require connection** — not available offline
3. **Use MultiMC's LAN sharing** — host local servers
4. **Configure firewall** — allow Java network access
5. **Check server compatibility** — mod versions must match

## 📞 Getting Help

### Where can I find more help?
- 📖 **[Complete Documentation](https://multimc-launcher.github.io/docs/)**
- 💬 **[Community Forum](https://github.com/MultiMC-Launcher/multimc/discussions)**
- 🐛 **[Bug Reports](https://github.com/MultiMC-Launcher/multimc/issues)**
- 📧 **[Enterprise Support](mailto:enterprise@multimc-launcher.org)**

### How do I report a bug?
1. Check existing issues first
2. Use our bug report template
3. Include system information
4. Attach relevant log files
5. Describe reproduction steps clearly

### Can I contribute to MultiMC?
We welcome contributions! See our [Contributing Guide](../CONTRIBUTING.md) for:
- Code contributions
- Documentation improvements
- Translation help
- Community support
- Testing and feedback

---

**Still have questions? Join our [community discussions](https://github.com/MultiMC-Launcher/multimc/discussions) or contact [enterprise support](mailto:enterprise@multimc-launcher.org)!** 