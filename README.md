# ufr-protocol
Over UDP Fast Reliable protocol

## testing UDP to TCP performance

**1. Test UDP:**

- message format:

header  |  squence number  |  data length  |  payload
--------|------------------|---------------|-------------------
1 byte  |  2 bytes         |  2 bytes      |  up to 56 536 bytes

- test content
   - send messages directelly over UDP
   - receive messages
   - count a number of lost messages using "squence number"
   - measure elapsed time
   - measure average speed

- results
   - sent bytes: ...
   - sent messages: ...
   - received bytes: ...
   - received messages: ...

**2. Test TCP:**

- message format:

|  payload             |
|----------------------|
|  up to 56 536 bytes  |

- test content
   - send messages directelly over TCP
   - receive messages
   - measure elapsed time
   - measure average speed

- results
   - sent bytes: ...
   - sent messages: ...
   - received bytes: ...
   - received messages: ...

**3. Conclusion**

 test metric             | UDP                | TCP                
-------------------------|--------------------|--------------------
 sent bytes              | ...                | ...
 sent messages           | ...                | ...
 received bytes          | ...                | ...
 received messages       | ...                | ...
 elapsed time, sec       | ...                | ...
 everage speed, KB/sec   | ...                | ...


## Implementation

- Selected message format:

header  |  squence number  |  data length  |  payload
--------|------------------|---------------|-------------------
1 byte  |  2 bytes         |  2 bytes      |  up to 56 536 bytes

- On the Client side:
   - read messages from UDP
   - push each received messages into the output queue
   - if squence number missed (configurable number of resend requests, default 3)
      - start timer (configurable, default 100 ms)
         - if timer is over 
            - message is missed
               - requesting resend
         - if during timer message receivedесли
            - stop the timer
            - push message into the output queue
   - continue

- On the Server side:
   - sending messages incremening sequence number
   - push each into the cache: {key: squence number, value: message}
   - if cache length exceeded, drop first message
   - if resend requested
      - get requested message from the cache
      - send it
   - continue 
