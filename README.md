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

|
| sent bytes: ...
| sent messages: ...
| received bytes: ...
| received messages: ...


## Implementation

- Selected message format:

header  |  squence number  |  data length  |  payload
--------|------------------|---------------|-------------------
1 byte  |  2 bytes         |  2 bytes      |  up to 56 536 bytes

- On the Client side:
   - put all received messages into the output queue

   - если squence number пропущен, (можно настоить количество повторений при неудаче)
      - запускается таймер, 
         - если таймер истекает,
            - посылка считается потерянной - отправляем запрос серверу на повторную отправку этой посылки 
         - если таймер не истек, а посылка дошла, просто идем дальше

- On the Server side:
   - sending messages incremening sequence number
