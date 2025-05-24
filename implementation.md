# FileCentipede Implementation Documentation

## Overview

FileCentipede is an All-In-One internet file upload/download manager, BitTorrent Client, WebDAV client, FTP client, and SSH client. This document provides a comprehensive breakdown of the project's structure, dependencies, implementation details, and compilation instructions.

## Project Structure

```
FileCentipede/
├── source_code/                 # Source code for the application
│   ├── fileu/                   # Main application code
│   │   ├── catalogs/            # File categorization
│   │   ├── dialogs/             # UI dialog components
│   │   ├── file_browser/        # File browsing functionality
│   │   ├── file_manager/        # File management operations
│   │   ├── help/                # Help documentation
│   │   ├── plugins/             # Plugin system
│   │   ├── search_engine/       # Search functionality
│   │   ├── settings/            # Application settings
│   │   ├── tasks/               # Task management system
│   │   ├── tools/               # Utility tools
│   │   ├── view/                # UI view components
│   │   ├── main.cpp             # Application entry point
│   │   ├── main_window.cpp      # Main window implementation
│   │   ├── main_window.h        # Main window header
│   │   ├── pro_global.cpp       # Global constants/functions
│   │   ├── pro_global.h         # Global header
│   │   ├── pro_headers.h        # Precompiled header
│   │   ├── pro_methods.cpp      # Common methods
│   │   ├── pro_methods.h        # Common methods header
│   │   ├── pro_sample.h         # Sample code
│   │   ├── CMakeLists.txt       # Build configuration
│   │   └── resources_win32.rc   # Windows resources
│   └── fileu_launch/            # Application launcher
│       ├── main.cpp             # Launcher entry point
│       ├── CMakeLists.txt       # Launcher build configuration
│       └── resources_win32.rc   # Windows resources
├── release/                     # Compiled binaries
│   ├── filecxx_latest_win_x64/  # Latest Windows build
│   │   ├── browser_extensions/  # Browser extensions
│   │   ├── filec.exe            # Main executable
│   │   ├── fileu.exe            # User interface executable
│   │   ├── icons/               # Application icons
│   │   ├── images/              # Application images
│   │   ├── lang/                # Language files
│   │   ├── lib/                 # Library dependencies
│   │   ├── plugins/             # Plugin files
│   │   ├── sounds/              # Sound resources
│   │   ├── ui/                  # UI definition files (.sml)
│   │   └── webui/               # Web interface files
│   └── ...                      # Other builds
├── script/                      # JavaScript files for website
├── style/                       # CSS files for website
├── images/                      # Screenshots and images
├── lang/                        # Language files
├── README.md                    # Primary documentation
└── update.json                  # Update information
```

## Technology Stack

### Languages
- **C++**: Modern C++11/14/17 for the core application
- **HTML/CSS/JavaScript**: For the website and browser extensions
- **CMake**: Build system

### Main Dependencies

#### Open Source Libraries
1. **Qt Framework 5.15.2**
   - Primary GUI framework
   - Used modules: Qt5Widgets, Qt5Svg

2. **Boost Libraries**
   - boost_locale: Internationalization
   - boost_nowide: Unicode filesystem operations
   - Various Boost algorithms and utilities

3. **WolfSSL**
   - SSL/TLS implementation for secure connections

4. **libtorrent**
   - BitTorrent protocol implementation

#### Proprietary/Custom Libraries

1. **extcpp Libraries** - Custom C++ utility libraries:
   - `ext_ui` - Custom UI framework extending Qt
   - `ext_net` - Networking library (HTTP, FTP, SSH)
   - `ext_uri` - URI parsing and handling
   - `ext_fs` - File system operations
   - `ext_archive` - Archive handling (ZIP, etc.)
   - `ext_process` - Process management
   - `ext_compressor` - Compression algorithms
   - `ext_crypto` - Cryptography functions
   - `ext_os` - OS-specific functionality
   - `ext_runtime` - Runtime utilities

2. **doom Libraries** - System-level libraries:
   - `doom_ipdb` - IP database functionality
   - `doom_privilege` - System privilege management
   - `doom_custom` - Custom utilities
   - `doom_startup` - Application startup handling

