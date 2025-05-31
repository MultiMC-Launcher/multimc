---
title: "Mod Management Guide - MultiMC Launcher"
description: "Complete guide to managing Minecraft mods with MultiMC launcher. Install Forge, Fabric, Quilt mods offline and resolve conflicts."
keywords: "multimc mod management, minecraft mods offline, forge fabric quilt, mod installation multimc"
layout: page
---

# Mod Management Guide

## 🔧 Mod Loader Setup

### Supported Mod Loaders
MultiMC supports all major Minecraft mod loaders:

- **🔥 Forge**: Most popular, extensive mod ecosystem
- **🧵 Fabric**: Lightweight, fast updates
- **🪡 Quilt**: Fabric fork with additional features
- **⚡ NeoForge**: Modern Forge alternative

### Installing Mod Loaders

#### Forge Installation
1. **Edit Instance** → **Version** tab
2. **Install Forge** button
3. **Select version** compatible with Minecraft
4. **Install** and wait for completion

#### Fabric Installation
1. **Edit Instance** → **Version** tab
2. **Install Fabric** button
3. **Choose Fabric Loader version**
4. **Install Fabric API** (recommended)

#### Quilt Installation
1. **Edit Instance** → **Version** tab
2. **Install Quilt** button
3. **Select Quilt Loader version**
4. **Install Quilted Fabric API** if needed

---

## 📦 Installing Mods

### Offline Mod Installation
Perfect for air-gapped systems:

#### Step-by-Step Process:
1. **Download mods** on internet-connected computer
2. **Transfer mod files** (.jar) to offline system
3. **Open MultiMC** → Select instance
4. **Edit Instance** → **Loader Mods** tab
5. **Add** button or **drag & drop** mod files
6. **Enable mods** in the list

### Online Mod Installation
When internet is available:

#### From CurseForge:
1. **Edit Instance** → **Loader Mods**
2. **Download Mods** button
3. **Search** for desired mod
4. **Select version** compatible with your setup
5. **Install** automatically

#### From Modrinth:
1. **Edit Instance** → **Loader Mods**
2. **Browse Modrinth** option
3. **Search and filter** mods
4. **One-click install** with dependencies

### Manual Mod Installation
For custom or development mods:

```bash
# Mod file locations
instances/[instance_name]/minecraft/mods/

# Copy mod files
cp ~/Downloads/MyMod-1.19.4.jar instances/MyInstance/minecraft/mods/
```

---

## 🗂 Mod Organization

### Mod Categories
Organize mods by function:

#### **Performance Mods**
- **OptiFine**: Graphics optimization and shaders
- **Sodium**: Fabric rendering optimization
- **Lithium**: Server-side optimizations
- **Phosphor**: Lighting engine improvements

#### **Utility Mods**
- **JEI (Just Enough Items)**: Recipe viewer
- **WAILA/Hwyla**: Block information display
- **Inventory Tweaks**: Automatic sorting
- **JourneyMap**: Advanced mapping

#### **Content Mods**
- **Biomes O' Plenty**: New biomes and blocks
- **Tinkers' Construct**: Tool crafting system
- **Applied Energistics**: Storage and automation
- **Thermal Expansion**: Machines and energy

#### **Quality of Life**
- **Iron Chests**: Better storage options
- **Fast Leaf Decay**: Faster tree cleanup
- **Mouse Tweaks**: Improved inventory handling
- **Appleskin**: Food information display

### Mod Profiles
Create different mod configurations:

1. **Duplicate instance** for different mod sets
2. **Name instances** descriptively:
   - "Vanilla Plus" (minimal mods)
   - "Tech Modded" (industrial mods)
   - "Magic Modded" (fantasy mods)
   - "Performance" (optimization only)

---

## ⚙️ Mod Configuration

### Config File Management
Most mods create configuration files:

#### Config Locations:
```
instances/[instance]/minecraft/config/
├── mod1.cfg
├── mod2.json
└── mod3/
    ├── client.toml
    └── server.toml
```

