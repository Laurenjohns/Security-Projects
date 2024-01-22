## Security Projects

### AES Encryption

Project Overview: Symmetric AES encryption in Python.

---
```python
from Crypto.Random import get_random_bytes
from Crypto.Protocol.KDF import PBKDF2
from Crypto.Cipher import AES
from Crypto.Util.Padding import pad, unpad


simple_key = get_random_bytes(32)
print(simple_key)

salt = b'mysimplekey'
password = "mypassword"

key = PBKDF2(password, salt, dkLen=32)

message = "Hello Secret World!"
message_bytes = message.encode('utf-8')

cipher = AES.new(key, AES.MODE_CBC)
ciphered_data = cipher.encrypt(pad(message_bytes, AES.block_size))

print(ciphered_data)

with open('encrypted.bin', 'wb') as f:
    f.write(cipher.iv)
    f.write(ciphered_data)

with open('encrypted.bin', 'rb') as f:
    iv = f.read(16)
    decrypt_data = f.read()

cipher = AES.new(key, AES.MODE_CBC, iv=iv)
original = unpad(cipher.decrypt(decrypt_data), AES.block_size)
print(original)
```
```python
#export the key
from Crypto.Random import get_random_bytes
from Crypto.Protocol.KDF import PBKDF2
from Crypto.Cipher import AES
from Crypto.Util.Padding import pad, unpad

with open('key.bin', 'rb') as f:
    key = f.read()

with open ('encrypted.bin', 'rb') as f:
    iv = f.read(16)
    decrypt_data = f.read()

cipher = AES.new(key, AES.MODE_CBC, iv=iv)
original = unpad(cipher.decrypt(decrypt_data), AES.block_size)
print(original)
```
---