## UI System

FileCentipede uses a custom UI description language with `.sml` files. These files define the layout and behavior of the user interface in a declarative manner. As noted in the README:

> "It has proved that writing user interfaces in C++ could be significantly easier than HTML and JavaScript, without reducing performance."

The `.sml` format appears to be a proprietary markup language with CSS-like syntax that is parsed and rendered by the `ext_ui` library. This approach allows for defining UI layouts in a declarative manner while maintaining the performance benefits of C++.

Example of an `.sml` file structure:
```
Dialog#main
{
    title:"${software_name_} - ${activation_code}"
    layout:VBoxLayout
    w:600
    h:400
    
    HBoxLayout
    {
        "UID:" LineEdit#uid{
            name:uid
            readonly:true
        }
        ToolButton{
            icon:"icons/16/copy.svg"
            click:$copy(${#uid})
        }
    }
}
```

## Protocol Implementations

FileCentipede supports multiple file transfer protocols:

1. **HTTP/HTTPS**
   - Multi-connection downloads
   - Cookie/header management
   - Gzip support
   - Resumable downloads

2. **FTP/FTPS**
   - Secure file transfers
   - Directory browsing

3. **BitTorrent**
   - Magnet link support
   - Torrent creation/management
   - DHT network

4. **WebDAV**
   - File browsing and management

5. **SSH/SFTP**
   - Secure shell and file transfer

6. **Custom Protocols**
   - Thunder, Flashget, qqdl protocols
   - m3u8 stream downloads with decryption

## Browser Extensions

FileCentipede includes browser extensions for:

- Chrome (standard and Manifest v3)
- Firefox

These extensions provide:
- Video/audio capture from websites
- Resource exploration
- Integration with the main application

## Compilation Instructions

### Prerequisites

1. **Required Software**
   - CMake 3.2 or higher
   - C++ compiler with C++17 support (GCC 8+ or MinGW 8.1+ on Windows)
   - Qt 5.15.2
   - Boost libraries (1.71.0 or higher recommended)
   - WolfSSL for secure connections
   - libtorrent-rasterbar (1.2.x or compatible)

2. **Proprietary Libraries**
   - The proprietary `ext_*` and `doom_*` libraries are required but not publicly available
   - Check for any available binary distributions from the official FileCentipede website

3. **Directory Structure Setup**
   Before building, ensure your project follows this structure:
   ```
   project_root/
   ├── source_code/
   │   ├── fileu/
   │   └── fileu_launch/
   ├── lib/
   │   ├── ext/           # extcpp libraries
   │   ├── doom/          # doom libraries
   │   ├── boost/         # Boost libraries
   │   └── qt/            # Qt libraries (optional local copy)
   └── bin/               # Output directory
   ```

4. **Environment Variables**
   - Set `EXTCPP_ROOT` to point to your extcpp libraries location
   - Set `DOOM_ROOT` to point to your doom libraries location

### Build Steps for Windows

1. **Setup Qt**
   - Install Qt 5.15.2 with MinGW 8.1
   - Set the Qt path in CMakeLists.txt

2. **Configure CMake**
   ```bash
   mkdir build
   cd build
   cmake -G "MinGW Makefiles" -DCMAKE_BUILD_TYPE=Release ../source_code
   ```

3. **Build the project**
   ```bash
   cmake --build .
   ```

4. **Output**
   - The compiled application will be in the `bin/lib` directory
   - The launcher will be in the `bin` directory

### Build Steps for Linux

1. **Setup Qt**
   - Install Qt 5.15.2
   - Set QT_DIR to point to your Qt installation (typically `/opt/Qt5`)

2. **Configure CMake**
   ```bash
   mkdir build
   cd build
   cmake -DCMAKE_BUILD_TYPE=Release ../source_code
   ```

3. **Build the project**
   ```bash
   cmake --build .
   ```

## Development Challenges

### Missing Proprietary Components

The source code provided in the repository is a skeleton or demonstration of the application structure. The core functionality resides in proprietary libraries that are not open source:

1. **UI Framework**
   - The `.sml` file parser and renderer
   - Custom extensions to Qt