#### Common Config Tasks:
1. **Edit config files** with text editor
2. **Backup configs** before changes
3. **Share configs** across instances
4. **Reset to defaults** if needed

### In-Game Configuration
Many mods provide in-game config:

- **Mod Options** in main menu
- **Key bindings** for mod features
- **GUI-based settings** panels
- **Command-based** configuration

### Resource Pack Integration
Mods often include resource packs:

1. **Check mod documentation** for resource packs
2. **Download additional textures** if available
3. **Enable in Minecraft** → Options → Resource Packs
4. **Order matters** - place mod packs correctly

---

## 🔍 Dependency Management

### Understanding Dependencies
Mods often require other mods to function:

#### Types of Dependencies:
- **Required**: Mod won't work without it
- **Optional**: Adds features if present
- **Incompatible**: Conflicts with certain mods

### Automatic Dependency Resolution
MultiMC helps manage dependencies:

1. **Install main mod** first
2. **Check for missing dependencies**
3. **Auto-download** required mods
4. **Verify compatibility** warnings

### Manual Dependency Installation
For offline environments:

#### Common Dependencies:
- **Forge**: `MinecraftForge-[version].jar`
- **Fabric API**: `fabric-api-[version].jar`
- **Architectury API**: `architectury-[version].jar`
- **Cloth Config**: `cloth-config-[version].jar`

#### Installation Order:
1. **Core libraries** first
2. **API mods** second
3. **Content mods** last
4. **Test launch** after each addition

---

## 🚫 Conflict Resolution

### Identifying Conflicts
Common signs of mod conflicts:

- **Crash on startup**
- **Missing items/blocks**
- **Duplicate recipes**
- **Performance issues**
- **Strange behavior**

### Conflict Resolution Process

#### Binary Search Method:
1. **Remove half** of your mods
2. **Test if problem persists**
3. **Narrow down** to problematic mod
4. **Identify specific conflict**

#### Systematic Testing:
```bash
# Test with minimal mods
1. Forge/Fabric only
2. Add core dependencies
3. Add one mod at a time
4. Test after each addition
```

### Common Conflict Types

#### ID Conflicts:
- **Block/Item IDs** overlap
- **Recipe conflicts**
- **Biome ID conflicts**

#### Compatibility Issues:
- **Version mismatches**
- **API incompatibilities**
- **Core mod conflicts**

#### Performance Conflicts:
- **Multiple optimization mods**
- **Overlapping features**
- **Resource competition**

---

## 📊 Performance Optimization

### Mod Performance Impact
Monitor mod performance:

#### High Impact Mods:
- **World generation** mods
- **Graphics enhancement** mods
- **Large content** additions
- **Automation** systems

#### Low Impact Mods:
- **Utility** mods
- **Interface** improvements
- **Quality of life** features
- **Small content** additions

### Optimization Strategies

#### Memory Management:
```bash
# Increase memory for modded instances
Minimum: 2GB (light modding)
Recommended: 4-6GB (heavy modding)
Maximum: 8-12GB (extreme modding)
```

#### Performance Mods Combination:
```
Forge: OptiFine + FoamFix + BetterFps
Fabric: Sodium + Lithium + Phosphor + Starlight
```

#### JVM Arguments for Modded:
```bash
-XX:+UseG1GC
-XX:+UnlockExperimentalVMOptions
-XX:MaxGCPauseMillis=100
-XX:G1NewSizePercent=20
-XX:G1ReservePercent=20
-XX:MaxGCPauseMillis=50
-XX:G1HeapRegionSize=32M
```

---

## 🎯 Modpack Management

### Creating Custom Modpacks
Build your own modpack:

1. **Start with base** instance
2. **Add mods gradually**
3. **Test compatibility**
4. **Configure settings**
5. **Document mod list**

### Modpack Export/Import

#### Export Modpack:
1. **Right-click instance**
2. **Export Instance**
3. **Choose format** (MultiMC, CurseForge, etc.)
4. **Include configs** and saves if desired

