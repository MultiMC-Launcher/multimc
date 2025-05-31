---
title: "Development Guide - MultiMC Launcher"
description: "Technical documentation for MultiMC launcher development, API reference, and contribution guidelines for developers."
keywords: "multimc development, minecraft launcher api, multimc source code, contribute to multimc"
layout: page
---

# Development Guide

## 🛠 Getting Started with Development

### Prerequisites
- **C++ Compiler**: GCC 7+ or MSVC 2019+
- **Qt Framework**: 5.12+ or 6.2+
- **CMake**: 3.15+
- **Git**: Latest version
- **Java JDK**: 8, 11, 17, 21 for testing

### Development Environment Setup

#### Windows
```cmd
# Install Qt via Qt Installer
# Download from https://www.qt.io/download

# Install Visual Studio 2019/2022 with C++ tools
# Install CMake via Visual Studio Installer

# Clone repository
git clone https://github.com/MultiMC-Launcher/multimc.git
cd multimc

# Configure build
mkdir build
cd build
cmake .. -G "Visual Studio 16 2019" -A x64

# Build
cmake --build . --config Release
```

#### Linux (Ubuntu/Debian)
```bash
# Install dependencies
sudo apt update
sudo apt install build-essential cmake git
sudo apt install qt5-default qtbase5-dev qttools5-dev-tools
sudo apt install openjdk-17-jdk

# Clone and build
git clone https://github.com/MultiMC-Launcher/multimc.git
cd multimc
mkdir build && cd build
cmake .. -DCMAKE_BUILD_TYPE=Release
make -j$(nproc)
```

#### macOS
```bash
# Install Xcode Command Line Tools
xcode-select --install

# Install Qt via Homebrew
brew install qt cmake git openjdk@17

# Clone and build
git clone https://github.com/MultiMC-Launcher/multimc.git
cd multimc
mkdir build && cd build
cmake .. -DCMAKE_BUILD_TYPE=Release -DQt5_DIR=$(brew --prefix qt5)/lib/cmake/Qt5
make -j$(sysctl -n hw.ncpu)
```

## 🏗 Architecture Overview

### Core Components

#### Launcher Core (`src/launcher/`)
- **Application lifecycle management**
- **Instance management and storage**
- **Java runtime detection and management**
- **Update system and version checking**

#### Instance Management (`src/launcher/minecraft/`)
- **Minecraft version handling**
- **Mod loader integration (Forge/Fabric/Quilt)**
- **Asset and library management**
- **Launch parameter generation**

#### UI Framework (`src/launcher/ui/`)
- **Qt-based user interface**
- **Instance creation and editing dialogs**
- **Settings and configuration panels**
- **Console output and logging display**

#### Network Layer (`src/launcher/net/`)
- **HTTP client for downloads**
- **Metadata fetching and caching**
- **Offline mode handling**
- **Progress tracking and error handling**

### Key Classes

#### `Application`
Main application class managing global state:
```cpp
class Application : public QApplication {
    Q_OBJECT
public:
    static Application* getInstance();
    
    // Instance management
    InstanceList* instances();
    JavaInstallList* javalist();
    
    // Settings and configuration
    std::shared_ptr<SettingsObject> settings();
    
    // Network and updates
    std::shared_ptr<HttpMetaCache> metacache();
    std::shared_ptr<UpdateChecker> updateChecker();
};
```

#### `MinecraftInstance`
Represents a single Minecraft installation:
```cpp
class MinecraftInstance : public BaseInstance {
    Q_OBJECT
public:
    // Launch management
    shared_qobject_ptr<LaunchTask> createLaunchTask(AuthSessionPtr session);
    
    // Version management
    std::shared_ptr<PackProfile> getPackProfile();
    
    // Mod management
    std::shared_ptr<ModFolderModel> loaderModList();
    std::shared_ptr<ResourcePackFolderModel> resourcePackList();
    
    // Configuration
    QString getJavaPath();
    int getMemoryInMB();
};
```

#### `LaunchTask`
Handles Minecraft launching process:
```cpp
class LaunchTask : public Task {
    Q_OBJECT
public:
    void executeTask() override;
    
protected:
    // Launch steps
    void checkJavaPath();
    void checkJavaVersion();
    void downloadAssets();
    void downloadLibraries();
    void generateLaunchCommand();
    void launchMinecraft();
};
```

