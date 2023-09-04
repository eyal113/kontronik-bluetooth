| Supported Targets | ESP32 |
| ----------------- | ----- |

# KONTRONIK Bluetooth Module

![image](images/Kontronik_Bluetooth_Modul.jpg)

The Kontronik ESCs (Kosmik and Jive pro) are utilizing a full duplex 8 bit 115200 1 stop bit no parity 3.3v UART communication.
The original Kontronik module is built on top of Blue Radios [BR-LE4.0-D2A](https://www.blueradios.com/hardware_LE4.0-D2.htm) bluetooth module. The ESC uses the built in module AT commands to check the presens of the bluetooth module.
Once the module reply to those commands the ESC starts sending data and telemetry.

On the boot phase, the ESC sends 3 AT commands and wait for response from the module.
* +++\n
* AT\r
* ATSN?


## How to use
TBD

### Hardware Required

The code can be run on any development board, that is based on the Espressif ESP32 SoC with classic Bluetooth capabilities. The board can be connected to a computer with a single USB cable for flashing and monitoring.
In my case I choosed the ESP32 D1 mini board as this was the smallest option.

![image](images/esp32-d1-board.png)


### Setup the Hardware

Connect the Kontronik serial interface to the board as follows.

```
  -----------------------------------------------------------------------------------------
  | ESP32 chip Interface  | Kconfig Option     | Default ESP Pin      | External UART Pin |
  | ----------------------|--------------------|----------------------|--------------------
  | Transmit Data (TxD)   | KONTRONIK_UART_TXD | GPIO16               | RxD               |
  | Receive Data (RxD)    | KONTRONIK_UART_RXD | GPIO17               | TxD               |
  | Ground                | n/a                | GND                  | GND               |
  -----------------------------------------------------------------------------------------
```

### ESC Pinout

![image](images/esc-pinout.jpg)

### Configure the project

Use the command below to configure project using Kconfig menu as showed in the table above.
The default Kconfig values can be changed such as: EXAMPLE_TASK_STACK_SIZE, EXAMPLE_UART_BAUD_RATE, EXAMPLE_UART_PORT_NUM (Refer to Kconfig file).
```
idf.py menuconfig
```

### Build and Flash

Build the project and flash it to the board, then run monitor tool to view serial output:

```
idf.py -p PORT flash monitor
```

(To exit the serial monitor, type ``Ctrl-]``.)

See the Getting Started Guide for full steps to configure and use ESP-IDF to build projects.


## Troubleshooting

You are not supposed to see the echo in the terminal which is used for flashing and monitoring, but in the other UART configured through Kconfig can be used.