#### Import Modpack:
1. **Add Instance** → **Import from zip**
2. **Select modpack file**
3. **Configure settings**
4. **Launch and test**

### Sharing Modpacks
Distribute your modpack:

#### For Classrooms:
```bash
# Create shared modpack
1. Export instance as zip
2. Place on shared network drive
3. Students import from network location
4. Consistent experience across computers
```

#### For Teams:
```bash
# Version control for modpacks
1. Use Git repository for configs
2. Document mod versions
3. Provide installation scripts
4. Maintain changelog
```

---

## 🏫 Educational Mod Collections

### STEM Education Mods
Mods perfect for learning:

#### Programming & Logic:
- **ComputerCraft**: Lua programming
- **OpenComputers**: Advanced computing
- **Redstone++**: Logic circuits
- **Project Red**: Advanced redstone

#### Science & Engineering:
- **Immersive Engineering**: Realistic machines
- **Mekanism**: Chemistry and physics
- **Applied Energistics**: Network systems
- **BuildCraft**: Automation and logistics

#### Mathematics:
- **Calculator**: Mathematical operations
- **Geometry**: 3D shapes and structures
- **Statistics**: Data collection mods
- **Graphing**: Visual mathematics

### Classroom-Ready Modpacks
Pre-configured educational setups:

#### "STEM Learning Pack":
```
- ComputerCraft (programming)
- Immersive Engineering (physics)
- Applied Energistics (systems)
- JEI (information lookup)
- JourneyMap (navigation)
```

#### "Creative Building Pack":
```
- WorldEdit (terrain editing)
- Architect (building tools)
- Chisel (decorative blocks)
- Carpenter's Blocks (custom shapes)
- Decocraft (furniture)
```

---

## 🔧 Advanced Mod Management

### Mod Development Environment
Set up for mod development:

#### Development Tools:
- **MCreator**: Visual mod creation
- **IntelliJ IDEA**: Java development
- **Eclipse**: Alternative IDE
- **Blockbench**: Model creation

#### Testing Environment:
```bash
# Development instance setup
1. Install mod loader
2. Add development tools
3. Enable debug logging
4. Configure hot-reload
```

### Custom Mod Installation
Install development/beta mods:

#### From Source:
```bash
# Compile mod from source
git clone https://github.com/modauthor/modname.git
cd modname
./gradlew build
cp build/libs/modname-*.jar instances/test/minecraft/mods/
```

#### Beta Versions:
1. **Download from** mod author's GitHub
2. **Check compatibility** warnings
3. **Backup instance** before testing
4. **Report bugs** to developers

---

## 📞 Mod Support

### Getting Help with Mods

#### Mod-Specific Issues:
- **Check mod documentation** first
- **Visit mod's GitHub/CurseForge** page
- **Search existing issues**
- **Contact mod author** if needed

#### MultiMC Mod Issues:
- **[MultiMC Discussions](https://github.com/MultiMC-Launcher/multimc/discussions)**
- **[Troubleshooting Guide](troubleshooting.md)**
- **[FAQ](faq.md)** for common problems

### Best Practices
Follow these guidelines:

1. **Read mod descriptions** thoroughly
2. **Check compatibility** before installing
3. **Backup instances** before major changes
4. **Update mods** carefully
5. **Document your setup**

### Mod Recommendations by Use Case

#### **Beginner Friendly**:
- OptiFine (performance)
- JEI (recipes)
- JourneyMap (navigation)
- Iron Chests (storage)

#### **Advanced Users**:
- Applied Energistics (automation)
- Thermal Expansion (machines)
- Tinkers' Construct (tools)
- Botania (magic)

#### **Performance Focus**:
- Sodium + Lithium + Phosphor (Fabric)
- OptiFine + FoamFix (Forge)
- FastCraft (older versions)

---

**Ready to explore more? Check out our [Enterprise Deployment](enterprise.md) guide!** 🚀 