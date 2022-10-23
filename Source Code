from ctypes.wintypes import LONG
import random
from sympy import randprime
#generate large prime numbers p and q
p = randprime(2 ** 14, (2 ** 18) - 1)
q = randprime(2 ** 14, (2 ** 18) - 1)

# calculate n and phi for specific p and q
n = p * q
totient = (p - 1) * (q - 1)

# calculate e
def GCD(e, t=totient):
    while t != 0:
        e, t = t, e % t
    return e

# return the value of e such that GCD(e t =totient) == 1 and e < totient
for i in range(5000, 10000):
    if (GCD(i, totient) == 1):
        e = i
        break

# create 2 methods that do inversing and pelverising
def Pulverizer(a, b):
    if (a % b == 0):
        return (b, 0, 1)
    else:
        gcd, s, t = Pulverizer(b, a % b)
        s = s - ((a // b) * t)
        print("%d = %d*(%d) + (%d)*(%d)" % (gcd, a, t, s, b))
        return (gcd, t, s)


def inverse(e, t=totient):
    gcd, s, _ = Pulverizer(e, t)
    if (gcd != 1):
        return None
    else:
        return s % t

# generate d
d = inverse(e, totient)
# write public and private key
publickey = (e,n)
privatekey = (d,n)

class RSA():
    
    def encrypt(self,message, publicKey):
        e, n = publicKey
        word = ""
        message.upper()
        for i in message:
            m = ord(i)
            encrypted = pow(m, e, n)
            word += str(encrypted)
            word += "o"
        return word

    def decrypt(self,privateKey, encrypted_message):
        d, n = privateKey
        new = str(encrypted_message).split("o")
        mapped_text = map(int,new)

        for char in mapped_text:
            text =  chr((char ** d) % n) 
        return ''.join(text)