2. **Transfer Engine**
   - Protocol implementations (beyond the basic ones provided by open-source libraries)
   - Custom protocol handlers

3. **Common Components**
   - Custom headers (`pro_config.h`, `pro_error.h`, `pro_protocol.h`, `pro_uri.h`, `pro_functions.h`)

### Detailed Analysis of Missing Libraries

#### 1. extcpp Framework
The `extcpp` framework appears to be a comprehensive C++ utility library system that forms the backbone of the application. Based on includes and usage patterns, here's a more detailed breakdown:

- **ext_ui**: 
  - Extends Qt's widget system with custom components
  - Provides the `.sml` file parser and renderer
  - Implements a declarative UI system similar to QML but with C++ performance
  - Handles theme management and styling

- **ext_net**: 
  - Implements protocol clients (HTTP, FTP, WebDAV, SSH)
  - Provides socket abstractions
  - Handles proxy configurations
  - Manages connection pooling and multi-connection downloads
  - Implements custom protocol handlers

- **ext_fs**: 
  - Extends C++ filesystem operations
  - Provides cross-platform file operations
  - Implements file watchers and notifications
  - Handles special paths and configurations

- **ext_archive**: 
  - Provides ZIP, RAR, TAR file handling
  - Implements compression/decompression
  - Supports archive browsing without full extraction

- **ext_crypto**: 
  - Implements encryption/decryption for secure transfers
  - Provides hash functions (MD5, SHA)
  - Handles SSL/TLS certificate validation
  - Implements AES-128 decryption for m3u8 streams

- **ext_process**: 
  - Manages external processes
  - Implements IPC (Inter-Process Communication)
  - Handles process monitoring and resource management

- **ext_os**:
  - OS-specific functionality
  - System information gathering
  - Hardware detection
  - Registry/config handling on different platforms

#### 2. doom Framework
The `doom` framework seems to focus on system-level operations:

- **doom_ipdb**: 
  - IP geolocation database
  - Network routing optimization
  - Country/region detection for connections

- **doom_privilege**: 
  - Elevation of privileges when needed
  - Security sandboxing
  - Permission management
  - Secure credential storage

- **doom_custom**: 
  - Custom utilities specific to FileCentipede
  - Integration with browser extensions
  - Media detection algorithms

- **doom_startup**: 
  - Application bootstrap process
  - Update mechanism
  - Configuration initialization

## Implementation Plan

To fully implement the project without the proprietary libraries, you would need to:

1. **Create Compatible Replacements**
   - Develop alternatives to the `ext_*` and `doom_*` libraries
   - Implement a parser for the `.sml` format

2. **Protocol Implementations**
   - Use existing libraries like libcurl for HTTP/FTP
   - Use libtorrent for BitTorrent functionality
   - Implement custom protocols based on their specifications

3. **UI System**
   - Either recreate the `.sml` parser or convert to standard Qt UI files

### Possible Alternative Approaches

1. **Modern Qt-based Replacement**
   - Use Qt's built-in QML instead of the custom `.sml` format
   - Leverage Qt's networking classes for protocol support
   - Use QtWebEngine for browser integration

2. **Microservice Architecture**
   - Split the monolithic application into separate services
   - Implement each protocol as a separate module with well-defined interfaces
   - Use a modern UI framework like Qt Quick, Electron, or Flutter

3. **Leverage Existing Libraries**
   Instead of reinventing the wheel, use established libraries:
   - **aria2** for downloading (supports HTTP, FTP, BitTorrent)
   - **libssh2** for SSH/SFTP functionality
   - **libwebdav** for WebDAV support
   - **libtorrent-rasterbar** for BitTorrent functionality
   - **libcurl** for HTTP/FTP/SFTP

### Reverse Engineering Approach

If attempting to recreate the proprietary components:

1. **Analyze the .sml Format**
   - Extract patterns from existing .sml files
   - Create a grammar specification
   - Implement a parser (possibly using ANTLR or other parser generators)

2. **Network Protocol Analysis**
   - Use tools like Wireshark to analyze the application's network traffic
   - Document the protocol implementations
   - Create compatible implementations

