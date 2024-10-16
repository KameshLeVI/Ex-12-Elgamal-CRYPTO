# Ex-12-Elgamal-CRYPTO
## AIM:
To encrypt and decrypt a message using the ElGamal encryption algorithm.

## DESIGN STEPS:
Step 1:
Choose a large prime number p and a generator g of the multiplicative group of integers modulo p.

Step 2:
Alice chooses a private key and computes her public key as
```
public_key = g^private_key mod p.
```
Step 3:
To encrypt a message, Bob chooses a random number k and computes a ciphertext pair (c1, c2).

Step 4:
To decrypt the message, Alice uses her private key and computes the original message.

Step 5:
The decrypted message is verified to be the same as the original.

## PROGRAM:
```
#include <stdio.h>
#include <math.h>
long long int modExp(long long int base, long long int exp, long long int mod) {
    long long int result = 1;
    while (exp > 0) {
        if (exp % 2 == 1) {
            result = (result * base) % mod;
        }
        base = (base * base) % mod;
        exp = exp / 2;
    }
    return result;
}

int main() {
    long long int p, g, privateKeyA, publicKeyA;
    long long int k, message, c1, c2, decryptedMessage;
    printf("Enter a large prime number (p): ");
    scanf("%lld", &p);
    printf("Enter a generator (g): ");
    scanf("%lld", &g);

    printf("Enter shin's private key: ");
    scanf("%lld", &privateKeyA);

    publicKeyA = modExp(g, privateKeyA, p);
    printf("shin's public key: %lld\n", publicKeyA);

    printf("Enter the message to encrypt (as a number): ");
    scanf("%lld", &message);
    printf("Enter a random number k: ");
    scanf("%lld", &k);

    c1 = modExp(g, k, p);
    c2 = (message * modExp(publicKeyA, k, p)) % p;
    printf("Encrypted message (c1, c2): (%lld, %lld)\n", c1, c2);

    decryptedMessage = (c2 * modExp(c1, p - 1 - privateKeyA, p)) % p;
    printf("Decrypted message: %lld\n", decryptedMessage);

    return 0;
}
```
## OUTPUT:
![image](https://github.com/user-attachments/assets/a1a6698b-5dd7-4803-a33e-6b836568fe8e)



## RESULT:
The program for ElGamal encryption and decryption was executed successfully. Alice and Bob exchanged an encrypted message and verified that the decrypted message matched the original message.
