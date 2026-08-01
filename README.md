# Bare-Metal RTOS (Cooperative Task Scheduler)

## 📌 Overview

This project implements a lightweight **Bare-Metal Real-Time Operating System (RTOS)** for the **STM32F446RE** microcontroller, built entirely from scratch in **C** without using the STM32 HAL, CMSIS, or any external RTOS libraries.

The scheduler uses a **cooperative round-robin scheduling algorithm** to manage multiple tasks, while the **SysTick timer** provides millisecond timing for task execution and delays. The project demonstrates fundamental RTOS concepts, embedded systems programming, GPIO interfacing, and direct register-level hardware control.

---

## 🚀 Features

- **Bare-Metal Development**
  - Direct register-level programming without HAL or CMSIS.
  - Complete control over STM32 peripherals.

- **Cooperative Task Scheduler**
  - Round-robin scheduling for multiple concurrent tasks.
  - Lightweight scheduler with minimal overhead.

- **SysTick-Based Timing**
  - 1 ms system tick using the Cortex-M SysTick timer.
  - Non-blocking task delay management.

- **LCD1602 Display Interface**
  - 4-bit communication mode.
  - Displays task execution and system status.

- **GPIO Button Handling**
  - Detects user input using GPIO.
  - Implements software debouncing for reliable button presses.

- **GDB Debugging**
  - Debugged using GDB to verify scheduler behavior and task execution.

---

## 🏗️ Project Structure

```text
STM32-BareMetal-RTOS/
├── Inc/
│   ├── scheduler.h
│   ├── systick.h
│   ├── gpio.h
│   ├── lcd.h
│   └── task.h
├── Src/
│   ├── main.c
│   ├── scheduler.c
│   ├── systick.c
│   ├── gpio.c
│   ├── lcd.c
│   └── task.c
├── startup/
├── linker/
├── Makefile
└── README.md
```

---

## ⚙️ Core Components

### Scheduler

- Implements cooperative round-robin scheduling.
- Executes tasks marked as ready.
- Supports delay-based task execution.

### SysTick Timer

- Generates a 1 ms system tick.
- Maintains a global time counter.
- Updates task delays and readiness.

### LCD Driver

- Interfaces with a 16×2 LCD using a 4-bit GPIO interface.
- Displays scheduler activity and task messages.

### GPIO Driver

- Configures STM32 GPIO peripherals.
- Handles LED output and push-button input.

---

## 📋 Implemented Tasks

| Task | Description | Interval |
|------|-------------|----------|
| `task_blink()` | Displays **"Blinking..."** on the LCD | 1000 ms |
| `task_heartbeat()` | Displays **"Task 2 is Alive"** | 2000 ms |
| `task_button_check()` | Detects button press on **PA9** using software debounce | 50 ms |

---

## 🧱 System Architecture

The scheduler follows a cooperative execution model:

1. `SysTick_Handler()` generates a system tick every millisecond.
2. A global tick counter is incremented.
3. Task delays are updated.
4. Tasks whose delay reaches zero are marked as **READY**.
5. The scheduler executes ready tasks sequentially.
6. Each task schedules its next execution before returning control.

---

## 🛠️ Hardware Requirements

- STM32F446RE Nucleo Board
- LCD1602 (16×2 Character LCD)
- Push Button
- ST-Link Programmer
- USB Cable

---

## 🧰 Tools Used

- C
- ARM GCC Toolchain
- GNU Make
- GDB
- OpenOCD / ST-Link
- Git

---

## ▶️ Getting Started



### Build

```bash
make
```

### Flash the Firmware

Flash the generated binary using:

- ST-Link
- OpenOCD
- STM32CubeProgrammer

### Hardware Connections

| Component | GPIO Pins |
|-----------|-----------|
| LCD Data | PA5 – PA8 |
| LCD Control | PA0, PA1, PA10 |
| Push Button | PA9 |

---

## 🧠 Key Concepts Covered

- Bare-Metal Embedded Programming
- Cooperative Multitasking
- Round-Robin Scheduling
- Cortex-M SysTick Timer
- GPIO Programming
- LCD Interfacing
- Register-Level Peripheral Programming
- Software Debouncing
- Embedded Systems Debugging

---