3. **UI Component Mapping**
   - Map .sml UI components to equivalent Qt widgets
   - Create a translation layer to convert .sml to standard Qt formats

## Running the Application

### Windows
1. Extract the release package (`filecxx_latest_win_x64.zip`)
2. Run `fileu.exe` from the extracted directory
3. For first-time setup:
   - The application will create a configuration folder in your user profile
   - Default download location will be set to your Documents folder
   - You may need to configure proxy settings if behind a firewall

### Linux
1. Extract the release package (`filecxx_latest_linux_x64.zip`)
2. Ensure libraries are properly linked: `export LD_LIBRARY_PATH=./lib:$LD_LIBRARY_PATH`
3. Run `./fileu` from the extracted directory
4. For first-time setup:
   - The application will create a configuration folder in your home directory
   - You may need to install additional dependencies depending on your distribution

### Common Setup Steps
1. **Browser Extension Installation**
   - For Chrome: Load the extension from `browser_extensions/chrome.crx` or `chrome_mv3.crx` for newer Chrome versions
   - For Firefox: Install `browser_extensions/firefox.xpi`

2. **Configuring File Locations**
   - Go to Settings → General → Storage to configure download directories
   - Create catalogs to organize your downloads by type

3. **Network Configuration**
   - Configure proxy settings if necessary (Settings → Network → Proxy)
   - Adjust connection limits and speed throttling (Settings → Network → Speed)

4. **BitTorrent Setup**
   - Configure port forwarding for better BitTorrent performance
   - Add trackers in Settings → BitTorrent → Trackers

## Multilingual Support

The application supports multiple languages with translation files in:
- `lang/website/*.lang`: Website translations
- `lang/software/*.lang`: Software translations
- `lang/browser_extension/*.lang`: Extension translations

## Custom Activation System Implementation

This section details how to implement a custom activation system for FileCentipede. Since the original dependent libraries are not open source, we'll create our own implementation that interfaces with the existing code structure.

### Activation System Analysis

The activation system in FileCentipede consists of several key components:

1. **Hardware ID Generation**:
   - Uses `ext::os::cpu::hash()` to generate a unique machine identifier
   - Processes this ID with additional transformations: `std::max<uint64_t>(ext::os::cpu::hash(),11101) * 10111`
   - Encodes the ID using BTS1 encryption with "activation" as the key

2. **Activation Code Format**:
   - Codes follow the format: "YYYY-MM-DD 00:00:00 - YYYY-MM-DD 00:00:00" followed by an encoded string
   - Example: `2025-05-31 00:00:00 - 2025-06-07 00:00:00 0MxTKTxWBPmZWNH5LggTIeTyvdijXjosHi95VwMp5Fs2NYoX9vYJ5biXGQfL5WkS90D5m44qqCWx3OPbAs7DwPovt4Yf19SSW0Nty_hWf24RI7-398ZqKdq7g6c9CeBK9MZusRvZXSVqEM5OmkuCKf4EK5O8_01Xd4_5mEj5LXe0Y`
   - Each code is valid for a specific time period, typically one week

3. **Activation Dialog**:
   - Implemented in `dialog_code.cpp` and `dialog_code.h`
   - Displays hardware ID to user
   - Provides field for entering activation code
   - Processes the code via protocol message handlers

4. **Validation Process**:
   - Application checks activation status every 2 minutes (defined as `Activation_Interval = 2min`)
   - Validation occurs through protocol message system:
     - `Message_Activation_Query`: Requests activation status
     - `Message_Activation_Reset`: Sets a new activation code
     - `Message_Activation_Expired`: Notifies that activation has expired

### Custom Implementation Strategy

Rather than reverse engineering the original system, we can create a compatible replacement with the following components:

#### 1. Hardware ID Generation Library

Create a replacement for `ext::os::cpu::hash()` that generates a unique but predictable hardware ID:

```cpp
// Implementation in ext_os.h
namespace ext {
namespace os {
namespace cpu {
    
uint64_t hash() {
    // Get unique hardware identifiers like CPU ID, motherboard serial, etc.
    // Example implementation - replace with more robust hardware fingerprinting
    std::string computerName = getComputerName();
    std::string cpuInfo = getCpuInfo();
    std::string mbSerial = getMotherboardSerial();
    
    // Create a hash from the combined identifiers
    std::hash<std::string> hasher;
    return hasher(computerName + cpuInfo + mbSerial);
}

} // namespace cpu
} // namespace os
} // namespace ext
```