## 🔧 Building and Testing

### Build Configurations

#### Debug Build
```bash
cmake .. -DCMAKE_BUILD_TYPE=Debug
make -j$(nproc)
```

#### Release Build
```bash
cmake .. -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX=/usr/local
make -j$(nproc)
make install
```

#### Portable Build
```bash
cmake .. -DCMAKE_BUILD_TYPE=Release -DMULTIMC_PORTABLE=ON
make -j$(nproc)
```

### Testing Framework

#### Unit Tests
```bash
# Run all tests
ctest --output-on-failure

# Run specific test suite
ctest -R InstanceTest

# Run with verbose output
ctest -V
```

#### Integration Tests
```bash
# Test Minecraft launching
./tests/integration/launch_test

# Test mod installation
./tests/integration/mod_test

# Test offline functionality
./tests/integration/offline_test
```

### Code Quality Tools

#### Static Analysis
```bash
# Clang-tidy
clang-tidy src/**/*.cpp -- -Isrc -Iinclude

# Cppcheck
cppcheck --enable=all --std=c++17 src/
```

#### Code Formatting
```bash
# Format all source files
find src/ -name "*.cpp" -o -name "*.h" | xargs clang-format -i
```

## 📚 API Reference

### Instance Management API

#### Creating Instances
```cpp
// Create new instance
auto instance = std::make_shared<MinecraftInstance>(
    FS::PathCombine(instanceRoot, name),
    settings,
    name
);

// Set Minecraft version
auto profile = instance->getPackProfile();
profile->setComponentVersion("net.minecraft", version);

// Install mod loader
profile->setComponentVersion("net.minecraftforge", forgeVersion);
```

#### Managing Mods
```cpp
// Get mod list
auto modList = instance->loaderModList();

// Install mod
modList->installMod(modFilePath);

// Enable/disable mod
modList->setModStatus(modName, enabled);

// Get mod information
auto mod = modList->getMod(modName);
QString version = mod->version();
QString description = mod->description();
```

### Java Management API

#### Java Detection
```cpp
// Get available Java installations
auto javaList = Application::getInstance()->javalist();
javaList->load();

// Find suitable Java for Minecraft version
auto java = javaList->getJavaForVersion(minecraftVersion);

// Set Java for instance
instance->settings()->set("JavaPath", java->path);
instance->settings()->set("JavaVersion", java->version);
```

#### Memory Management
```cpp
// Set memory allocation
instance->settings()->set("MinMemAlloc", 1024);  // 1GB minimum
instance->settings()->set("MaxMemAlloc", 4096);  // 4GB maximum

// Get system memory info
auto totalMem = Sys::getSystemRam();
auto recommendedMem = std::min(totalMem / 2, 8192);
```

### Launch Process API

#### Custom Launch Steps
```cpp
class CustomLaunchStep : public LaunchStep {
public:
    void executeTask() override {
        // Custom pre-launch logic
        emit logLine("Executing custom step...", MessageLevel::Info);
        
        // Continue to next step
        emitSucceeded();
    }
};

// Add to launch task
launchTask->prependStep(std::make_shared<CustomLaunchStep>());
```

#### Launch Parameters
```cpp
// Customize JVM arguments
QStringList jvmArgs;
jvmArgs << "-XX:+UseG1GC";
jvmArgs << "-XX:+UnlockExperimentalVMOptions";
jvmArgs << QString("-Xms%1m").arg(minMem);
jvmArgs << QString("-Xmx%1m").arg(maxMem);

// Set custom arguments
instance->settings()->set("JvmArgs", jvmArgs.join(' '));
```

## 🔌 Plugin System

### Creating Plugins
```cpp
class MyPlugin : public QObject, public IPlugin {
    Q_OBJECT
    Q_PLUGIN_METADATA(IID "org.multimc.IPlugin")
    Q_INTERFACES(IPlugin)

public:
    QString name() const override { return "MyPlugin"; }
    QString version() const override { return "1.0.0"; }
    
    void initialize() override {
        // Plugin initialization
        connect(Application::getInstance(), &Application::instanceLaunched,
                this, &MyPlugin::onInstanceLaunched);
    }
    
private slots:
    void onInstanceLaunched(MinecraftInstance* instance) {
        // Handle instance launch
        qDebug() << "Instance launched:" << instance->name();
    }
};
```

