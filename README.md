# Wacli for Windows 🪟

This is a Windows-compatible fork of the original **[wacli](https://github.com/steipete/wacli)** by [steipete](https://github.com/steipete). 

## 🚀 The Achievement
The original `wacli` is a powerful CLI tool for WhatsApp automation, but it was previously incompatible with Windows due to its reliance on Unix-specific system calls for file locking. **I, Yasir Amin Brohi, modified the core locking mechanism to support the Windows API**, allowing developers on Windows to finally use this robust tool natively.

## 🛠️ The Problem
The original code used `syscall.Flock`, which is not available in the Windows environment. This caused the build to fail with `undefined: syscall.Flock` errors, preventing Windows users from compiling or running the tool.

## 💡 The Solution
I refactored the `internal/lock/lock.go` file to:
1.  Detect the operating system at runtime.
2.  Use `golang.org/x/sys/windows` and the `LockFileEx` / `UnlockFileEx` API for Windows environments.
3.  Maintain backward compatibility for Unix-based systems using the original `syscall.Flock`.

## 📂 Files Changed
*   **`internal/lock/lock.go`**: Completely rewritten to handle cross-platform file locking.
*   **`go.mod`**: Added `golang.org/x/sys` dependency to support Windows API calls.

## 📋 How to Build
1.  Ensure you have **Go (1.25+)** installed.
2.  Clone this repository:
    ```bash
    git clone https://github.com/YasirAminBrohi/wacli_window.git
    cd wacli_window
    ```
3.  Build the executable:
    ```bash
    go build -o wacli.exe ./cmd/wacli
    ```

## 🔐 Authentication
Run `./wacli.exe auth` to link your WhatsApp account via QR code. Your session will be securely stored in your user directory (`%USERPROFILE%\.wacli`).

## 🙏 Credits
*   Original Project: [steipete/wacli](https://github.com/steipete/wacli)
*   Windows Port & Fixes: **Yasir Amin Brohi**

---
*Built with passion by a BSCS student at FAST Karachi.* 💻🇵🇰