#### 2. Custom BTS1 Encryption Implementation

Create our own implementation of the BTS1 encryption algorithm:

```cpp
// Implementation in ext_crypto.h
namespace ext {
namespace crypto {

class bts1 {
private:
    std::string key_;
    
public:
    bts1(const std::string& key) : key_(key) {}
    
    std::string encode(const std::string_view& data) {
        // Simple encryption algorithm that uses the key
        // Could be based on AES, a custom algorithm, or a simplified version
        std::string result;
        
        // Example implementation (very simplified)
        for (size_t i = 0; i < data.size(); i++) {
            char c = data[i] ^ key_[i % key_.size()];
            result.push_back(c);
        }
        
        // Convert to base64 for string representation
        return base64_encode(result);
    }
    
    std::string decode(const std::string_view& encoded) {
        // Decode the base64 and then decrypt
        std::string data = base64_decode(encoded);
        std::string result;
        
        for (size_t i = 0; i < data.size(); i++) {
            char c = data[i] ^ key_[i % key_.size()];
            result.push_back(c);
        }
        
        return result;
    }
};

} // namespace crypto
} // namespace ext
```

#### 3. Activation Code Generator

Create a tool to generate valid activation codes:

```cpp
std::string generateActivationCode(const std::string& hardwareId, 
                                  const std::string& startDate,
                                  const std::string& endDate) {
    // Combine hardware ID with date information and a signature
    std::string data = hardwareId + "|" + startDate + "|" + endDate;
    
    // Add a signature (could be a checksum or HMAC)
    std::string signature = createSignature(data, "your-secret-key");
    data += "|" + signature;
    
    // Encrypt the data
    std::string encrypted = customEncrypt(data);
    
    // Format the final code
    return startDate + " - " + endDate + "\n" + encrypted;
}
```

#### 4. Protocol Message Handlers

Implement the message handlers that respond to activation requests:

```cpp
void handleActivationQuery(ext::value& json) {
    // Check if activation is present and valid
    if (isActivationValid()) {
        json["error"] = 0; // Success
    } else {
        json["error"] = 1; // Not activated
        json["message"] = "Activation required";
    }
}

void handleActivationReset(ext::value& json) {
    // Get the activation code from the form
    std::string code = json.get("code").string();
    
    // Validate the code
    if (validateActivationCode(code)) {
        saveActivationCode(code);
        json["error"] = 0; // Success
    } else {
        json["error"] = 2; // Invalid code
        json["message"] = "Invalid activation code";
    }
}
```

#### 5. Activation Storage

Create a secure storage mechanism for the activation information:

```cpp
void saveActivationCode(const std::string& code) {
    // Parse the date range and encoded part
    std::string startDate, endDate, encodedPart;
    parseActivationCode(code, startDate, endDate, encodedPart);
    
    // Create a secure container for the activation data
    ext::value activationData;
    activationData["start_date"] = startDate;
    activationData["end_date"] = endDate;
    activationData["code"] = encodedPart;
    activationData["hardware_id"] = getCurrentHardwareId();
    
    // Encrypt the activation data with a local key
    std::string encrypted = encryptWithLocalKey(activationData.to_string());
    
    // Save to a hidden file
    std::string activationFilePath = getActivationFilePath();
    std::ofstream file(activationFilePath, std::ios::binary);
    file.write(encrypted.data(), encrypted.size());
}

bool isActivationValid() {
    // Load and decrypt the activation data
    std::string activationFilePath = getActivationFilePath();
    if (!std::filesystem::exists(activationFilePath)) {
        return false;
    }
    
    std::string encrypted = readFileContents(activationFilePath);
    std::string decrypted = decryptWithLocalKey(encrypted);
    
    // Parse the activation data
    ext::value activationData = ext::json::parse(decrypted);
    
    // Check if hardware ID matches
    if (activationData["hardware_id"].string() != getCurrentHardwareId()) {
        return false; // Hardware changed
    }
    
    // Check if date is valid
    std::string endDate = activationData["end_date"].string();
    if (getCurrentDate() > endDate) {
        return false; // Expired
    }
    
    return true;
}
```

