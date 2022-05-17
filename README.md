# Computer System Interfaces | The Silesian University of Technology

## Wojciech Mielczarek, PhD | Computer Science, BSc

![CSI Miami](https://c.tenor.com/FrbcnrE3U68AAAAd/blow-up-walking-away.gif)

This is the repostiory for the class project for Computer Systems Interfaces. It contains an application that implements the ModBus protocol.

Proudly developed by the apes of In5matics during the 6th semester of the Computer Science BSc.

![Apes](https://i.kym-cdn.com/photos/images/newsfeed/001/676/568/d02.png)

We will develop this application using Python and PyModbus lib.

An extract from PyModbus docs:

"Pymodbus is a full Modbus protocol implementation using twisted/tornado/asyncio for its asynchronous communications core. It can also be used without any third party dependencies (aside from pyserial) if a more lightweight project is needed."

## App Specifications:

**The program implements the functions of the physical, data link and application (in the very
limited extend) layers of the MODBUS-ASCII bus (OB).
Remark:
Implementing MODBUS-RTU will be warmly appreciated although is only OP.**

Functions of the program:

1.  MODBUS unit mode selection: Master or Slave

    1.  Master unit: - Implementation of an addressed and broadcast transaction. - Transmission parameters setting: bit rate and character format (based on COM port parameters).
        **_Remark: The transmission parameters can be set permanently (none selection is required) because in the case of MODBUS protocol handling we are interested rather in link layer and application layer parameters than in physical layer parameters._**

        - Preparing the query frame:

          - selecting the slave unit by its address,
          - selecting the operation (command),
          - preparing data (command arguments),
          - control sum calculating: ASCI transmission mode – LRC, RTU mode – CRC).
          - appending the terminator (ASCII mode – CR,LF, RTU mode – time interval).

        - Sending the frame at the operator's require.
        - The master unit operates under the control of 3 parameters:
          - transaction timeout set in the range from 0 to 10 s, with resolution of 100 ms
          - number of retransmissions in case of failure of subsequent transactions (set in the range 0 to 5.  timeout (from 0 to 1 s, with resolution of 10 ms) limiting the space between subsequent characters in the frame. This parameters guarantees the continuity of the frame and must be checked by any receiving device, both the slave (receives the query) and master (receives the response.

    2.  Slave unit
        - Query frame receipt,
        - Frame validation (testing the control sum to consider if the frame is not corrupted),
        - Checking the destination address,
        - If the slave is “addressed” (or in case of broadcast) executing the command.
        - Returning the “normal response” or the “exception response”.
        - Slave operation is controlled by 2 parameters:
          - slave address (set in the range from 1 to 247)
          - timeout (from 0 to 1 s, with resolution of 10 ms) limiting the space between subsequent characters in the query frame.

2.  Application layer
    You only need to implement two custom orders: - command code = 1 - sending the text from the Master station to the Slave station. The text entered into the edit window at the Master is transferred (write operation) to the slave and displayed in the "Text received" window at the slave station. This command can be used in addressed transaction or broadcast transaction. - command code = 2 - reading the text from the Slave station and displaying the text in the "Text received ” window at the Master. This command can only be used in addressed transaction.
    **_Remark: In the MASTER station and in the SLAVE station, it should be possible to preview frames sent and received in hexadecimal code._**
