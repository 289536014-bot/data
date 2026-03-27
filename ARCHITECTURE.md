# Disk Recovery Tool - Architecture

## Overview
This is a professional-grade disk recovery system with a layered architecture:
- **Frontend**: C# WPF/WinUI for user interface
- **Backend**: Rust DLL for low-level disk operations and file recovery

## Project Structure

```
project/
├── frontend/              # C# WPF Application
│   ├── DiskRecoveryUI.csproj
│   ├── MainWindow.xaml
│   ├── MainWindow.xaml.cs
│   ├── App.xaml
│   └── App.xaml.cs
├── backend/               # Rust Recovery Engine
│   ├── Cargo.toml
│   └── src/
│       ├── lib.rs              # FFI exports
│       ├── disk_scanner.rs     # Sector-level disk scanning
│       ├── file_system.rs      # ext4/NTFS parsing
│       └── recovery_engine.rs  # Core recovery logic
└── README.md
``` 

## How It Works

### Frontend (C# WPF)
1. User selects drive and clicks "Start Scan"
2. Calls Rust DLL functions via P/Invoke
3. Receives progress updates via callback
4. Displays recovered files in DataGrid
5. User selects files for recovery

### Backend (Rust)
1. **Disk Scanner**: Reads disk sectors sequentially
2. **Filesystem Parser**: Detects and parses NTFS/ext4 structures
3. **Recovery Engine**: Identifies deleted files and reconstructs them
4. **FFI Interface**: Exports C functions for C# interop

## Key Features

- ✅ Multi-filesystem support (NTFS, ext4, FAT32)
- ✅ Deleted file detection and recovery
- ✅ Real-time progress tracking
- ✅ Native performance via Rust backend
- ✅ Cross-platform capable

## Compilation

### Rust Backend
```bash
cd backend
cargo build --release
# Output: target/release/disk_recovery_engine.dll (Windows)
```

### C# Frontend
```bash
cd frontend
dotnet restore
dotnet build
```

## API Reference

### Exported Functions

#### `init_recovery_engine() -> *mut RecoveryEngine`
Initializes a new recovery engine instance.

#### `scan_disk(engine, drive, callback) -> bool`
Scans disk for deleted files.
- `engine`: Engine pointer
- `drive`: Drive letter (e.g., "C:")
- `callback`: Progress callback function

#### `get_recovered_files(engine) -> *const c_char`
Returns JSON array of recovered files.

#### `recover_file(engine, file_id, output_path) -> bool`
Recovers a specific file.

#### `free_engine(engine) -> void`
Frees engine resources.