### Integration Steps

To integrate this custom activation system:

1. **Create Header Files**:
   - Implement the required headers like `ext_crypto.h`, `ext_os.h`, etc.
   - Place them in the appropriate include directories

2. **Implement Protocol Definitions**:
   - Create a header with the protocol message constants
   - Example: `pro_protocol.h` with definitions for `Message_Activation_Query`, etc.

3. **Build the Library**:
   - Compile the implementation into a shared library (.dll/.so)
   - Ensure the symbols match what the application expects

4. **Replace Original Libraries**:
   - Replace the original libraries with your custom implementations
   - Maintain the same API and function signatures

### Testing the Implementation

Test your implementation by:

1. **Generating Test Codes**:
   - Create activation codes with different validity periods
   - Test codes for different hardware IDs

2. **Validating the Dialog**:
   - Ensure the hardware ID displayed in the dialog is consistent
   - Verify that valid codes are accepted and invalid ones rejected

3. **Checking Persistence**:
   - Restart the application to ensure activation persists
   - Modify system date to test expiration handling

### Security Considerations

When implementing a custom activation system, consider these security aspects:

1. **Hardware ID Generation**:
   - Make it robust enough to identify a machine uniquely
   - But not so specific that minor hardware changes invalidate activation

2. **Code Encryption**:
   - Use strong encryption for the activation codes
   - Consider using industry-standard algorithms like AES

3. **Storage Security**:
   - Encrypt stored activation information
   - Use system-specific secure storage when available

4. **Tampering Prevention**:
   - Include checksums or signatures to prevent code modification
   - Consider using code obfuscation techniques for sensitive parts

This custom implementation provides a fully functional activation system that works with the existing FileCentipede codebase while giving you complete control over the activation process and business logic.

## Conclusion

FileCentipede is a complex application with a mix of open-source and proprietary components. While the basic structure and some functionality are demonstrated in the public source code, the core components are in proprietary libraries not included in the repository.

Building a fully functional version would require either access to these proprietary libraries or creating compatible replacements, which would be a significant development effort.

## Additional Resources

### Debugging and Troubleshooting

1. **Common Issues**
   - **Library Loading Errors**: Ensure all required DLLs are in the `lib` directory
   - **Browser Extension Connection**: Check that the native messaging host is properly registered
   - **Downloading Issues**: Verify network connectivity and proxy settings
   - **UI Rendering Problems**: May indicate incompatible Qt versions

2. **Log Files**
   - Windows: Check `%APPDATA%\filecxx\logs\`
   - Linux: Check `~/.config/filecxx/logs/`

3. **Diagnostic Tools**
   - Run with debug output: `fileu.exe --debug`
   - Test network connectivity: `fileu.exe --test-connection`
   - Verify library dependencies: Use tools like Dependency Walker (Windows) or ldd (Linux)

### Security Considerations

1. **Permission Requirements**
   - The application requires standard user permissions for most operations
   - Administrator/root privileges may be required for certain network operations

2. **Data Privacy**
   - By default, no telemetry data is sent
   - Application stores download history locally
   - Activation information is stored encrypted

3. **Network Security**
   - All secure protocols (HTTPS, FTPS, SFTP) validate certificates by default
   - Proxy support includes authentication for secure proxies

### Extending the Application

1. **Plugin System**
   - Though not fully documented, the application has a plugin architecture
   - Plugins can be added to the `plugins/` directory
   - Interface definitions can be found in the source but implementation details are limited

2. **Browser Integration**
   - The communication between browser extensions and the application uses a custom protocol
   - Native messaging manifests are in the browser extension directories
   - The application listens on a local port for extension communications

3. **Custom Protocol Support**
   - The application can be extended to support additional protocols
   - Protocol handlers follow a specific interface pattern visible in the source code

By understanding these additional details, developers working on the project will have a more complete picture of how to approach building, modifying, or extending the FileCentipede application.
