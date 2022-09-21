In order to record data from the flow meter with a small time step, we need to use two tools: Hterm to set up the flow meter and our own script to get the data sent by the flow meter and record them in a csv file.


Download Hterm :   This allows serial communication with the flow meter. Advised configuration:

Baud=19200

Port=15 or other

Newline at: CR

Send on enter at : CR

Ascii

When connected, write these commands :

1:    *@=@  (streaming mode)

2:    *@=A  (pulling mode)

3:     A$$W91=30  (set up the time step value to 30ms. Be careful, going too little can result in a bug, minimum advice would be 20ms.)

4:    *@=@


With the Python script named “flowReader.py” we can now get the values sent by the flow meter and record them in a csv file. (If prefer, you can work with the code CommunicationS358Python.py which work with no graphic interface)

Modify the script to fit your set up: port=”COM11” for exemple.

When running the script, a window opens. Choose the number of iterations and hit “Start record”. This will create a csv file named according to the time and record the data. Choosing to many iterations might crash the program. Usually, 1500 or 2000 iterations are enough. 



The most common error happening is : SerialException: could not open port 'COM15': PermissionError(13, 'Access is denied.', None, 5) That means the serial is still connected, and is not possible to create a new connection. Try to close the connection, by for example unplugging the USB.
