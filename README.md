## InterruptHandler

### Overview

**InterruptHandler** is a real-time embedded project developed using the **STM32F401VE** microcontroller. It demonstrates the practical use of **external interrupts (EXTI)** to control a 3-digit 7-segment display and an LED in response to hardware events triggered by push buttons. Designed for both simulation (Proteus) and real hardware deployment, the project encapsulates low-level embedded programming principles including:

- Interrupt-driven input handling
- Safe critical section management
- Efficient display multiplexing
- Modular C driver development

![InterruptHandler System Overview](https://github.com/user-attachments/assets/71f2e2ad-f7e6-4b17-839e-11ace7bb7ff3)

---

### Features

- Custom EXTI driver with support for rising, falling, and both edge triggers
- Three-button interface: Increment, Decrement, and Toggle LED
-  3-digit multiplexed 7-segment display
- Real-time counter updates based on EXTI ISR
- Race condition protection via critical sections (`__disable_irq()`)
- Proteus simulation and hardware-ready logic

---

### Demo Video

[Watch the full demo](https://github.com/user-attachments/assets/4482cfc3-b778-4457-8908-76c10578a72c)

---

### Functional Summary

#### Button Functions:
- **PA4**: Increment counter on **falling edge**
- **PB10**: Decrement counter on **rising edge**
- **PB11**: Toggle LED (PA3) on **rising** and **falling edge**

#### Output:
- **PA3**: LED indicator
- **PB7, PB8, PB9**: Enable control for 3-digit 7-segment display

#### Display:
- Displays decimal count (0–999)
- Shows real-time changes using multiplexing

#### Safety:
- Shared variables are updated inside ISRs and safely accessed in `main()` using `__disable_irq()` / `__enable_irq()` guards

---

### Project Structure

```plaintext
Simulation/
├── InterruptHandler.pdsprj                # Proteus simulation project

stm32f4-task5/
├── cmake/                                 # CMake build system files
│   ├── ArmToolchain.cmake
│   ├── Device.cmake
│   ├── IncludeList.cmake
│   └── SourceList.cmake
├── EXTI/                                  # External interrupt driver
├── Gpio/                                  # GPIO abstraction layer
├── include/                               # Header includes
├── Keypad/                                # (unused)
├── Lib/                                   # Utility code
├── Rcc/                                   # RCC driver for clock config
├── SevenSegment/                          # Display driver
├── src/
│   └── main.c                             # Main logic and ISRs
├── STM32-base/
├── STM32-base-STM32Cube/
├── CMakeLists.txt
└── README.md
```

---

### How to Build & Run

1. **Set ARM Toolchain Path:**  
   Edit `cmake/ArmToolchain.cmake`:
   ```
   set(ARM_TOOLCHAIN_DIR "<Your Path to ARM Toolchain>")
   ```

2. **Build:**  
   Use `CLion` or `STM32CubeIDE` with CMake support to compile the project.

3. **Simulate:**  
   Load the `.hex` output into **Proteus** using `InterruptHandler.pdsprj`.

---

### Team

<div>
  <table align="center">
    <tr>
      <td align="center">
        <a href="https://github.com/YassienTawfikk" target="_blank">
          <img src="https://avatars.githubusercontent.com/u/126521373?v=4" width="150px;" alt="Yassien Tawfik"/><br/>
          <sub><b>Yassien Tawfik</b></sub>
        </a>
      </td>
      <td align="center">
        <a href="https://github.com/malak-emad" target="_blank">
          <img src="https://avatars.githubusercontent.com/u/126415070?v=4" width="150px;" alt="Malak Emad"/><br/>
          <sub><b>Malak Emad</b></sub>
        </a>
      </td>
    </tr>
  </table>
</div>
