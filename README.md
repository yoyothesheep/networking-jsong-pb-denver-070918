
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
from io import BytesIO
from network import NetworkEnvelope
from helper import (
    double_sha256,
    int_to_little_endian,
    little_endian_to_int
)

NETWORK_MAGIC = b'\xf9\xbe\xb4\xd9'


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
