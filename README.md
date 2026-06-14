
AES-CBC Encryption (Şifrələmə)

def solution(key: str, iv: str, plaintext: str) -> str:
    k = bytes.fromhex(key)
    v = bytes.fromhex(iv)
    p = pkcs7_pad(plaintext.encode())
    cbc = b''
    for i in range(0, len(p), 16):
        v = aes_encrypt_block(k, bytes(a^b for a,b in zip(p[i:i+16], v)))
        cbc += v
    return out.hex()

AES-CBC Decryption (Şifrəni Açmaq).

def solution(key: str, iv: str, ciphertext: str) -> str:
    k = bytes.fromhex(key)
    v = bytes.fromhex(iv)
    c = bytes.fromhex(ciphertext)
    cbc = b''
    for i in range(0, len(c), 16):
        block = c[i:i+16]
        cbc += bytes(a^b for a,b in zip(aes_decrypt_block(k, block), v))
        v = block
    return pkcs7_unpad(cbc).decode()
BLOCK OUT V------ BLOCK CBC V

AES-ECB Encryption (Şifrələmə)

def solution(key: str, plaintext: str) -> str:
    k = bytes.fromhex(key)
    d = pkcs7_pad(plaintext.encode())
    ecb = b''
    for i in range(0, len(d), 16):
        ecb += aes_encrypt_block(k, p[i:i+16])
    return ecb.hex()

AES-ECB Decryption (Şifrəni Açmaq)

def solution(key: str, ciphertext: str) -> str:
    k = bytes.fromhex(key)
    p = bytes.fromhex(ciphertext)
    out = b''
    for i in range(0, len(d), 16):
        out += aes_decrypt_block(k, p[i:i+16])
    return pkcs7_unpad(out).decode()

AES-CTR Decryption (Şifrəni Açmaq) !!!!!!!!!

def solution(key: str, nonce: str, ciphertext: str) -> str:
    k = bytes.fromhex(key)
    n = bytes.fromhex(nonce)
    c = bytes.fromhex(ciphertext)
    ctr = b''
    for i in range(0, len(c), 16):
        ctr += bytes(a^b for a,b in zip(c[i:i+16],
                   aes_encrypt_block(k, n + (i//16).to_bytes(8, 'big'))))
    return ctr.decode()

Detect ECB vs CBC

def solution(ciphertext: str) -> str:
    b = [ciphertext[i:i+32] for i in range(0, len(ciphertext), 32)]
    return "ECB" if len(b) != len(set(b)) else "CBC"

5. RSA Ailəsi 14.06
•	RSA Encryption !
•	RSA Decryption !
•	Derive RSA Private Exponent 
•	RSA Sign !
•	RSA Verify Signature
•	RSA Decrypt to UTF-8

RSA Encryption !

def solution(n: int, e: int, m: int) -> int:
    return pow(m, e, n)

RSA Decryption !

def solution(n: int, d: int, c: int) -> int:
    return pow(c, d, n)

Derive RSA Private Exponent !

def solution(p, q, e):
    return pow(e, -1, (p-1)*(q-1))

RSA Sign !

def solution(n: int, d: int, m: int) -> int:
    return pow(m, d, n)

RSA Verify Signature !

def solution(n: int, e: int, s: int, m: int) -> str:
    return "VALID" if pow(s, e, n) == m else "INVALID"


RSA Decrypt to UTF-8

def solution(n: int, d: int, c: int) -> str:
    m = pow(c, d, n)
    return m.to_bytes((m.bit_length()+7)//8, "big").decode()



HMAC Ailəsi 16.06
•	HMAC-SHA1 Verify
•	HMAC-SHA256 Verify
•	HMAC-SHA1 Generate
•	HMAC-MD5 Generate’
•	HMAC vs Naive H(key||msg
1) HMAC-SHA1 Verify
import hmac,hashlib
def solution(k,m,t):
    return "VALID" if hmac.new(bytes.fromhex(k),m.encode(),hashlib.sha1).hexdigest()==t else "INVALID"
2) HMAC-SHA256 Verify
import hmac,hashlib
def solution(k,m,t):

    return "VALID" if hmac.new(k.encode(),m.encode(),hashlib.sha256).hexdigest()==t else "INVALID"
3) HMAC-SHA1 Generate
import hmac,hashlib

def solution(k,m):
    return hmac.new(bytes.fromhex(k),m.encode(),hashlib.sha1).hexdigest()
4) HMAC-MD5 Generate
 import hmac,hashlib

def solution(k,m):
    return hmac.new(bytes.fromhex(k),m.encode(),hashlib.md5).hexdigest()
5) HMAC vs Naive H(key||msg)
import hashlib,hmac

def solution(k,m):
    naive = hashlib.sha256((k+m).encode()).hexdigest()
    real = hmac.new(k.encode(),m.encode(),hashlib.sha256).hexdigest()
    return [naive,real]


Hashing Ailəsi. 17.06
