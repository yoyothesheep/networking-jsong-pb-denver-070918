
# Networking

### Exercise

#### Check the cheat sheet for the network message structure.

#### 9.1. Parse this message
```
f9beb4d976657261636b000000000000000000005df6e0e2
```


```python
# Exercise 9.1

msg = bytes.fromhex('f9beb4d976657261636b000000000000000000005df6e0e2')

# first 4 are network magic
# next 12 are command
# next 4 are payload length
# next 4 are checksum
# rest is payload
```

# Test Driven Exercise


```python
from network import NetworkEnvelope

class NetworkEnvelope(NetworkEnvelope):
    
    @classmethod
    def parse(cls, s):
        '''Takes a stream and creates a NetworkEnvelope'''
        # check the network magic NETWORK_MAGIC
        # check the network magic b'\xf9\xbe\xb4\xd9'
        # command 12 bytes
        # payload length 4 bytes, little endian
        # checksum 4 bytes, first four of double-sha256 of payload
        # payload is of length payload_length
        # verify checksum
        pass

    def serialize(self):
        '''Returns the byte serialization of the entire network message'''
        # add the network magic NETWORK_MAGIC
        # command 12 bytes
        # payload length 4 bytes, little endian
        # checksum 4 bytes, first four of double-sha256 of payload
        # payload
        pass
```

### Exercise 10

#### 10.1. Parse this message
```
f9beb4d974780000000000000000000002010000e293cdbe01000000016dbddb085b1d8af75184f0bc01fad58d1266e9b63b50881990e4b40d6aee3629000000008b483045022100f3581e1972ae8ac7c7367a7a253bc1135223adb9a468bb3a59233f45bc578380022059af01ca17d00e41837a1d58e97aa31bae584edec28d35bd96923690913bae9a0141049c02bfc97ef236ce6d8fe5d94013c721e915982acd2b12b65d9b7d59e20a842005f8fc4e02532e873d37b96f09d6d4511ada8f14042f46614a4c70c0f14beff5ffffffff02404b4c00000000001976a9141aa0cd1cbea6e7458a7abad512a9d9ea1afb225e88ac80fae9c7000000001976a9140eab5bea436a0484cfab12485efda0b78b4ecc5288ac00000000
```



```python
# Exercise 10.1

from io import BytesIO

from network import NetworkEnvelope

stream = BytesIO(bytes.fromhex('f9beb4d974780000000000000000000002010000e293cdbe01000000016dbddb085b1d8af75184f0bc01fad58d1266e9b63b50881990e4b40d6aee3629000000008b483045022100f3581e1972ae8ac7c7367a7a253bc1135223adb9a468bb3a59233f45bc578380022059af01ca17d00e41837a1d58e97aa31bae584edec28d35bd96923690913bae9a0141049c02bfc97ef236ce6d8fe5d94013c721e915982acd2b12b65d9b7d59e20a842005f8fc4e02532e873d37b96f09d6d4511ada8f14042f46614a4c70c0f14beff5ffffffff02404b4c00000000001976a9141aa0cd1cbea6e7458a7abad512a9d9ea1afb225e88ac80fae9c7000000001976a9140eab5bea436a0484cfab12485efda0b78b4ecc5288ac00000000'))
```

### Exercise 11

Use https://bitnodes.earn.com/nodes/ to find nodes to connect to.

#### 11.1. Run the code below and parse some messages

#### Bonus: Run the connect.py script in the terminal to see how asynchronous connections can work


```python
import socket
s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
msg = bytes.fromhex('f9beb4d976657273696f6e0000000000650000005f1a69d2721101000100000000000000bc8f5e5400000000010000000000000000000000000000000000ffffc61b6409208d010000000000000000000000000000000000ffffcb0071c0208d128035cbc97953f80f2f5361746f7368693a302e392e332fcf05050001')
s.connect(('46.101.99.121', 8333))
s.sendall(msg)
data = s.recv(200)
print(data.hex())
```


    ---------------------------------------------------------------------------

    OSError                                   Traceback (most recent call last)

    <ipython-input-5-71063165afd9> in <module>()
          2 s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
          3 msg = bytes.fromhex('f9beb4d976657273696f6e0000000000650000005f1a69d2721101000100000000000000bc8f5e5400000000010000000000000000000000000000000000ffffc61b6409208d010000000000000000000000000000000000ffffcb0071c0208d128035cbc97953f80f2f5361746f7368693a302e392e332fcf05050001')
    ----> 4 s.connect(('46.101.99.121', 8333))
          5 s.sendall(msg)
          6 data = s.recv(200)


    OSError: [Errno 51] Network is unreachable

