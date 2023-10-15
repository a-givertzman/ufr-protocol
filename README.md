# ufr-protocol
Over UDP Fast Reliable protocol

## testing UDP to TCP performance

**1. Test UDP:**

message format:
header  |  squence number  |  data length  |  payload
--------|------------------|---------------|-------------------
1 byte  |  2 bytes         |  2 bytes      |  up to 56 536 bytes

- send messages directelly over UDP
- receive messages
- count a number of lost messages using "squence number"
- measure elapsed time
- measure average speed

**2. Test TCP:**

- send messages directelly over UDP
- receive messages
- count a number of lost messages using "squence number"
- measure elapsed time
- measure average speed

- пакет будет содержать только payload: 56 536 bytes

- так же замерим скорость и среднюю скорость за весь перод передачи


если в результате тестов будет понятно что UDP существенно выигрываети, будет смысл пытаться переходить

и так же можно попробовать реализовать простой вариант для передачи Point-ов просто для тестирования пока...

допустим посылка такая: 
header: 1 byte
squence number: 2 bytes
data length: 2 bytes
payload: up to 56 536 bytes

на стороне клиента:
- складываем все полученные посылки в очередь, из нее пользователь получает приходящие данные

- если squence number пропущен, (можно настоить количество повторений при неудаче)
   - запускается таймер, 
      - если таймер истекает,
         - посылка считается потерянной - отправляем запрос серверу на повторную отправку этой посылки 
      - если таймер не истек, а посылка дошла, просто идем дальше

на стороне сервера:
