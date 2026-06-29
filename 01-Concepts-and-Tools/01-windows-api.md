# Windows API

> **Prerequisites**
>
> - Basic C Programming
> - User Mode vs Kernel Mode
> - Windows Architecture (Recommended)

---

# What is the Windows API?

The **Windows API (Application Programming Interface)** is the primary programming interface that enables user-mode applications to communicate with the Windows operating system.

Instead of directly interacting with hardware or the Windows kernel, applications request operating system services by calling Windows API functions.

These APIs expose operating system functionality such as:

- File management
- Process creation
- Thread management
- Memory allocation
- Registry access
- Networking
- Security
- Graphical User Interface (GUI)

Almost every Windows application, from Notepad to Microsoft Word, uses the Windows API.

---

# Why does the Windows API exist?

Modern operating systems isolate applications from hardware and kernel memory.

Imagine if every application could directly:

- Read physical memory
- Write to disk sectors
- Modify kernel memory
- Access another process

The operating system would become unstable and insecure.

Instead, Windows provides a controlled interface.

![[Pasted image 20260629171822.png]]

Whenever an application needs the operating system to perform an action, it requests that service through the Windows API.

Examples include:

| Task | Windows API |
|------|-------------|
| Create a file | CreateFile() |
| Read a file | ReadFile() |
| Allocate memory | VirtualAlloc() |
| Create a process | CreateProcess() |
| Open Registry | RegOpenKeyEx() |
| Load DLL | LoadLibrary() |

---

# Evolution of Windows APIs

The Windows API has evolved significantly over time.

## 1. Win32 API

The original Windows API mainly consisted of thousands of standalone C functions.

Example:

```c
CreateFile()
CreateProcess()
VirtualAlloc()
CloseHandle()
```

C was chosen because:

- Windows itself was written largely in C.
- C allowed low-level access to operating system services.
- Many programming languages could call C functions.

However, as Windows grew larger, several problems appeared:

- Huge number of APIs
- Inconsistent naming
- Difficult organization
- Poor component reuse

Microsoft needed a better software architecture.

This led to COM.

---

## 2. Component Object Model (COM)

COM (Component Object Model) introduced reusable software components.

Instead of exposing only functions, Windows began exposing objects through interfaces.

Example:

```
Application

      │

      ▼

 Interface

      │

      ▼

 COM Object
```

Originally COM was created to support communication between Microsoft Office applications.

For example:

```
Microsoft Word

      │

      ▼

 Embedded Excel Spreadsheet
```

This capability became known as **OLE (Object Linking and Embedding).**

OLE originally relied on **Dynamic Data Exchange (DDE)**.

DDE had several limitations:

- Slow
- Difficult to maintain
- Limited scalability

Microsoft replaced DDE with COM.

---

### Two Core Principles of COM

#### Interface-Based Communication

Applications communicate through interfaces instead of directly accessing objects.

An interface exposes only the methods an object supports.

Internally these methods are stored inside a Virtual Method Table (vtable).

Benefits:

- Binary compatibility
- Language independence
- Easy extensibility

---

#### Dynamic Loading

Instead of linking everything during compilation, COM components are loaded when needed.

A COM server is usually:

- DLL
- EXE

This allows software components to be updated independently.

---

## 3. Windows Runtime (WinRT)

Windows 8 introduced Windows Runtime.

WinRT was designed primarily for Universal Windows Platform (UWP) applications.

Applications built with WinRT can target:

- Desktop
- Laptop
- Tablet
- Xbox
- HoloLens
- IoT Devices

An important point:

**WinRT is built on top of COM.**

```
 Application

     │

     ▼

Windows Runtime

     │

     ▼

    COM

     │

     ▼

  Windows
```

Desktop applications can still use many WinRT APIs.

Likewise, UWP applications can access selected Win32 APIs.

---

## 4. .NET Framework

The .NET Framework is Microsoft's managed application platform.

It consists of two major components.

### Common Language Runtime (CLR)

The CLR provides:

- Just-In-Time Compilation (JIT)
- Garbage Collection (GC)
- Memory Management
- Exception Handling
- Security

---

### Framework Class Library (FCL)

The FCL contains reusable libraries for:

- Networking
- Collections
- User Interfaces
- Databases
- Cryptography
- XML
- File I/O

Applications written in C#, VB.NET, or F# ultimately interact with Windows through the underlying Windows APIs.

---

# Key Takeaways

- Windows API is the primary interface between applications and Windows.
- Applications never directly interact with hardware.
- Early Windows APIs were mostly standalone C functions.
- COM introduced reusable software components.
- WinRT is built on top of COM.
- .NET applications eventually rely on Windows APIs.