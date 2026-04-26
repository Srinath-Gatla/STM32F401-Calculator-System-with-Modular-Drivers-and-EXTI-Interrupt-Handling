# 📟 STM32F401 Calculator using LCD & Keypad

This project implements a **basic calculator** using the **STM32F401 microcontroller**, a **16x2 LCD**, and a **4x4 matrix keypad**. It supports standard arithmetic operations along with a **hardware interrupt-based backspace feature**.

---

## 🚀 Features

- ➕ Basic arithmetic operations:
  - Addition (`+`)
  - Subtraction (`-`)
  - Multiplication (`*`)
  - Division (`/`)
- 🔢 Multi-digit number input
- 🧮 Real-time display on LCD
- ⌫ Backspace using external interrupt (PA0)
- 🧹 Clear function (`c` key)
- ⚠️ Division-by-zero error handling

---

## 🛠️ Hardware Requirements

- STM32F401 Microcontroller
- 16x2 LCD (8-bit mode)
- 4x4 Matrix Keypad
- Push Button (for backspace interrupt)
- Jumper wires

---

## 🔌 Pin Configuration

### 📺 LCD Connections

| LCD Pin | STM32 Pin |
|--------|----------|
| D0–D7  | PB0–PB7  |
| RS     | PC1      |
| RW     | PC2      |
| EN     | PC0      |

---

### ⌨️ Keypad Connections

| Keypad | STM32 Pin |
|--------|----------|
| Rows   | PC3, PC4, PC5, PC6 |
| Columns| PC7, PC8, PC9, PC10 |

---

### 🔘 Backspace Button

| Function   | STM32 Pin |
|-----------|----------|
| Backspace | PA0 (EXTI0 Interrupt) |

---

## 🧠 Project Structure
├── main.c
├── STM32F401_GPIO.h / .c
├── STM32F401_LCD.h / .c
├── STM32F401_KEYPAD.h / .c


---

## ⚙️ How It Works

### 🔢 Input Handling

- Keypad scans rows and columns to detect key presses.
- Numbers are accumulated into:
  - `num1` (before operator)
  - `num2` (after operator)

---

### ➗ Operation Execution

- When `=` is pressed:
  - Operation is performed based on selected operator.
  - Result is displayed on LCD.
  - Result is reused as `num1` for chaining operations.

---

### ⌫ Backspace (Interrupt-Based)

- Triggered using **PA0 (EXTI Line 0)**.
- Removes last digit/operator:
- Updates LCD cursor
- Updates internal variables (`num1`, `num2`, `op`)

---

### 🧹 Clear Function

- Press `c` on keypad:
- Clears LCD
- Resets all variables

---

## 🔄 Keypad Layout

| 7 | 8 | 9 | / |
|---|---|---|---|
| 4 | 5 | 6 | * |
| 1 | 2 | 3 | - |
| c | 0 | = | + |


---

## ⚠️ Error Handling

- Division by zero displays:

- System resets automatically after error.

---

## 🧩 Key Modules

### 📟 LCD Driver

Functions:
- `InitLCD()`
- `CmdLCD()`
- `CharLCD()`
- `StrLCD()`
- `NumLCD()`
- `FloatLCD()`

---

### ⌨️ Keypad Driver

Functions:
- `InitKeypad()`
- `Press_Key()`

---

### 🔔 Interrupt Handling

External interrupt on **PA0**:

```c
void EXTI0_IRQHandler(void)
{
  GPIO_IRQHandle(0);
  backspace_flag = 1;
}
```
---
🏗️ Build & Flash
Open project in STM32CubeIDE / Keil / any ARM IDE
Compile the code
Flash to STM32F401 board
Power up and test using keypad
---

📌 Future Improvements
Floating-point calculation support
Negative number handling
Operator precedence (e.g., 2+3*4)
Timer-based debouncing
LCD cursor enhancements

---

👨‍💻 Author
SD (Self-driven Embedded Developer)
Focused on Embedded Systems and Drone Development

📄 License

This project is open-source and free to use for learning and development purposes.
