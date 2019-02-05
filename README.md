# Transistor-tools-K2636
A driver for controlling a keithley 2636.
The K2636.py program in this folder loads a set of .tsp instructions into the memory of the Keithley. It then tells the keithley to execute the instructions before closing the connection with the instrument.

# User interface
To start the user interface run the following command:

>python ofetMeasure.py

# Example python script:
You can take the driver to script your own programs:

>keithley = K2636(address='ASRL/dev/ttyUSB0', read_term='\n', baudrate=57600)

>sample = 'ofet1'

>keithley.IVsweep(sample)

>keithley.Output(sample)

>keithley.Transfer(sample)

>keithley.DisplayMeasurement(sample)

>keithley.closeConnection()


# Requirements:
It is written is python3. You will need to download the following modules too:
- visa
- serial
- matplotlib
- pandas
- for remote control:
	export XKB_DEFAULT_RULES=base
	export QT_XKB_CONFIG_ROOT=/usr/share/X11/xkb

# How to hook up the keithley 2636 for three terminal OFET measurements:
![Alt text](.K2636_connections.png?raw=true "Setup")

# Things to note
- The Keithley 2636 uses 'TSP' rather than 'SCPI' which the Keithley 2400 understood.
- Other than the change in syntax, the way the commands are executed have changed. Now the Keithley now loads an entire script's worth of commands into it's non-volatile memory before execution. This means it's faster than before.
- The .tsp files in this repo are scripts which can be loaded into the K2636.
- .tsp are written in Lua (http://www.lua.org). Comments begin with '--'
- For more info on TSP check out the following links:
	- http://www.tek.com/sites/tek.com/files/media/document/resources/2616%20SCPI_to_TSP_AN.pdf
	- https://forum.tek.com/viewtopic.php?t=121440
