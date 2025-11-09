# AUTOMATIC-LED-CONTROL-USING-IR-SENSOR
##  AIM
To design and implement a system using the **STM32 microcontroller** where an LED automatically turns ON or OFF based on the input from an **IR sensor**.

---

##  Components Required
- STM32 Nucleo or Discovery Board (e.g., **Nucleo-G071RB**)
- IR Sensor Module
- LED (5mm Green or any color)
- Jumper wires
- Breadboard

---

##  Theory
An **IR sensor** detects the presence of an object by emitting and receiving infrared light.

### IR Sensor Behavior
- When an **object is detected**, the IR sensor output goes **LOW (0V)**.
- When **no object is detected**, the output stays **HIGH (3.3V)**.

### Microcontroller Response
- If **IR output = LOW** → **LED ON**
- If **IR output = HIGH** → **LED OFF**
### **Procedure**

1. Open **STM32CubeIDE**.
<img width="800" height="500" alt="Screenshot 2025-11-03 140814" src="https://github.com/user-attachments/assets/92711a9f-9923-4894-a440-8fefe205167a" />

2. Click **File → New STM32 Project**.
<img width="800" height="500" alt="Screenshot 2025-11-03 141246" src="https://github.com/user-attachments/assets/294a12ee-8574-4f47-92bd-03d151484e2f" />
<img width="800" height="500" alt="Screenshot 2025-11-03 141343" src="https://github.com/user-attachments/assets/19acc4e0-0587-4628-9f27-f161dc51ef24" />

3. Select the **target microcontroller** or board and click **Next**.
<img width="800" height="500" alt="Screenshot 2025-11-04 193237" src="https://github.com/user-attachments/assets/80e9117c-679e-4a60-be09-53256b3bb149" />



4. Name the project.
<img width="800" height="500" alt="Screenshot 2025-11-06 021032" src="https://github.com/user-attachments/assets/517bc441-d87a-49bf-9465-1faa35bc4f8f" />

5. The corresponding `.ioc` file will be generated automatically.
<img width="800" height="500" alt="Screenshot 2025-11-06 021116" src="https://github.com/user-attachments/assets/e15ca5cb-cb83-40d7-9d97-916a67f0aea7" />

6. Configure the pins as **GPIO (Input/Output)**, **USART**, etc. as needed.
<img width="800" height="500" alt="Screenshot 2025-11-06 021116" src="https://github.com/user-attachments/assets/a85c116e-9bc9-42f8-9460-8730851ff7c9" />


7. Save the configuration (`Ctrl + S`) – the base C program will be generated automatically.
<img width="800" height="500" alt="Screenshot 2025-11-06 021116" src="https://github.com/user-attachments/assets/93467e0b-d25c-4a20-90c0-fdbc0fa8d0a1" />
 
8. Edit the generated main program as required.
<img width="800" height="500" alt="Screenshot 2025-11-06 021313" src="https://github.com/user-attachments/assets/ea58d4d4-ba12-4c4e-9a1b-1f29b07afac8" />


9. Click **Project → Build All**.
<img width="800" height="500" alt="Screenshot 2025-11-06 021439" src="https://github.com/user-attachments/assets/512fd5d2-f35a-4f90-aa63-04fa78a77d4f" />

10. Link the **HEX file** using the post-build process.
<img width="800" height="500" alt="Screenshot 2025-11-06 021525" src="https://github.com/user-attachments/assets/4a9f6c67-7a29-4a19-97d7-dde53ab12013" />

11. Click **Debug** and connect the **STM Nucleo Board**.
<img width="800" height="500" alt="Screenshot 2025-11-06 021621" src="https://github.com/user-attachments/assets/853d1f92-76d0-405b-bcf3-968ca6191204" />

13. Click **Run** to execute the program.
    
---

### 💻 **Program**


```c
#include "main.h"

void SystemClock_Config(void);
static void MX_GPIO_Init(void);

int main(void)
{
    HAL_Init();
    SystemClock_Config();
    MX_GPIO_Init();

    while (1)
    {
        GPIO_PinState ir = HAL_GPIO_ReadPin(GPIOA, GPIO_PIN_10); // IR OUT at PA10 (D2)

	      if (ir == GPIO_PIN_RESET)  // IR sensor HIGH = object detected
	      {
	          HAL_GPIO_WritePin(GPIOB, GPIO_PIN_3, GPIO_PIN_SET); // Turn ON LED
	      }
	      else
	      {
	          HAL_GPIO_WritePin(GPIOB, GPIO_PIN_3, GPIO_PIN_RESET); // Turn OFF LED
	      }

	      HAL_Delay(100);
    }
}
```
---
### OUTPUT
CASE 1: LED ON 

![on](https://github.com/user-attachments/assets/5ec9b77a-f3ac-45d3-bc3f-54cc0166c517)

CASE 2: LED OFF

![off](https://github.com/user-attachments/assets/814e9071-d69a-4006-9f91-640802f67b27)

---
### RESULT

The experiment on IR Sensor-Based Automatic LED Control using STM32 was successfully carried out. The STM32 microcontroller accurately read the IR sensor output and controlled the LED based on object detection. When an object was detected, the LED glowed (ON) and when no object was present, the LED remained OFF. Thus, the objective of the experiment was achieved.




