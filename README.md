# Run-FreeRTOS-on-Arduino-UNO

## Step 1 : Install the ArduinoFreeRTOS library
- Go to **"Tools -> Manage Libraries"** in Arduino IDE
- Search for "FreeRTOS" and install the library

![image](https://user-images.githubusercontent.com/31447839/128365882-dc74b237-5537-4b0c-af5d-1697412c4491.png)

## Step 2 : Include ArduinoFreeRTOS header file and define the tasks
```c
#include <Arduino_FreeRTOS.h>

// define two tasks for Blink & AnalogRead
void TaskBlink( void *pvParameters );
void TaskSerialPrint( void *pvParameters );
```
Here the tasks are to blink the LED and print some logs to the SerialMonitor.
```c
void TaskBlink(void *pvParameters)  // This is a task.
{
  (void) pvParameters;

  // initialize digital pin 13 as an output.
  pinMode(13, OUTPUT);

  for (;;) // A Task shall never return or exit.
  {
    digitalWrite(13, HIGH);   // turn the LED on (HIGH is the voltage level)
    vTaskDelay( 3000 / portTICK_PERIOD_MS ); // wait for one second
    digitalWrite(13, LOW);    // turn the LED off by making the voltage LOW
    vTaskDelay( 2000 / portTICK_PERIOD_MS ); // wait for one second
  }
}

void TaskSerialPrint(void *pvParameters)  // This is a task.
{
  (void) pvParameters;

  // initialize serial communication at 9600 bits per second:
  Serial.begin(9600);

  for (;;)
  {
    Serial.println("TaskSerialPrint");
    vTaskDelay(1);  // one tick delay (15ms) in between reads for stability
  }
}
```
## Step 3: Flash the code into the Arduino
After flashing the code, you can see that the LED is blinking and in parallel the logs are print in the Serial Monitor

## References
[https://create.arduino.cc/projecthub/feilipu/using-freertos-multi-tasking-in-arduino-ebc3cc](https://create.arduino.cc/projecthub/feilipu/using-freertos-multi-tasking-in-arduino-ebc3cc)
