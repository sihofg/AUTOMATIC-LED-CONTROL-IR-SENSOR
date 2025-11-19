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
   <img width="2880" height="1743" alt="Screenshot 2025-11-04 223247" src="https://github.com/user-attachments/assets/a4579d8a-a137-4150-a4f9-ebc60f390587" />

2. Click **File → New STM32 Project**.
    <img width="1920" height="1200" alt="Screenshot 2025-11-06 135034" src="https://github.com/user-attachments/assets/aa104ee2-f24a-47ab-8da9-8c013defcc5a" />
	
3. Select the **target microcontroller** or board and click **Next**.
  <img width="1920" height="1200" alt="Screenshot 2025-11-06 133821" src="https://github.com/user-attachments/assets/1d2aee7b-d59f-48b2-8735-05c7c953f5a4" />


4. Name the project.
   <img width="1920" height="1200" alt="Screenshot 2025-11-06 133856" src="https://github.com/user-attachments/assets/e33e5ea7-b143-40a0-8f3c-f1237d87d7d3" />
   
5. The corresponding `.ioc` file will be generated automatically.
   <img width="1920" height="1200" alt="Screenshot 2025-11-06 132025" src="https://github.com/user-attachments/assets/1d355695-5192-4bec-85c5-06ea8752de9b" />


6. Configure the pins as **GPIO (Input/Output)**, **USART**, etc. as needed.
   <img width="1920" height="1200" alt="Screenshot 2025-11-06 132135" src="https://github.com/user-attachments/assets/cc66ed23-9970-4bf5-9326-4c1467478802" />

7. Save the configuration (`Ctrl + S`) – the base C program will be generated automatically.
   <img width="1920" height="1200" alt="Screenshot 2025-11-06 131510" src="https://github.com/user-attachments/assets/97ba8c25-42b6-4fbf-937c-8a3aeef2e6ed" />

 
8. Edit the generated main program as required.
   <img width="1920" height="1200" alt="Screenshot 2025-11-06 131739" src="https://github.com/user-attachments/assets/234f145b-0d33-4f48-83c8-188ece937461" />
  
   
9. Click **Project → Build All**.
    <img width="1920" height="1200" alt="Screenshot 2025-11-06 132843" src="https://github.com/user-attachments/assets/b69192de-f23d-41ed-8e5c-ca786495addf" />


10. Link the **HEX file** using the post-build process.
   <img width="1920" height="1200" alt="Screenshot 2025-11-06 132843" src="https://github.com/user-attachments/assets/c5ea9e43-0fd5-4a88-a7e6-395c00f7a8b5" />


11. Click **Debug** and connect the **STM Nucleo Board**.
   <img width="1920" height="1200" alt="Screenshot 2025-11-06 132930" src="https://github.com/user-attachments/assets/aab4c84a-f8f2-4f90-878f-59f43b1c21a4" />

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
	![WhatsApp Image 2025-11-05 at 19 24 50_b76f736e](https://github.com/user-attachments/assets/19de543b-4d9e-43f0-80bd-da715bb5c4a3)

CASE 2: LED OFF
	![WhatsApp Image 2025-11-05 at 19 24 37_8bf0d766](https://github.com/user-attachments/assets/3c686f91-6327-42a2-9a66-7d355078d963)

---
### RESULT

The experiment on IR Sensor-Based Automatic LED Control using STM32 was successfully carried out. The STM32 microcontroller accurately read the IR sensor output and controlled the LED based on object detection. When an object was detected, the LED glowed (ON) and when no object was present, the LED remained OFF. Thus, the objective of the experiment was achieved.



