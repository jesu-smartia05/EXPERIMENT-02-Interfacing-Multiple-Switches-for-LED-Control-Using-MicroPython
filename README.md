# EXPERIMENT-02-Interfacing-Multiple-Switches-for-LED-Control-Using-MicroPython


 
## NAME: Jesu Smartia A

## DEPARTMENT: B.E.CSE(IoT)

## ROLL NO: 212223110016

## DATE OF EXPERIMENT: 11.02.2026

## AIM

To interface multiple switches with the Raspberry Pi Pico and control LEDs using MicroPython.

## APPARATUS REQUIRED

Raspberry Pi Pico

2 Push Button Switches

2 LEDs (Light Emitting Diodes)

330Ω Resistors

Breadboard

Jumper Wires

USB Cable

## THEORY



FIGURE-01: RASPBERRY PI PICO PINOUT DIAGRAM

Raspberry Pi Pico is a microcontroller board based on the RP2040 chip. It supports MicroPython, making it suitable for IoT and embedded applications. The Raspberry Pi Pico is a compact microcontroller board featuring a 40-pin layout, including power, ground, GPIO, and communication interface pins. It operates with a dual-core ARM Cortex-M0+ processor and supports MicroPython and C/C++ programming.

The power pins include VBUS (5V from USB), VSYS (1.8V to 5.5V input), 3V3(OUT) (regulated 3.3V output), and multiple ground (GND) connections. The board offers 26 multi-purpose GPIO pins (GP0 to GP28), which can be used for digital input, output, PWM, and communication interfaces such as I2C, SPI, and UART. It also features three analog-to-digital converter (ADC) pins (GP26, GP27, GP28), used for reading analog sensor values, along with an ADC_VREF pin to set the reference voltage.

For communication, I2C (SDA, SCL), SPI (MOSI, MISO, SCK), and UART (TX, RX) interfaces are mapped across different GPIO pins, allowing seamless connectivity with sensors and peripherals. All GPIO pins support PWM (Pulse Width Modulation), making it useful for motor control, LED brightness adjustment, and sound applications. The BOOTSEL button enables USB mass storage mode for firmware flashing, while the DEBUG pins (SWD interface) provide debugging capabilities. With its low power consumption, flexible GPIO options, and rich interface support, the Raspberry Pi Pico is widely used for IoT, embedded systems, robotics, and automation projects.

WORKING PRINCIPLE

The switches are connected as inputs to GPIO pins of the Pico.

The LEDs are connected as outputs.

A MicroPython script reads the switch states and controls the LEDs accordingly.

### CIRCUIT DIAGRAM
<img width="878" height="493" alt="Screenshot 2026-02-11 112024" src="https://github.com/user-attachments/assets/6cb3e235-a40f-4bfa-b0e3-ae070018d046" />
   
Figure-01 circuit diagram of digital input interface 

Connect switch 1 to GP2 and switch 2 to GP3.

Connect LED 1 to GP14 via a 330Ω resistor.

Connect LED 2 to GP17 via a 330Ω resistor.

Connect the other terminals of the switches to GND.

## PROGRAM (MicroPython)
### EXPERIMENT 2A
```
from machine import Pin
from time import sleep

print("Welcome Pi Pico")

# Switches with internal pull-ups
switch1 = Pin(2, Pin.IN, Pin.PULL_UP)
switch2 = Pin(3, Pin.IN, Pin.PULL_UP)

# LEDs
led1 = Pin(15, Pin.OUT)
led2 = Pin(16, Pin.OUT)

while True:
    sw1_state = switch1.value()  # 0 when pressed, 1 when released
    sw2_state = switch2.value()
    
    print("Switch 1 state:", sw1_state)
    print("Switch 2 state:", sw2_state)
    
    # Turn off LEDs by default
    led1.value(0)
    led2.value(0)
    
    if sw1_state == 1 and sw2_state == 1:
        # Both pressed -> both LEDs off
        led1.value(0)
        led2.value(0)
    elif sw1_state == 1:
        # Only switch1 pressed -> blink led1
        led1.value(0)
        sleep(0.5)
        led1.value(1)
    elif sw2_state == 1:
        # Only switch2 pressed -> blink led2
        led2.value(0)
        sleep(0.5)
        led2.value(1)
    
    sleep(0.1)
```
### EXPERIMENT 2B
```
from machine import Pin
import time
print("Pi Pico")
led1 = Pin(0, Pin.OUT)
led2 = Pin(3, Pin.OUT)
led3 = Pin(6, Pin.OUT)
buzzer=Pin(15,Pin.OUT)
while True:
    led1.value(1) 
    print("LED is ON")
    time.sleep(1) 
    led1.value(0)  
    print("LED is OFF")
    time.sleep(1)
    led2.value(1) 
    print("LED is ON")
    time.sleep(1) 
    led2.value(0)  
    print("LED is OFF")
    time.sleep(1)
    led3.value(1) 
    print("LED is ON")
    time.sleep(1) 
    led3.value(0)  
    print("LED is OFF")
    time.sleep(1)
    buzzer.value(1) 
    print("Buzzer is ON")
    time.sleep(1) 
    buzzer.value(0)  
    print("Buzzer is OFF")
    time.sleep(1)
```

## OUTPUT
### EXPERIMENT 2A

<img width="896" height="721" alt="Screenshot 2026-02-11 111507" src="https://github.com/user-attachments/assets/b6c4659f-d26f-4147-ab75-28393c2bb855" />

<img width="874" height="669" alt="Screenshot 2026-02-11 111726" src="https://github.com/user-attachments/assets/7bf8e37e-7a92-4a64-902d-9e25e2e29d9e" />

<img width="907" height="722" alt="Screenshot 2026-02-11 111803" src="https://github.com/user-attachments/assets/ab9519ee-211f-4d54-ad00-34f97d3c99aa" />

<img width="878" height="626" alt="Screenshot 2026-02-11 112024" src="https://github.com/user-attachments/assets/7273a324-b28e-433f-a9b7-6dc6c4a9dffa" />

### EXPERIMENT 2B
<img width="907" height="607" alt="Screenshot 2026-02-11 113806" src="https://github.com/user-attachments/assets/e9a88af0-b624-4cb2-9ebb-dbd2080cb151" />

<img width="915" height="611" alt="Screenshot 2026-02-11 113829" src="https://github.com/user-attachments/assets/c2a0559e-44ec-4b4d-9b96-f9977403fe3f" />

<img width="924" height="662" alt="Screenshot 2026-02-11 113840" src="https://github.com/user-attachments/assets/58254c48-0541-475f-844a-326121d427e5" />

<img width="915" height="664" alt="Screenshot 2026-02-11 114046" src="https://github.com/user-attachments/assets/5ea61791-8387-4dc7-92ad-cf2c06a8b63a" />

## RESULTS

The multiple switches connected to the Raspberry Pi Pico successfully controlled the LEDs based on their states, confirming the proper interfacing of digital inputs and outputs.