### Plugin API
```cpp
// Register custom instance type
PluginManager::registerInstanceType<CustomInstance>("custom");

// Add custom settings page
PluginManager::registerSettingsPage<CustomSettingsPage>();

// Register custom mod loader
PluginManager::registerModLoader<CustomModLoader>("custom-loader");
```

## 🚀 Deployment

### Packaging

#### Windows Installer
```bash
# Build installer with NSIS
cmake .. -DCMAKE_BUILD_TYPE=Release
make -j$(nproc)
cpack -G NSIS
```

#### Linux AppImage
```bash
# Build AppImage
cmake .. -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX=/usr
make -j$(nproc)
make DESTDIR=AppDir install
linuxdeploy --appdir AppDir --output appimage
```

#### macOS Bundle
```bash
# Build macOS app bundle
cmake .. -DCMAKE_BUILD_TYPE=Release
make -j$(nproc)
macdeployqt MultiMC.app -dmg
```

### Continuous Integration

#### GitHub Actions Workflow
```yaml
name: Build and Test

on: [push, pull_request]

jobs:
  build:
    strategy:
      matrix:
        os: [ubuntu-latest, windows-latest, macos-latest]
    
    runs-on: ${{ matrix.os }}
    
    steps:
    - uses: actions/checkout@v3
    
    - name: Install Qt
      uses: jurplel/install-qt-action@v3
      with:
        version: '5.15.2'
    
    - name: Configure CMake
      run: cmake -B build -DCMAKE_BUILD_TYPE=Release
    
    - name: Build
      run: cmake --build build --config Release
    
    - name: Test
      run: ctest --test-dir build --output-on-failure
```

## 📖 Contributing Guidelines

### Code Style
- **Follow Qt coding conventions**
- **Use meaningful variable names**
- **Document public APIs with Doxygen**
- **Keep functions focused and small**
- **Use RAII for resource management**

### Commit Guidelines
```bash
# Commit message format
type(scope): description

# Examples
feat(launcher): add offline mode support
fix(instances): resolve mod loading issue
docs(api): update launch task documentation
test(core): add unit tests for instance management
```

### Pull Request Process
1. **Fork the repository**
2. **Create feature branch** from `develop`
3. **Implement changes** with tests
4. **Update documentation** if needed
5. **Submit pull request** with clear description

### Code Review Checklist
- [ ] Code follows style guidelines
- [ ] All tests pass
- [ ] Documentation is updated
- [ ] No breaking changes without discussion
- [ ] Performance impact considered
- [ ] Security implications reviewed

## 🐛 Debugging

### Debug Builds
```bash
# Enable debug symbols
cmake .. -DCMAKE_BUILD_TYPE=Debug -DMULTIMC_DEBUG=ON

# Run with debugger
gdb ./MultiMC
(gdb) run
```

### Logging System
```cpp
// Use MultiMC logging
qDebug() << "Debug message";
qWarning() << "Warning message";
qCritical() << "Critical error";

// Custom log categories
Q_LOGGING_CATEGORY(launcher, "multimc.launcher")
qCDebug(launcher) << "Launcher debug message";
```

### Memory Debugging
```bash
# Valgrind (Linux)
valgrind --tool=memcheck --leak-check=full ./MultiMC

# AddressSanitizer
cmake .. -DCMAKE_BUILD_TYPE=Debug -DENABLE_ASAN=ON
```

## 📞 Developer Support

### Getting Help
- 💬 **[Developer Discussions](https://github.com/MultiMC-Launcher/multimc/discussions/categories/development)**
- 📧 **[Developer Mailing List](mailto:dev@multimc-launcher.org)**
- 🐛 **[Bug Reports](https://github.com/MultiMC-Launcher/multimc/issues)**
- 📖 **[API Documentation](https://docs.multimc-launcher.org/api/)**

### Resources
- **[Qt Documentation](https://doc.qt.io/)**
- **[CMake Documentation](https://cmake.org/documentation/)**
- **[Minecraft Wiki](https://minecraft.fandom.com/wiki/)**
- **[Mod Loader Documentation](https://docs.minecraftforge.net/)**

---

**Ready to contribute? Check out our [good first issues](https://github.com/MultiMC-Launcher/multimc/labels/good%20first%20issue)!** 🚀 