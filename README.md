# EX10-DiffeeHellman
## AIM:
To implement the Diffee Hellman Algoirthm using C or Python.

## DESIGN STEPS:
### Step 1:
Design the Diffie-Hellman key exchange algorithm.

### Step 2:
Implement the algorithm using C.

### Step 3:
The Diffie-Hellman algorithm uses a large prime number p and a primitive root g. Both Eve and David select private keys and exchange public keys computed using the formula:

Public Key = (g^Private Key) % p
After exchanging public keys, both compute a shared secret key using:

Shared Secret = (Other's Public Key^Private Key) % p

## PROGRAM:
```c
#include <stdio.h>
#include <math.h>

// Function to calculate (base^exp) % mod using modular exponentiation
int modExp(int base, int exp, int mod) {
    int result = 1;
    base = base % mod;
    while (exp > 0) {
        if (exp % 2 == 1) {
            result = (result * base) % mod;
        }
        exp = exp >> 1;
        base = (base * base) % mod;
    }
    return result;
}

int main() {
    // Publicly known values
    int p = 23;  // A large prime number
    int g = 5;   // A primitive root modulo p
    
    // Private keys (chosen secretly by Jack and Rose)
    int jackPrivateKey, rosePrivateKey;
    printf("Enter Jack's private key: ");
    scanf("%d", &jackPrivateKey);
    printf("Enter Rose's private key: ");
    scanf("%d", &rosePrivateKey);
    
    // Public keys (computed from private keys)
    int jackPublicKey = modExp(g, jackPrivateKey, p);  // Jack's public key
    int rosePublicKey = modExp(g, rosePrivateKey, p);  // Rose's public key
    
    printf("Jack's Public Key: %d\n", jackPublicKey);
    printf("Rose's Public Key: %d\n", rosePublicKey);
    
    // Shared secret keys (computed from the other's public key and own private key)
    int sharedKeyJack = modExp(rosePublicKey, jackPrivateKey, p);  // Jack computes the shared secret key
    int sharedKeyRose = modExp(jackPublicKey, rosePrivateKey, p);  // Rose computes the shared secret key
    
    printf("Shared Secret Key (Jack): %d\n", sharedKeyJack);
    printf("Shared Secret Key (Rose): %d\n", sharedKeyRose);
    
    // The shared keys should be the same
    if (sharedKeyJack == sharedKeyRose) {
        printf("Key Exchange Successful! Shared Secret Key: %d\n", sharedKeyJack);
    } else {
        printf("Key Exchange Failed!\n");
    }

    return 0;
}
```
## OUTPUT:
![image](https://github.com/user-attachments/assets/aad098f8-c9b1-4dc0-97d8-85b2fd3033a1)


## RESULT:
Thus the implementation of Diffe Hellman Algorithm executed successfully.
